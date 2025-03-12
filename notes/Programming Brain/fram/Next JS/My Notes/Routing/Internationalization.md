# Internationalization

Next.js enables you to configure the routing and rendering of content to support multiple languages. Making your site adaptive to different locales includes translated content (localization) and internationalized routes.

## Terminology

- **Locale:** An identifier for a set of language and formatting preferences. This usually includes the preferred language of the user and possibly their geographic region.
    - `en`: English as spoken in the United States.
    - `bn`: Bengali as spoken in Bangladesh.

## Routing Overview

It’s recommended to use the user’s language preferences in the browser to select which locale to use. Changing your preferred language will modify the incoming `Accept-Language` header to your application.

For example, using the following libraries, you can look at an incoming `Request` to determine which locale to select, based on the `Headers`, locales you plan to support, and the default locale.

At first, you need to install some npm packages.

```bash
npm install @formatjs/intl-localematcher negotiator
```

Create a file named **src/middleware.js**

```jsx
import { match } from '@formatjs/intl-localematcher'
import Negotiator from 'negotiator'
 
    const acceptedLanguage =
        request.headers.get("accept-language") ?? undefined;
    const headers = { "accept-language": acceptedLanguage };
    const languages = new Negotiator({ headers }).languages();

    return match(languages, locales, defaultLocale); // en or bn
```

Routing can be internationalized by either the sub-path (`/en/products`) or domain (`my-site.en/products`). With this information, you can now redirect the user based on the locale inside Middleware.

Create a file named **src/middleware.js**

```jsx
import { match } from "@formatjs/intl-localematcher";
import Negotiator from "negotiator";
import { NextResponse } from "next/server";

let locales = ["en", "bn"];
let defaultLocale = "en";

function getLocale(request) {
  const acceptedLanguage = request.headers.get("accept-language") ?? undefined;

  let headers = { "accept-language": acceptedLanguage };
  let languages = new Negotiator({ headers }).languages();

  return match(languages, locales, defaultLocale); // en or bn
}

export function middleware(request) {
  // get the pathname from request url
  const pathname = request.nextUrl.pathname;

  const pathnameIsMissingLocale = locales.every(
    (locale) =>
      !pathname.startsWith(`/${locale}`) && pathname !== `/${locale}/`,
  );

  if (pathnameIsMissingLocale) {
    // detect user's preference & redirect with a locale with a path eg: /en/page
    const locale = getLocale(request);

    return NextResponse.redirect(
      new URL(`/${locale}/${pathname}`, request.url),
    );
  }
}

export const config = {
  matcher: [
    // Skip all internal paths (_next, assets, api)
    "/((?!api|assets|.*\\..*|_next).*)",
    // Optional: only run on root (/) URL
    // '/'
  ],
};

```

Finally, ensure all special files inside `app/` are nested under `app/[lang]`. This enables the Next.js router to dynamically handle different locales in the route, and forward the `lang` parameter to every layout and page. For example:

Create a file named **src/app/[lang]/page.js**

```jsx
// You now have access to the current locale
// e.g. /en/products -> `lang` is "en"
export default async function Page({ params: { lang } }) {
  return ...
}
```

The root layout can also be nested in the new folder (e.g. `app/[lang]/layout.js`)

## Localization

Changing displayed content based on the user’s preferred locale, or localization, is not something specific to Next.js. The patterns described below would work the same with any web application.

Let’s assume we want to support both English and Dutch content inside our application. We might maintain two different “dictionaries”, which are objects that give us a mapping from some key to a localized string. For example:

Create a file named **src/dictionaries/en.json**

```jsx
{
  "products": {
    "cart": "Add to Cart"
  }
}
```

Create a file named **src/dictionaries/bn.json**

```jsx
{
  "products": {
    "cart": "কার্ডে যুক্ত করুন"
  }
}
```

We can then create a `getDictionary` function to load the translations for the requested locale:

Create a file named **src/dictionaries/index.js**

```jsx
import "server-only";

const dictionaries = {
    en: () => import("./en.json").then((module) => module.default),
    bn: () => import("./bn.json").then((module) => module.default),
};

export const getDictionary = async (locale) => dictionaries[locale]();

```

Given the currently selected language, we can fetch the dictionary inside of a layout or page.

```jsx
import { getDictionary } from '../dictionaries'
 
export default async function Page({ params: { lang } }) {
  const dict = await getDictionary(lang) // en
  return <button>{dict.products.cart}</button> // Add to Cart
}
```

Because all layouts and pages in the `app/` directory default to Server Components, we do not need to worry about the size of the translation files affecting our client-side JavaScript bundle size. This code will **only run on the server**, and only the resulting HTML will be sent to the browser.

## Static Generation

To generate static routes for a given set of locales, we can use `generateStaticParams` with page or layout. This can be global, for example, in the root layout:

```jsx
export async function generateStaticParams() {
  return [{ lang: 'en' }, { lang: 'bn' }]
}
 
export default function RootLayout({ children, params }) {
  return (
    <html lang={params.lang}>
      <body>{children}</body>
    </html>
  )
}
```