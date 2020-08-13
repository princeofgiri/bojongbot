# bojongbot
A simple script send alerts using Telegram bot.

This modify from https://github.com/matriphe/monit2telegram/ and custom it for personal needs. So only made for **ping** and **url/http/https** checking.


## Requirements

* Bash
* CURL
* [jq](https://stedolan.github.io/jq/)
* Telegram Bot

## Create Telegram Bot

If you don't have a Telegram Bot, just [create one](https://core.telegram.org/bots#create-a-new-bot). By using a Telegram bot you don’t have to use a real Telegram client or reuse your Telegram account. 

### Getting Bot Token

You will get a **Telegram Bot Token** after bot created. Keep this token, we will use it later. The bot token is looked like this.

```nginx
123456789:aBcDeFgHiJkLmN-OpQrStUvWXyZ12345678
```

### Getting Chat ID

To send messages to a Telegram chat, you must first needs to start a chat with the bot. Clicking on the bot link after creation should be enough, it will automatically send a message of `/start` to the bot.

To get the **Chat ID** from Telegram bot, execute this command using [getUpdates](https://core.telegram.org/bots/api#getupdates) function of Telegram API.

```console
$ curl --silent "https://api.telegram.org/bot{TOKEN}/getUpdates" | jq
{
  "ok": true,
  "result": [
    {
      "update_id": 17082016,
      "message": {
        "message_id": 17,
        "from": {
          "id": 22031984,
          "first_name": "User"
        },
        "chat": {
          "id": 22031984,
          "first_name": "User",
          "type": "private"
        },
        "date": 1471402800,
        "text": "Hello from the other side~"
      }
    }
  ]
}
```

In this example the **Chat ID** to look out for is **22031984**. Replace `{TOKEN}` with your Telegram bot token.

## Usage

Clone this repo or download the zipped file. 

```console
$ git clone https://github.com/princeofgiri/bojongbot.git 
$ mv bojongbot /opt/
```

Put your Telegram Bot ID and Chat ID in `/opt/bojongbot/telegramrc` and save it.

Test the `sendtelegram` script by running this command.

```console
$ /opt/bojongbot/sendtelegram -c /opt/bojongbot/telegramrc -m "Hello from the other side!"
Sending message 'Hello from the other side!' to 22031984
Done!
#
```
You should see Telegram message sent by your Telegram bot.

## Using ping script

Edit `iplist` in `/opt/bojongbot/iplist` and save it (there's example already in this file).
To execute this command to test:

```console
$ /opt/bojongbot/ping
```

## Cron

If you need to execute ping script every 5 seconds, you need to put it to crontab. Here the step:

```console
$ crontab -e
```

Add this `*/5 * * * * /opt/bojongbot/ping` then save.

## More feature

Yes, I need several idea or pull request about other implementation. Feel free to create pull request!