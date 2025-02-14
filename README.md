# ✍️ 💻 👋

Source code for my blog.

- [In English](https://bespoyasov.me)
- [In Russian](https://bespoyasov.ru)

## Overview

[Next](https://nextjs.org) is used as a static site generator. Pages call the `network` service that triggers `persistence` to read a post or a project from an MDX file in the `storage` directory.

Translation dictionary collection, RSS generation and image optimization are performed by custom scripts located in `ops`. For optimizing images, [Squoosh](https://squoosh.app) is used.

[Jest](https://jestjs.io) is used as a test runner and [Hygen](https://www.hygen.io) as a code generator.

Deployed on static servers using [GitHub Actions](https://github.com/features/actions).

## Installation

Clone the repo and install dependencies:

```sh
git clone https://github.com/bespoyasov/www.git
cd www

npm install
```

## Development

For starting the development mode, run:

```sh
npm start
```

This command will start 3 daemons in parallel:

- Next dev server for En version on [2001 port](http://localhost:2001);
- Next dev server for Ru version on [2002 port](http://localhost:2002);
- Translation dictionary watcher for live-updates of localization data.

### Code Generation

To create a component, post, or a page, run:

```sh
npm run new:component
npm run new:post
npm run new:page

# After hitting any of these commands,
# an interactive CLI will guide you.
```

### Testing

To run the tests while developing:

```sh
npm run test:dev
```

To run all tests once:

```sh
npm test
```

The latter command is also used in CI.

## Project Build

The project can be built in 2 different languages:

```sh
npm run build:en
npm run build:ru
```

After the build, Next exports the generated site sources into the `out` directory. Then the static resources are cleaned up to contain only the media related to the current build locale. In the end, RSS is generated.

As a result, you will find sources for a static website in the `out` directory that can be deployed.

## Devops

For operations that aren't included in Next by default, custom `ops` scripts are used.

### Image Optimization

To optimize images in `public/images` using Squoosh, run:

```sh
npm run images:convert
```

Next's `Image` component doesn't support optimizations when using SSG, hence this script.

Also, generated images are kept in the repository to avoid too long deployments. Since all images require optimizations, without this every update would last for tens of minutes.

### Translation

Instead of using a third-party library and a localization service, the custom translation “library” is used.

It collects data from `translations.json` files in the `src` directory and creates a translation dictionary. Except the resulting dictionary, the script also creates the type definitions for the dictionary. The typings improve the IDE support and autocompletion.

To collect translations, run:

```sh
npm run dict:collect
```

This command is also run automatically after installing the dependencies and before project start and build.

To set up a watcher over the translation data that updates the dictionary on every `translations.json` file change, run:

```sh
npm run dict:watch
```

This command is run automatically before start of the project.

## Plans and TODOs

Everything I consider implementing is located in the [projects section](https://github.com/bespoyasov/www/projects) on GitHub. If you have an idea of an improvement, please, let me know in the [project issues](https://github.com/bespoyasov/www/issues).

## License

The source code is distributed under the [GNU GPL v3.0](LICENSE) license. You can use, modify, and redistribute it as long as you keep the license and disclose the source.

The content of the site is distributed under the [CC BY-NC-SA 4.0](LICENSE-SA.md) license. You can use and modify it as long as you mention the source and author, keep the license, and don't use the content in a commercial product.
