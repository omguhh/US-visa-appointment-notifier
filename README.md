# US-visa-appointment-telegram-notifier

This is a fork from this repo, [US-visa-appointment-notifier](https://github.com/theoomoregbee/US-visa-appointment-notifier) by [@theoomoregbee](https://github.com/theoomoregbee/).

I've updated the script to send it to a chat bot I set up on Telegram. It only notifies when there's an earlier date before the date I set - there is no rescheduling functionality. **Note: You do get rate limited if you make > 60 requests in ~ 5 hours, so be careful** :)

You can run the script locally, this is what you'll see in the console.

```
$ npm start
=====>>> Step: starting process with 250 tries left
=====>>> Step: logging in
=====>>> Step: checking for schedules
[{"date":"2023-02-08","business_day":true},{"date":"2023-04-26","business_day":true},{"date":"2023-10-11","business_day":true}]
=====>>> Step: starting process with 249 tries left
=====>>> Step: checking for schedules
[{"date":"2023-04-26","business_day":true},{"date":"2023-10-11","business_day":true}]
=====>>> Step: starting process with 248 tries left
=====>>> Step: checking for schedules
[{"date":"2023-10-11","business_day":true}]
=====>>> Step: sending an email to schedule for 2023-10-11
...
```

![telegram notification sample](./chat_screenshot.png)


## How it works

* Logs you into the portal
* checks for schedules by day 
* If there's a date before your initial appointment, it notifies you via email
* If no dates found, the process waits for set amount of seconds to cool down before restarting and will stop when it reaches the set max retries.

> see `config.js` or `.env.example` for values you can configure

## Configuration

copy the example configuration file exampe in `.env.example`, rename the copied version to `.env` and replace the values.

### Telegram config values 

You can create a chat bot with [@BotFather](https://t.me/botfather) - there's many tutorials online for this, you can use [this](https://core.telegram.org/bots/features#creating-a-new-bot) one. Keep note of the `token` that gets generated for you here. Once you've created the bot, create a group chat with just you and the bot on Telegram, I called my group `US-VISA-NOTIFIER`. 

The `TELEGRAM_CHAT_URL` can now be set in the enviroment variables. You can follow this structure:
`https://api.telegram.org/bot${your_token}`

The `TELEGRAM_CHAT` ID can be found by accessing the group chat on `web.telegram.com` - just log in to your account, open the group chat and copy the ID in your URL. `https://web.telegram.org/k/#{chat_id}`. You might need to add `-100` to the beginning of the ID if get an error, so the format could look like this `-10014xxxxxx`.

The `TELEGRAM_ADMIN` variable is just your telegram username, without the @. `yourusername`.

You should be set to send messages from this script now. :)

## FAQ

* How do I get my facility ID - https://github.com/theoomoregbee/US-visa-appointment-notifier/issues/3
* How do I get my schedule ID - https://github.com/theoomoregbee/US-visa-appointment-notifier/issues/8, https://github.com/theoomoregbee/US-visa-appointment-notifier/issues/7#issuecomment-1372565292
* How to setup Telegram bot - https://github.com/theoomoregbee/US-visa-appointment-notifier/issues/5

## How to use it

* clone the repo
* run `npm i` within the cloned repo directory
* start the process with `npm start`


