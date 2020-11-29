# Travis the Chimp

[![Build Status](https://github.com/blazingbulldogs/travis-the-chimp/workflows/CI/badge.svg)](https://github.com/blazingbulldogs/travis-the-chimp/actions)
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/xojs/xo)

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/blazingbulldogs/travis-the-chimp)

A Discord bot that uses the [Perspective API](https://www.perspectiveapi.com/#/home) to automatically moderate users without a role.

## About

### How it works

Unlike most Discord bots, this one has no commands.
As long as it's running it will be automatically scanning messages.

Each time a message is sent the bot will check if the author has 0 roles.
If they have roles message checking is cancelled. Otherwise, the message is sent to the [Perspective API](https://www.perspectiveapi.com/#/home) and graded for toxicity.

#### Thresholds

The [thresholds configured](https://github.com/blazingbulldogs/travis-the-chimp/blob/d5bdfe787db00059c8bbc5ee44855ff716498b32/src/config.ts#L13) set the minimum confidence required to take a moderation action.
The action with the highest threshold will be taken if possible.
Configured thresholds represent the confidence that [Perspective API](https://www.perspectiveapi.com/#/home) had.
So, a threshold of `0.5` would mean that [Perspective API](https://www.perspectiveapi.com/#/home) was 50% confident that a message was toxic.

Changing thresholds is relatively simple, just fork the repository and edit [the file where they are configured](https://github.com/blazingbulldogs/travis-the-chimp/blob/master/src/config.ts#L13).
However, checking for another attribute type (ex. `SEVERE_TOXICITY`) would require more complex changes to [the file where API operations are performed](https://github.com/blazingbulldogs/travis-the-chimp/blob/d5bdfe787db00059c8bbc5ee44855ff716498b32/src/events/message.ts#L24-L27).

If you want help changing the attribute types used to monitor messages for your bot, or want it to be easily configurable, please open an issue on GitHub and a maintainer will help you.

### Inviting the bot

After creating a bot account you'll want to invite it to your server.

Go to the [Discord Developer Portal](https://discord.com/developers/applications/) and copy the client ID from your application.
Visit this URL, but replace the template with your ID:

```
https://discord.com/oauth2/authorize?client_id=[YOUR_CLIENT_ID_GOES_HERE]&permissions=11270&scope=bot
```

For our bot with an ID of `758523212362416128` our URL is:

```
https://discord.com/oauth2/authorize?client_id=758523212362416128&permissions=11270&scope=bot
```

After inviting it to your server you may want to restart the bot.

### Log channel

Log messages will be automatically posted to the first text channel named `travis-logs`.
Make sure you have granted the bot account access this channel and inform server moderators not to rename it.

If the channel can't be found nothing will be posted, but you can check the audit logs for relevant info.

## Contributing

### Prequisites

This project uses [Node.js](https://nodejs.org) 14 to run.

This project uses [Yarn](https://yarnpkg.com) to install dependencies, although you can use another package manager like [npm](https://www.npmjs.com) or [pnpm](https://pnpm.js.org).

```sh
yarn install
# or `npm install`
# or `pnpm install`
```

### Building

Run the `build` script to compile the TypeScript into the `tsc_output` folder.

### Style

This project uses [Prettier](https://prettier.io) and [XO](https://github.com/xojs/xo).

You can run Prettier in the project with this command:

```sh
yarn run style
```

You can run XO with this command:

```sh
yarn run lint
```

Note that XO will also error if you have TypeScript errors, not just if your formatting is incorrect.

### Linting

This project uses [XO](https://github.com/xojs/xo) (which uses [ESLint](https://eslint.org) and some plugins internally) to perform static analysis on the TypeScript.
It reports things like unused variables or not following code conventions.

```sh
yarn run lint
```

Note that XO will also error if you have incorrect formatting, not just if your TypeScript code has errors.
