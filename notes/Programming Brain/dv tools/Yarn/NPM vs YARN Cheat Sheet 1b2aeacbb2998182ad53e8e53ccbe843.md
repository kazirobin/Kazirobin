# NPM vs YARN Cheat Sheet

This is a cheat sheet that you can use as a handy reference for npm & Yarn commands.

There are many similarities between [npm](https://www.npmjs.com/) and [Yarn](https://yarnpkg.com/). **Yarn** (released 2016) drew considerable inspiration from **npm** (2010).

Here is a useful reference to keep the two CLIs straight:

| Command | NPM | YARN |
| --- | --- | --- |
| Install dependencies | `npm install` | `yarn` |
| Install package | `npm install [package]` | `yarn add [package]` |
| Install dev package | `npm install --save-dev [package]` | `yarn add --dev [package]` |
| Uninstall package | `npm uninstall [package]` | `yarn remove [package]` |
| Uninstall dev package | `npm uninstall --save-dev [package]` | `yarn remove [package]` |
| Update | `npm update` | `yarn upgrade` |
| Update package | `npm update [package]` | `yarn upgrade [package]` |
| Global install package | `npm install --global [package]` | `yarn global add [package]` |
| Global uninstall package | `npm uninstall --global [package]` | `yarn global remove [package]` |

Here are some commands that **Yarn** decided not to change:

| NPM | YARN |
| --- | --- |
| `npm init` | `yarn init` |
| `npm run` | `yarn run` |
| `npm test` | `yarn test` |
| `npm login` (and `logout`) | `yarn login` (and `logout`) |
| `npm link` | `yarn link` |
| `npm publish` | `yarn publish` |
| `npm cache clean` | `yarn cache clean` |