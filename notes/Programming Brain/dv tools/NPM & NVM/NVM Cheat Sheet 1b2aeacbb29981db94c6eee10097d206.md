# NVM Cheat Sheet

NVM (Node Version Manager) is a command-line utility that **allows developers to manage multiple Node.** **js versions easily**. NVM provides a simple interface to install, switch, and remove Node. js versions, enabling developers to work on different projects without worrying about compatibility issues.

---

➤ Lists all of the available versions of NodeJs on remote

```bash
nvm ls-remote
#or
nvm list available
```

➤ Lists all of the available LTS versions of NodeJs on remote

```bash
nvm ls-remote --lts
```

➤ List locally installed NodeJs version

```bash
nvm ls
```

➤ Install a specific version 0.12.3 (see ls-remote for available options)

```bash
nvm install 0.12.3
```

➤ Install the latest LTS release

```bash
nvm install --lts
```

➤ Install latest NPM release only

```bash
nvm install-latest-npm
```

➤ Switch to and use the installed 0.12.3 version

```bash
nvm use 0.12.3
```

➤ Switch to the latest LTS version

```bash
nvm use --lts
```

➤ The path to the installed node version

```bash
nvm which 0.12.2
```

➤ What is the current installed nvm version

```bash
nvm current
```

➤ Set the default node to the installed 0.10.32 version

```bash
nvm alias default 0.10.32
```

➤ Sets a user-defined alias to a versions

```bash
nvm alias <alias_name> <node_version>
```

➤ Deletes the alias named

```bash
nvm unalias <alias_name> 
```

➤ Uninstall a specific version

```bash
nvm uninstall <node_version>
```

➤ Uninstall the latest LTS release

```bash
nvm uninstall --lts
```

➤ The help documents

```bash
nvm --help
```