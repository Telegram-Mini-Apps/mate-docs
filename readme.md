# Telegram Mini Apps Mate

Your companion for managing Telegram Mini Apps.

This project simplifies the manipulation of your mini app distribution files.

## Getting Started

To start using the project, you need to obtain your deploy token, which is unique to each project.
To get your token, go to [@tma_mate_bot](https://t.me/tma_mate_bot) and press the `Start` button.

<p align="center">
  <img src="./img/start.png" width="320"/>
</p>

Next, press the `Create a Project` button and enter the name of your project, following the
specified rules.

<p align="center">
  <img src="./img/create.png" width="320"/>
</p>

After this step, the bot will provide you with a `Deploy Token`, which you will use later to deploy
the project.

### Installing @telegram-apps/mate

To deploy your project, you need to install
the [@telegram-apps/mate](https://www.npmjs.com/package/@telegram-apps/mate) CLI package.

```bash
# Using pnpm
pnpm i -D @telegram-apps/mate
# or npm
npm i -D @telegram-apps/mate
# or yarn
yarn add -D @telegram-apps/mate
```

Alternatively, you can install it globally:

```bash
# Using pnpm
pnpm i -g @telegram-apps/mate
# or npm
npm i -g @telegram-apps/mate
# or yarn
yarn global add @telegram-apps/mate
```

Once installed, the package will be accessible via the `mate` CLI tool:

```bash
mate --help
```

## Getting Project Deployment Info

Before deploying the project, you might want to know the base URL. The base URL is the absolute URL
that the project bundler will use to create links to all project assets.

To retrieve the project deployment information, including the base URL, use the following command:

```bash
# TOKEN refers to the deploy token received from the bot.
# PROJECT is a project identifier. Example: 48
mate deploy info --token {TOKEN} --project {PROJECT}
```

You will see an output similar to this:

```
✔ Fetched deploy information for paper-planes (id 48) project
Project Title: paper-planes
Short title of the project
--------
Base Path (using tag "test"): https://35f105bd6b.tapps.global/latest
This path will be used as a base path for the uploaded assets associated with this project. 
Consider using this value as a base path in your bundler. You can also use different tags using 
the --tag option
--------
Allowed file extensions: html, css, js, cjs, mjs, png, jpg, jpeg, webp, ttf, woff, woff2, eot, 
json, ico
Files extensions which are allowed to be uploaded
--------
Maximum size: 10485760 bytes
Maximum upload size
--------
Maximum files count: 100
Maximum files count a single upload can contain
```

The value `https://35f105bd6b.tapps.global/latest` is the base URL that you should
use in your bundler.

## Deploying

Before deploying the project assets, ensure that you have built your project and are not deploying
source files. You should only deploy files that can be successfully opened by the user's browser.

Let’s assume you have a project with id `48`. Also, you have a `dist` directory with all
the built files. To deploy this directory to the CDN, use the following command:

```bash
# TOKEN refers to the deploy token received from the bot.
mate deploy upload --dir dist --token {SPECIFY TOKEN HERE} --project 48
```

As a result, you will see a message like this in your console:

```
✔ Fetched deploy information for paper-planes (id 48) project
i Assets base path (using tag "latest"): https://35f105bd6b.tapps.global/latest
i Allowed file extensions: html, css, js, cjs, mjs, png, jpg, jpeg, webp, ttf, woff, woff2, eot, 
json, ico
i Maximum upload size: 10485760 bytes
i Maximum files count: 100
✔ Directory compressed successfully from 24185 to 7168 bytes
✔ Archive uploaded successfully
📁 dist
╰ 📄 index.js (https://35f105bd6b.tapps.global/latest/index.js)
```

> **Important**
>
> Note that your directory must include only usual files and directories.
> All other types of files (symlinks, for example) are forbidden, the CLI toll will let you know
> about it.

## Tagging

Mate allows you to use multiple tags in your project. A tag is simply a marker for your deployment
version.

Each tag corresponds to its own subdirectory, which is reflected in the final asset URL.

By default, Mate uses the `latest` tag. To override this, use the `--tag` option:

```bash
mate deploy upload --dir dist --token {TOKEN} --project {PROJECT} --tag test
```

## Using Config

To enhance your experience, you can create a `mate.yml` file in your project root directory and
include the following content:

```yml
deploy:
  projectId: {PROJECT}
  directory: dist
  token: {TOKEN}
```

Then, you can use the `mate` commands:

```bash
mate deploy info
mate deploy upload
```
