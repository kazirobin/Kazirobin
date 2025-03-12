# Component Hierarchy

The React components defined in special files of a route segment are rendered in a specific hierarchy:

- `layout.js`
- `template.js`
- `error.js` (React error boundary)
- `loading.js` (React suspense boundary)
- `not-found.js` (React error boundary)
- `page.js` or nested `layout.js`

[file-conventions-component-hierarchy.avif](Component%20Hierarchy%201b2aeacbb299812aa554ec530dec31d8/file-conventions-component-hierarchy.avif)

In a nested route, the components of a segment will be nested **inside** the components of its parent segment.

[nested-file-conventions-component-hierarchy.avif](Component%20Hierarchy%201b2aeacbb299812aa554ec530dec31d8/nested-file-conventions-component-hierarchy.avif)