[![Netlify Status](https://api.netlify.com/api/v1/badges/86a86566-a833-4d2a-a4cf-867ad6c9f68a/deploy-status)](https://app.netlify.com/sites/eq-runner-prototypes/deploys)

# eQ runner prototype kit

This repo was created from the ONS Design System prototype kit template [prototype-kit](https://github.com/ONSdigital/prototype-kit).

## Getting setup

To install the dependencies run:

```bash
yarn
```

To install the latest version of the ONS design system run:

```bash
yarn add @ons/design-system
```

## How to use this project?

This project comes with the following commands:

- `yarn start` - Builds prototype content and starts a local server for previewing content changes. The command displays the URL for accessing the local server.

- `yarn watch` - Starts a local server for previewing content changes. The command displays the URL for accessing the local server. Unlike `yarn start`, this command does not perform an initial build.

- `yarn build` - Builds prototype content as a static website to a 'build' directory inside this project. The output of this command could be used by a CI process to deploy the prototype website.

## How do the build commands work?

This project uses [gulp](https://gulpjs.com/) to automate the above commands. The [prototype kit]({{PROTOTYPE_KIT_HOMEPAGE}}) provides default gulp tasks which are used by this repository which are inherited in the `./gulpfile.js` script.

Additional gulp tasks can be added to this project's `gulpfile.js` in the usual way. Refer to the gulp documentation for information on how to do this.

## Getting started

1. Create a directory alongside the 'example' prototype directory and then populate with files using 'example' as a starting point.

2. Create prototype by editing the prototype entry points (`index.njk`, `index.js` and `index.scss`).

3. Preview the prototype by running `yarn start`.

## Using a specific version of the design system

Begin by adding a reference to the specific design system version in the `package.json` file of this repository; for example, if version 44.0.0 were required then this would look like this:

```json
"dependencies": {
  "@ons/design-system/44.0.0": "npm:@ons/design-system@44.0.0",
  ...
}
```

And then add the `version` attribute at the top of each Nunjucks template that requires this specific design system version:

```nunjucks
---
version: 44.0.0
---
<p>This page uses design system version 44.0.0.</p>
```

### Custom JavaScript

If you need to add custom JavaScript to your prototype, the build system will automatically look for a file called `index.js` in your prototype. Gulp will convert your JavaScript to ES5 code. You can refer to the example folder to see how to include the JavaScript in your template.

### JavaScript helpers
If the `index.js` file is included in your prototype it also automatically imports some ready made helpers for you:
- Questions Manager - this adds all questions and answers entered on pages into the session storage in the browser so that they can be accessed at any time for things such as piping and summaries
- Piping - this uses the data collected by the questions manager and pipes the answer into another page, e.g. into the wording of another question. To use it add the `.js-piped-answer` class to the element you want to pipe the answer into along with a `{x}` where in that element you want to pipe it. Then add the `data-question-to-pipe` attribute too and set it to the url of the page you want to pipe the answer from.
- Previous Link - if you add the class `.js-previous` to a link and a `previous` variable in the url variables is set. Then the link url will be set to what the `previous` variable is set to. But this can be overridden by setting `prevPage` in the nunjucks to the name of the page you want the link to go to and the url will be populated from that.

### Custom CSS

If you need to add custom CSS to style a new component or override styling on an existing component you can create a `.scss` file in the directory of your prototype. Gulp will spit out a `.css` file named the same as any `.scss` file that isn't prefixed with an underscore. You can refer to the example folder to see how to include generated css in your template.
