# Federal Credit Union website

A small-business website for a (fictional) credit union, built as a static site with Hugo and styled with Tachyons and PostCSS. Visitors can read the home page, products, values, contact and blog pages. Site owners can edit the content in a browser through Netlify CMS.

The project started from the open source Netlify template "one-click-hugo-cms" (see Credits). The text and images in `site/content` are placeholder sample content from that template (a coffee business), so the site is a working starting point rather than a finished credit union site.

## What it does

* Generates a fast, fully static multi-page site: home, products, values, contact, blog posts and a 404 page.
* Small reusable layout partials (jumbotron, media blocks, tables, image grids, forms) in `site/layouts/partials`, fed by Hugo `dict` data.
* A content editor at `/admin` powered by Netlify CMS with live preview templates (React). Saving content commits to the Git repository through Netlify Identity and Git Gateway.
* CSS pipeline with Sass, PostCSS (preset-env, import, cssnano) and a custom Tachyons fork. Variables live in `src/css/imports/_variables.css`.

## Tech stack

* Hugo (static site generator; the repository bundles Hugo binaries in `bin/`, and `hugo-bin` installs Hugo through npm)
* Webpack 4, Babel, Sass, PostCSS
* Netlify CMS (React 16) for editing, Netlify for hosting
* Node.js (version in `.nvmrc`) and Yarn

## Run it locally

You need Node.js (see `.nvmrc`) and Yarn or npm.

```
yarn            # or: npm install
yarn start      # Hugo plus webpack dev server with live reload
```

Open the address printed by the dev server (the dev server defaults to http://localhost:3000, see `webpack.dev.js`).

## Build a static copy (for a live demo)

```
yarn build      # or: npm run build
```

This runs webpack first (it writes the hashed CSS and JS file names to `site/data/webpack.json`) and then Hugo. The finished static site is in `dist/`. No secrets or API keys are needed to build. Serve it with any static file host, for example:

```
cd dist && python3 -m http.server 8000
```

To include draft and future dated posts, use `yarn build:preview`.

The `/admin` content editor only works when the site is deployed on Netlify with Identity and Git Gateway enabled. The public pages work anywhere.

Note: the Hugo templates read `site/data/webpack.json`, so running Hugo alone (for example `bin/hugo.linux -d dist -s site`) produces HTML without the stylesheet and script links. Run the webpack step first.

## Deploy

`netlify.toml` already holds the Netlify build settings (`yarn build`, publish `dist`). You can use the Deploy to Netlify button from the upstream template to get your own copy.

## Project layout

* `site/content` pages and blog posts (Markdown)
* `site/layouts` Hugo templates and partials
* `site/static` images, icons and the CMS config (`admin/config.yml`)
* `src` CSS, fonts and JavaScript (including the CMS preview templates)
* `webpack.*.js` build configuration

## Status

Working template, with placeholder content. The dependencies are from 2019 to early 2020 (for example `node-sass` 4 and webpack 4), so a modern Node.js version may fail to install them. Use the Node version in `.nvmrc`. The contact and newsletter forms have no form handler configured, so they do not send anything yet.

## Credits

Based on [one-click-hugo-cms](https://github.com/netlify-templates/one-click-hugo-cms) by Netlify, which is built on [Victor Hugo](https://github.com/netlify/victor-hugo). Template designed and developed by [Darin Dimitroff](http://www.darindimitroff.com/) of [spacefarm.digital](https://www.spacefarm.digital). Released under the MIT license (see `LICENSE`).
