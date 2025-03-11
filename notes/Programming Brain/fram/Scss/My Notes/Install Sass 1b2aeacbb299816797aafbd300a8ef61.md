# Install Sass

When you install Sass on the command line, you’ll be able to run the `sass` executable to compile `.sass` and `.scss` files to `.css` files. For example:

```jsx
sass source/stylesheets/index.scss build/stylesheets/index.css
```

First install Sass using one of the options below, then run `sass --version` to be sure it installed correctly. If it did, this will include `1.76.0`. You can also run `sass --help` for more information about the command-line interface.

Once it’s all set up, **go and play**. If you’re brand new to Sass we’ve set up some resources to help you learn pretty darn quick.

This will download the `SASS` package from npm's repository and install it globally on your system. Once you insall that second time no need to install for another project.

```bash
npm install -g sass
```

If you want to install dev dependencies, run the command:

```bash
npm install --save-dev sass
```

To check the version, run the command:

```bash
sass --version
```