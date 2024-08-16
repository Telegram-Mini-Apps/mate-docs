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

### Installing @telegram-apps/mate

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

## Getting Project Info

It is the most common, that before deploying the project you would like to know the base URL. The
base URL is absolute the URL, which will be used by the project bundler to create URLs to
all project assets.

To get the project base URL, use the following command:

```bash
# TOKEN here is the deploy token we received from the bot.
mate deploy info --token {SPECIFY TOKEN HERE} --project paper-planes
```

You will see the following output:

```
✔ Fetched deploy information for paper-planes
Base Path (using tag "latest"): https://cdn.webappsbot.com/tma-assets/1da9a53596/latest
This path will be used as a base path for the uploaded assets associated with this project.
Consider using this value as a base path in your bundler.
You can also use different tags using the --tag option.
```

Here, the value `https://cdn.webappsbot.com/tma-assets/1da9a53596/latest` is the base URL you must
use in your bundler.

## Deploying

Before deploying the project assets, make sure you've built your project, and you are not
deploying the source files. You must deploy only files, which could be successfully opened by the
user's browser.

Let's imagine that we have a project `paper-planes` and it contains the `dist` directory,
containing all project's built files. To deploy this directory to CDN, we have to use the
following command:

```bash
# TOKEN here is the deploy token we received from the bot.
mate deploy upload --dir dist --token {SPECIFY TOKEN HERE} --project paper-planes
```

As a result, you will see a similar message in your console:

```bash
i Uploading directory: D:\users\qbnk\paper-planes\dist (2 files)
i Project: paper-planes
i Tag: latest
📁 dist
├ 📄 index.html (https://cdn.webappsbot.com/tma-assets/1da9a53596/latest/index.html)
├ 📄 create.png (https://cdn.webappsbot.com/tma-assets/1da9a53596/latest/create.png)
╰ 📄 start.png (https://cdn.webappsbot.com/tma-assets/1da9a53596/latest/start.png)
```

## Tagging

Mate allows using multiple tags in your project. The tag is just a marker of your deployment 
version. 

Each tag has its own subdirectory, which is reflected in the final asset URL. 

By default, mate uses the `latest` tag. To override this value, use the `--tag` option:

```bash
mate deploy upload --dir dist --token {SPECIFY TOKEN HERE} --project paper-planes --tag test
```

Here is the output:

```bash
✔ Fetched deploy information for paper-planes
Base Path (using tag "test"): https://cdn.webappsbot.com/tma-assets/1da9a53596/test
This path will be used as a base path for the uploaded assets associated with this project.
Consider using this value as a base path in your bundler.
You can also use different tags using the --tag option.
```

## Using Config

To make your experience better, you may create a `mate.yml` file in your project root directory and
specify the following content:

```yml
deploy:
  project: paper-planes
  directory: dist
  token: { SPECIFY TOKEN HERE }
```

Then, use the `mate` commands:

```bash
mate deploy info
mate deploy upload
```