# Victor Hugo - Now with 100% more Sass!

**Built on a Hugo boilerplate for creating truly epic websites**

This is a boilerplate for using [Hugo](https://gohugo.io/) as a static site generator and [Gulp](https://gulpjs.com/) + [Webpack](https://webpack.js.org/) as your asset pipeline.

Victor Hugo is setup to use [PostCSS](http://postcss.org/) and [Babel](https://babeljs.io/) for CSS and JavaScript compiling/transpiling. This version of the boilerplate adds Sass support through [node-sass](https://www.npmjs.com/package/node-sass). Special thanks to [Kuhrt](https://github.com/Kuhrt) for his `hugo-template` repo.

### Installation

To use this boilerplate, you'll need to have the latest [Node](https://nodejs.org/en/download/) installed.

First clone the repo:
`git clone https://github.com/TheCing/hugo-template.git`
(or use SSH)

After CDing to the project directory, install npm packages and dependencies:

```bash
npm install
```
Wait for this to complete before moving on.

## Site Structure

```
|--site                // Everything in here will be built with hugo
|  |--content          // Pages and collections
|  |--data             // YAML/TOML data files
|  |--layouts          // This is where all templates go
|  |  |--partials      // This is where includes live
|  |  |--index.html    // The index page
|  |--static           // Files in here ends up in the public folder
|--src                 // Files that will pass through the asset pipeline
|  |--css              // We won't be using the CSS folder here as we are using Sass
|  |--fonts            // Fonts placed here can be referenced in Sass and JS files
|  |--js               // app.js will be compiled to /app.js with babel
|  |--scss             // All styling goes here. main.scss will be compiled to main.css at compilation
```

### Running

To run your local development server:

```bash
npm start
```

Visit http://localhost:3000/ to preview your new website. [BrowserSync](https://browsersync.io/) will automatically refresh the browser window when changes are made to your site. Access the BrowserSync UI at http://localhost:3001/.

### Deploying

#### Deploying to FTP or rsync
To build a static version of the website inside the `/dist` folder, run:

```bash
npm run build
```

#### Deploying to Netlify
Victor-Hugo was built to integrate cleanly with Netlify. To deploy to Netlify:
- Push your clone to your own GitHub repository.
- [Create a new site on Netlify](https://app.netlify.com/start) and link the repository.

Netlify will now build and deploy your site whenever you push your repo.

## Basic Concepts

You can read more about Hugo's template language in their documentation here:

https://gohugo.io/templates/overview/

The most useful page there is the one about the available functions:

https://gohugo.io/templates/functions/

For assets that are completely static and don't need to go through the asset pipeline,
use the `site/static` folder. Images, font-files, etc, all go there.

Files in the static folder ends up in the web root. So a file called `site/static/favicon.ico`
will end up being available as `/favicon.ico` and so on...

The `src/js/app.js` file is the entrypoint for webpack and will be built to `/dist/app.js`.

You can use **ES6** and use both relative imports or import libraries from npm.

Any CSS file directly under the `src/css/` folder will get compiled with [PostCSS Next](http://cssnext.io/)
to `/dist/css/{filename}.css`. Import statements will be resolved as part of the build

## Environment variables

To separate the development and production *- aka build -* stages, all gulp tasks run with a node environment variable named either `development` or `production`.

You can access the environment variable inside the theme files with `getenv "NODE_ENV"`. See the following example for a conditional statement:

    {{ if eq (getenv "NODE_ENV") "development" }}You're in development!{{ end }}

All tasks starting with *build* set the environment variable to `production` - the other will set it to `development`.
