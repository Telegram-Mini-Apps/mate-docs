# Telegram Mini Apps Mate

Your Telegram Mini Apps mate.

This project helps you to manipulate your mini apps distributive files in a simple manner.

## Getting Started

To start using the project, it is required to get your deploy token, each project has its own. To do
so, go to [@tma_mate_bot](https://t.me/tma_mate_bot) and press the `Start` button.

<p align="center">
  <img src="./img/start.png" width="320"/>
</p>

Then, press the `Create a Project` button and enter the name or your project, following the defined
rules.

<p align="center">
  <img src="./img/create.png" width="320"/>
</p>

After this step, the bot will return a `Deploy Token`, which we will further use to deploy the
project.

## Deploying

To deploy the project, you have to install
the [@telegram-apps/mate](https://www.npmjs.com/package/@telegram-apps/mate) CLI package.

```bash
# pnpm
pnpm i -D @telegram-apps/mate
# or npm
npm i -D @telegram-apps/mate
# or yarn
yarn add -D @telegram-apps/mate
```

After installing the package, it will be accessible via the `mate` CLI applet:

```bash
mate --help
```

> Before deploying the project assets, make sure you've built your project, and you are not
> deploying the source files. You must deploy only files, which could be successfully opened by the
> user's browser.

Let's imagine that we have a project `paper-planes` and it contains the `dist` directory,
containing all project's built files. To deploy this directory to CDN, we have to use the
following command:

```bash
# TOKEN here is the deploy token we received from the bot.
mate deploy upload --dir dist --token {TOKEN} --project paper-planes
```

[//]: # (To make your development experience better, you may install)