# Composition Patterns

When building React applications, you will need to consider what parts of your application should be rendered on the server or the client. This page covers some recommended composition patterns when using Server and Client Components.

## When to use Server and Client Components?

Here's a quick summary of the different use cases for Server and Client Components:

| **What do you need to do?** | **Server Component** | **Client Component** |
| --- | --- | --- |
| Fetch data | YES | NO |
| Access backend resources (directly) | YES | NO |
| Keep sensitive information on the server (access tokens, API keys, etc) | YES | NO |
| Keep large dependencies on the server / Reduce client-side JavaScript | YES | NO |
| Add interactivity and event listeners (`onClick()`, `onChange()`, etc) | NO | YES |
| Use State and Lifecycle Effects (`useState()`, `useReducer()`, `useEffect()`, etc) | NO | YES |
| Use browser-only APIs | NO | YES |
| Use custom hooks that depend on state, effects, or browser-only APIs | NO | YES |
| Use React Class components | NO | YES |

[**Server Component Patterns**](Composition%20Patterns%201b2aeacbb2998192b11bf27a8999340e/Server%20Component%20Patterns%201b2aeacbb2998139a77cfbed792a8d2d.md)

[**Client Components**](Composition%20Patterns%201b2aeacbb2998192b11bf27a8999340e/Client%20Components%201b2aeacbb299810c95d5ccd24b458ceb.md)

[Interleaving Server and Client Components](Composition%20Patterns%201b2aeacbb2998192b11bf27a8999340e/Interleaving%20Server%20and%20Client%20Components%201b2aeacbb2998106a017fd7de54d1914.md)