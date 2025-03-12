# Intercepting Routes

Intercepting routes allows you to load a route from another part of your application within the current layout. This routing paradigm can be useful when you want to display the content of a route without the user switching to a different context.

For example, when clicking on a photo in a feed, you can display the photo in a modal, overlaying the feed. In this case, Next.js intercepts the `/photo/123` route, masks the URL, and overlays it over `/feed`.

[intercepting-routes-soft-navigate.avif](Intercepting%20Routes%201b2aeacbb29981edaa6ae74c0043e6c7/intercepting-routes-soft-navigate.avif)

However, when navigating to the photo by clicking a shareable URL or by refreshing the page, the entire photo page should render instead of the modal. No route interception should occur.

[intercepting-routes-hard-navigate.avif](Intercepting%20Routes%201b2aeacbb29981edaa6ae74c0043e6c7/intercepting-routes-hard-navigate.avif)

## Convention

Intercepting routes can be defined with the `(..)` convention, which is similar to relative path convention `../` but for segments.

You can use:

- `(.)` to match segments on the **same level**
- `(..)` to match segments **one level above**
- `(..)(..)` to match segments **two levels above**
- `(...)` to match segments from the **root** `app` directory

For example, you can intercept the `photo` segment from within the `feed` segment by creating a `(..)photo` directory.

[intercepted-routes-files.avif](Intercepting%20Routes%201b2aeacbb29981edaa6ae74c0043e6c7/intercepted-routes-files.avif)

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> Note that the `(..)` convention is based on *route segments*, not the file-system.

</aside>

## Examples

### Modals

Intercepting Routes can be used together with Parallel Routes to create modals. This allows you to solve common challenges when building modals, such as:

- Making the modal content **shareable through a URL**.
- **Preserving context** when the page is refreshed, instead of closing the modal.
- **Closing the modal on backwards navigation** rather than going to the previous route.
- **Reopening the modal on forwards navigation**.

Consider the following UI pattern, where a user can open a photo modal from a gallery using client-side navigation, or navigate to the photo page directly from a shareable URL:

[intercepted-routes-modal-example.avif](Intercepting%20Routes%201b2aeacbb29981edaa6ae74c0043e6c7/intercepted-routes-modal-example.avif)

In the above example, the path to the `photo` segment can use the `(..)` matcher since `@modal` is a slot and **not** a segment. This means that the `photo` route is only one segment level higher, despite being two file-system levels higher.

### Good to know:

- Other examples could include opening a login modal in a top navbar while also having a dedicated `/login` page, or opening a shopping cart in a side modal.