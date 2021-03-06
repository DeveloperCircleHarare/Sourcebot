# Sourcebot
An open source Facebook Messenger news bot for your Wordpress website
To help African news organisations deliver personalized news and engage more effectively via messaging platforms.

- [Develop](#develop)
- [Test](#test)
- [Build](#build)
- [Deploy](#deploy)
- [Run](#run)
- [Contribute](#contribute)
- [Notes](#notes)

## Sourcebot version 1.X

## <a name="develop"></a> Develop

### Requirements
- A [Facebook Page](https://web.facebook.com/pages/create)
- A [Facebook App](https://developers.facebook.com/apps/) with the Facebook Messenger product
- [PHP 7.1+](http://php.net/downloads.php)
- [Xdebug](https://xdebug.org/download.php)
- [Composer](https://getcomposer.org/)
- A local web-server e.g. [Apache](https://www.apache.org/dyn/closer.cgi)
- A publicly accessible URL e.g. [ngrok](https://ngrok.com/)
- A Wordpress instance with the [Wordpress REST API](https://wordpress.org/plugins/rest-api/)

### First time

- Run `composer install`
- Visit localhost to confirm you see `index.php`
- Run `cp .env.example .env`
- Edit `.env`
- Run `phpunit`
- Run `ngrok http 80` to get the publicly accessible URL
- Go to your [Facebook App](https://developers.facebook.com/apps/)
- Click `Webhooks`
- Select `Page` from the drop-down
- Click `Subscribe to this topic`
- Enter the publicly accessible URL of your app and `/webhook.php`
- Enter the `FACEBOOK_VERIFY_TOKEN`
- Click `Verify and Save`
- Visit [Facebook Messenger](https://messenger.com)
- Search for your Facebook Page and send it a message

## <a name="test"></a> Test

Tests are run with `phpunit`

## <a name="build"></a> Build

Sourcebot is configured to build on [CircleCI](https://circleci.com/).

You can run local CircleCI builds with `circleci build` using the [CircleCI CLI](https://circleci.com/docs/2.0/local-jobs/).

## <a name="deploy"></a> Deploy

You can deploy Sourcebot to your own web-server or quickly and for free to Heroku.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

The latest release of Sourcebot is now supported! Changes include:

  * Requires PostgresSQL database, available through add-ons:
    * [Heroku-Postgresql](https://elements.heroku.com/addons/heroku-postgresql) (deploy default)
  * It also requires an instance of Elasticsearch
	* [Bonsai-Elasticsearch](https://elements.heroku.com/addons/bonsai) (deploy default)
  * `HEROKU_URL` config var renamed to `PUBLIC_URL` to avoid using Heroku's namespace
  * `DATABASE_URL` config var will be set for you to access your database

### Things you should know

### Requirements

- A [Facebook Page](https://web.facebook.com/pages/create)
- A [Facebook App](https://developers.facebook.com/apps/) with the Facebook Messenger product
- [PHP 7.1+](http://php.net/downloads.php)
- [Composer](https://getcomposer.org/)
- A web-server e.g. [Apache](https://www.apache.org/dyn/closer.cgi)
  - SSL must be configured
- A Wordpress instance with the [Wordpress REST API](https://wordpress.org/plugins/rest-api/)

### Before Deploy

Before deploying you probably want to give your bot a nice home page as `web/index.php` currently displays this `README.md`.

### After Deploy

Once you have Sourcebot running on a publicly accessible URL you need to set and verify your Facebook App's Webhook.

## Local
- Go to your [Facebook App](https://developers.facebook.com/apps/)
- Click `Webhooks`
- Select `Page` from the drop-down
- Click `Subscribe to this topic`
- Enter the URL of your app and `/webhook.php`
- Enter the `FACEBOOK_VERIFY_TOKEN`
  - If you are using Heroku then it was autogenerated and you can get it from the `Reveal Config Vars` section of your Heroku app's `Settings`
- Click `Verify and Save`
- Visit [Facebook Messenger](https://messenger.com)
- Search for your Facebook Page and send it a message

## HEROKU_URL
- Go to your [Facebook App](https://developers.facebook.com/apps/)
- Click `Webhooks`
- Select `Page` from the drop-down
- Click `Subscribe to this topic`
- Enter the URL of your app and `https://YOURAPPNAME.herokuapp.com/`
- Visit [Facebook Messenger](https://messenger.com)
- Search for your Facebook Page and send it a message

## <a name="run"></a> Run

To check Sourcebot can connect to your Wordpress go to <code>/wordpress-api-status.php</code>

## <a name="contribute"></a> Contribute

Contributions are welcome and follows the straightforward Github pull request process:

- Fork
- Code
- Test
- Submit a pull request

## <a name="notes"></a> Notes

### Facebook Page and App

- Facebook Messenger requires SSL/HTTPS to communicate with Sourcebot.
- The [quickstart](https://developers.facebook.com/docs/messenger-platform/guides/quick-start) guide is useful for setting up your Facebook Page and Facebook App. You do not need to follow the Node.js instructions.
- Make sure you associate your Facebook App with your Facebook Page in `Settings -> Advanced -> App Page`.
- Your Facebook App has to be reviewed for the `pages_messaging` permission. Before it is approved only Administrators, Developers, and Testers on the Facebook App's Roles page can interact with the bot.
- You can only have one webhook endpoint setup per Facebook App so you probably want a `development` and a `production` Facebook App at least.
- You can only associate one Facebook App per Facebook Page so you probably want a `development` and a `production` Facebook Page at least.