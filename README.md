# SpellingBee UI app

This is an app I built to help my son practice spelling, and help me learn [Svelte](https://svelte.dev).

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Svelte - Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Svelte - Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## What does the app do?
The [Svelte](https://svelte.dev) app is the UI to a spelling test.  The app leverages Lambda APIs to build a grid of MP3 and input text fields.
The user then plays an MP3 of each word, and then spells the word in the input field. When the user is complete, they will POST their response and UI will compute and output their score.

## Architecture
This project leverages multiple AWS services.  The Spelling UI (this repo) is deployed on a S3 bucket that is setup as a static website.  It communicates with an API gateway (backed by Lambda/DynamoDb) to get a list of words.
The MP3 files are pre-created (by an API Gateway, Lambda, and Polly) and stored on S3.