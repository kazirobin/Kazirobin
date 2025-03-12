# Optimizing

Next.js comes with a variety of built-in optimizations designed to improve your application's speed and [Core Web Vitals](https://web.dev/vitals/). This guide will cover the optimizations you can leverage to enhance your user experience.

## Built-in Components

Built-in components abstract away the complexity of implementing common UI optimizations. These components are:

- **Images**: Built on the native `<img>` element. The Image Component optimizes images for performance by lazy loading and automatically resizing images based on device size.
- **Link**: Built on the native `<a>` tags. The Link Component prefetches pages in the background, for faster and smoother page transitions.
- **Scripts**: Built on the native `<script>` tags. The Script Component gives you control over loading and execution of third-party scripts.

## Metadata

Metadata helps search engines understand your content better (which can result in better SEO), and allows you to customize how your content is presented on social media, helping you create a more engaging and consistent user experience across various platforms.

The Metadata API in Next.js allows you to modify the `<head>` element of a page. You can configure metadata in two ways:

- **Config-based Metadata**: Export a static `metadata` object or a dynamic `generateMetadata` function in a `layout.js` or `page.js` file.
- **File-based Metadata**: Add static or dynamically generated special files to route segments.

Additionally, you can create dynamic Open Graph Images using JSX and CSS with imageResponse constructor.

## Static Assets

Next.js `/public` folder can be used to serve static assets like images, fonts, and other files. Files inside `/public` can also be cached by CDN providers so that they are delivered efficiently.

## Analytics and Monitoring

For large applications, Next.js integrates with popular analytics and monitoring tools to help you understand how your application is performing.

---

[**Image Optimization**](Optimizing%201b2aeacbb299818ebc7afe9a3da4e544/Image%20Optimization%201b2aeacbb299816c82afc1cd19bf52a0.md)

[**Font Optimization**](Optimizing%201b2aeacbb299818ebc7afe9a3da4e544/Font%20Optimization%201b2aeacbb299815faccffe07e490ab63.md)

[**Metadata**](Optimizing%201b2aeacbb299818ebc7afe9a3da4e544/Metadata%201b2aeacbb2998124b8c7cdebab67b3d7.md)

[**Static Assets**](Optimizing%201b2aeacbb299818ebc7afe9a3da4e544/Static%20Assets%201b2aeacbb2998180a834ff3c8f51fba3.md)