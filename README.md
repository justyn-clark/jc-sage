# JC Sage

JC Sage is a WordPress starter theme with a modern development workflow.

## Features

* Sass for stylesheets
* ES6 for JavaScript
* [Webpack](https://webpack.github.io/) for compiling assets, optimizing images, and concatenating and minifying files
* [BrowserSync](http://www.browsersync.io/) for synchronized browser testing
* [Bootstrap 4](http://getbootstrap.com/) for a front-end framework (can be removed or replaced)
* Template inheritance with the [theme wrapper](https://roots.io/sage/docs/theme-wrapper/)

## Requirements

Make sure all dependencies have been installed before moving on:

* [PHP](http://php.net/manual/en/install.php) >= 5.5.x
* [Composer](https://getcomposer.org/download/)
* [Node.js](http://nodejs.org/) >= 4.5

## Theme installation

Install Sage using Composer from your WordPress themes directory (replace `your-theme-name` below with the name of your theme):

```shell
# @ example.com/site/web/app/themes/
$ composer create-project roots/sage your-theme-name dev-master
```

## Theme structure

```shell
themes/your-theme-name/   # → Root of your Sage based theme
├── assets                # → Front-end assets
│   ├── config.json       # → Settings for compiled assets
│   ├── build/            # → Webpack and ESLint config
│   ├── fonts/            # → Theme fonts
│   ├── images/           # → Theme images
│   ├── scripts/          # → Theme JS
│   └── styles/           # → Theme stylesheets
├── composer.json         # → Autoloading for `src/` files
├── composer.lock         # → Composer lock file (never edit)
├── dist/                 # → Built theme assets (never edit)
├── functions.php         # → Composer autoloader, theme includes
├── index.php             # → Never manually edit
├── node_modules/         # → Node.js packages (never edit)
├── package.json          # → Node.js dependencies and scripts
├── screenshot.png        # → Theme screenshot for WP admin
├── src/                  # → Theme PHP
│   ├── lib/Sage/         # → Theme wrapper, asset manifest
│   ├── admin.php         # → Theme customizer setup
│   ├── filters.php       # → Theme filters
│   ├── helpers.php       # → Helper functions
│   └── setup.php         # → Theme setup
├── style.css             # → Theme meta information
├── templates/            # → Theme templates
│   ├── layouts/          # → Base templates
│   └── partials/         # → Partial templates
└── vendor/               # → Composer packages (never edit)
```

## Theme setup

Edit `src/setup.php` to enable or disable theme features, setup navigation menus, post thumbnail sizes, post formats, and sidebars.

## Theme development

JC Sage uses [Webpack](https://webpack.github.io/) as a build tool and [npm](https://www.npmjs.com/) to manage front-end packages.

### Install dependencies

From the command line on your host machine (not on your Vagrant development box), navigate to the theme directory then run `npm install`:

```shell
# @ example.com/site/web/app/themes/your-theme-name
$ npm install
```

You now have all the necessary dependencies to run the build process.

### Build commands

* `npm start` — Compile assets when file changes are made, start BrowserSync session
* `npm run build` — Compile and optimize the files in your assets directory
* `npm run build:production` — Compile assets for production

#### Additional commands

* `npm run clean` — Remove your `dist/` folder
* `npm run lint` — Run eslint against your assets and build scripts
* `composer test` — Check your PHP for code smells with `phpmd` and PSR-2 compliance with `phpcs`

### Using BrowserSync

To use BrowserSync during `npm start` you need to update `devUrl` at the bottom of `assets/config.json` to reflect your local development hostname.

If your local development URL is `https://project-name.dev`, update the file to read:
```json
...
  "devUrl": "https://project-name.dev",
...
```

If you are not using [Bedrock](https://roots.io/bedrock/), update `publicPath` to reflect your folder structure:

```json
...
  "publicPath": "/wp-content/themes/sage/"
...
```

By default, BrowserSync will use webpack's [HMR](https://webpack.github.io/docs/hot-module-replacement.html), which won't trigger a page reload in your browser.

If you would like to force BrowserSync to reload the page whenever certain file types are edited, then add them to `watch` in `assets/config.json`.

```json
...
  "watch": [
    "assets/scripts/**/*.js",
    "templates/**/*.php",
    "src/**/*.php"
  ],
...
```

