# Prettier Setup

Plugins and configuration settings that can improve the developer experience when working with Tailwind CSS.

## Automatic class sorting with Prettier

To get started, install `prettier-plugin-tailwindcss` as a dev-dependency:

```bash
npm install -D prettier prettier-plugin-tailwindcss
```

Then add the plugin to your Prettier configuration:

Create a `.prettierrc` file and place it in the root of your project.

```json
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```