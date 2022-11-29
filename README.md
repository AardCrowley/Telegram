# Telegram

Note: You will need a later version than r1825 of MUSHclient, so if you haven't updated in a while, you should.

# What is Telegram?

Telegram is an application that can be a chat platform as well as a way to receive notifications, not limited to Aardwolf. I have taken the time to write the code so that one may easily receive notifications of certain events in Aardwolf.

# Initial Setup

First things first, you need to install Telegram. Though the most common use would be for a phone, you can install it as a desktop application or even just use the Web platform. Get it here: http://telegram.org. Once downloaded, sign up for an account.

# Getting a Bot API token

Your next order of business will be to get your own Bot API token. To do this, you'll need to talk to the Botfather, which you can add to your application here: https://telegram.me/botfather

Once he's been added, you'll simply type `/newbot` in order to create your first bot. You'll receive an API token for it, so you'll want to copy that token and save it somewhere as you'll be using it shortly.

To add your bot's channel to Telegram, you'll need to click the link from Botfather's message congratulating you on creating your bot. It'll be `t.me/<yourbotname>`. Then click `Start` and send a message in preparation for the next step.

# Getting your Chat ID

The next step will be to get your chat ID. The easiest way I've found to do this is using the test message in your new Bot channel. Go to the following page: `https://api.telegram.org/bot<token>/getUpdates` (where `<token>` is the token you got in the last step). Upon heading to the site, you'll see a JSON-formatted list of information. Look specifically for the table `chat`, which has an `id` field. Copy that ID (including any negative symbols). If you only see mostly empty JSON without any chat id like this -
```json
{"ok":true,"result":[]}
```
Send a message to the bot using the following format, to get updated JSON.
```
/start your_msg_whatever
```

# Putting it all together

Now, open the plugin and make the following changes. Where it says:

```lua
chatID = <your chat ID>
```

replace `<your chat ID>` with the ID you picked up from the previous step. Where it says:

```lua
apiToken = "<your bot token>"
```

replace `<token>` where again it is what you received from creating your bot.

From here on out, it should work out of the gate.

If you're wanting to add new triggers, locate the `triggerLines` section, and add your trigger as such:

```lua

{name = "<name of your trigger>", match = "<the trigger pattern to match>", message = "<text you want sent>"},

```

An example pulled directly from the plugin is this, for quest alerts:

```lua
{name = "questAlert", match = "^QUEST: You may now quest again.", message = "Quest time!"},
```

Please note, you can use wildcard symbols (use regular expression for the matches), but it will not process within the message. Otherwise, as long as you follow this format, you should be able to add as many triggers as you like.

If you are wanting to add channel messages to Telegram such as tell notifications, you'll need to incorporate GMCP data into the plugin. It will look something like the following:

```lua
require 'gmcphelper'
dofile (GetInfo(60) .. "aardwolf_colors.lua")

function OnPluginBroadcast(msg, id, name, text)
    if (id == '3e7dedbe37e44942dd46d264') and (text =='comm.channel') then
        if gmcp('comm.channel.chan') == "tell" then
            cmsg, player = strip_colours(gmcp('comm.channel.msg')), gmcp('comm.channel.player')

            if player ~= gmcp("char.base.name") then
                pageRequest(cmsg)
            end
        end
    end
end
```

# New feature: Setting your own triggers client-side

Now you can set your own triggers client-side as of 11/29/2022 (or 29/11/2022 for you non-Americans!). Simply create the trigger you want an alert for and use the following syntax to utilize it:

```CallPlugin("f99bb4b89cfa8c90ac2d03d5", "pageRequest", "Whatever your want your message to be.")```

Please be aware that if you utilize this feature so you can bot and pass bot checks, you are a bad person and you will be caught eventually. This feature is only to be used so you do not miss any tells for legitimate reasons. Besides, the Imms have other ways to botcheck you, too.

If you have any questions or difficulties, please feel free to drop me (Crowley) a tell or a note on personal board.
