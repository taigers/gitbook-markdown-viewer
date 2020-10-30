# Gitbook Markdown Viewer
This Vue.js webapp is a simple reader for Markdown files generated using [Gitbook](https://www.gitbook.com).

To use this viewer you will need a Github Repository  which contains:
- Markdown files as generated by Gitbook via the inbuilt Github integration
- A `package.json` file at the repository root folder. This will allow us to use `npm` or `yarn` to pull down the Markdown document content and set it as a frontend dependency.

For demonstration, this project has already installed the [converse-docs](https://github.com/taigers/converse-docs) package dependency, which contains the Product Documentation for TAIGER Converse.

## How it works

### Compile operations
- When the project is compiled with `yarn run serve` or `yarn run build`, the markdown files are compiled into HTML markup and copied into the project public folder (see `vue.config.js` for details). Images in the Gitbook assets folder are also copied.
- The HTML files and assets are placed in a `TARGET_DOC_FOLDER`, specified in `docs-config.js`.

### Runtime operations
- When the application is loaded, vue-router will take the Markdown **folder path** and **file name** from the URL in the browser window.
- The 2 values are passed to the `MarkdownViewer` component, which will load the corresponding HTML text content via HTTP, and render the it on the UI.
- For example:
  - `<base-url>/README.md` will load the `README.html` found at root folder `/` of the `TARGET_DOC_FOLDER`
  - `<base-url>/essentials/quickstart/introduction.md` will load the `introduction.html` found at `/essentials/quickstart` in the `TARGET_DOC_FOLDER`
- The `MarkdownViewer` component also:
  - Parses the loaded HTML file and looks for header anchor links to display on the right sidebar.
  - Retrieves content for the left sidebar with the links to other pages of the Gitbook, found at `SUMMARY.md`. This file is automatically generated by Gitbook when exporting to Github.


## Project setup

```
yarn install
```

### Add the Documentation Node Package as a dependency
```
yarn add ssh://git@github.com:taigers/<your-docs-repo-name>.git#<version>
```

### Set the Node Package Name in the configuration
```javascript
// docs-config.js
module.exports = {
  ..
  NODE_PACKAGE_NAME: '<your-package-name>'
  ..
}
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Run your tests
```
yarn run test
```

### Lints and fixes files
```
yarn run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
