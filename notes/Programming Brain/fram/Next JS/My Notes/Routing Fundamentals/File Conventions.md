# File Conventions

Next.js provides a set of special files to create UI with specific behavior in nested routes:

| `layout` | Shared UI for a segment and its children |
| --- | --- |
| `page` | Unique UI of a route and make routes publicly accessible |
| `loading` | Loading UI for a segment and its children |
| `not-found` | Not found UI for a segment and its children |
| `error` | Error UI for a segment and its children |
| `global-error` | Global Error UI |
| `route` | Server-side API endpoint |
| `template` | Specialized re-rendered Layout UI |
| `default` | Fallback UI for Parallel Routes |

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**: `.js`, `.jsx`, or `.tsx` file extensions can be used for special files.

</aside>