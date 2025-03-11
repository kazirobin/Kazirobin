# The App Router

In version 13, Next.js introduced a new **App Router** built on React Server Components, which supports shared layouts, nested routing, loading states, error handling, and more.

The App Router works in a new directory named `app`. The `app` directory works alongside the `pages` directory to allow for incremental adoption. This allows you to opt some routes of your application into the new behavior while keeping other routes in the `pages` directory for previous behavior. If your application uses the `pages` directory, please also see the [Pages Router](https://nextjs.org/docs/pages/building-your-application/routing) documentation.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**: The App Router takes priority over the Pages Router. Routes across directories should not resolve to the same URL path and will cause a build-time error to prevent a conflict.

</aside>

[next-router-directories.avif](The%20App%20Router%201b2aeacbb299810ea9a3f51a1779a75a/next-router-directories.avif)

By default, components inside `app` are React Server Components. This is a performance optimization and allows you to easily adopt them, and you can also use Client Components.