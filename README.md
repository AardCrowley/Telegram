# Telegram

Note: You will need a later version than r1825 of MUSHclient, so if you haven't updated in a while, you should. 

# What is Telegram?

Telegram is an application that can be a chat platform as well as a way to receive notifications, not limited to Aardwolf. I have taken the time to write the code so that one may easily receive notifications of certain events in Aardwolf.

# Initial Setup

First things first, you need to install Telegram. Though the most common use would be for a phone, you can install it as a desktop application or even just use the Web platform. Get it here: http://telegram.org. Once downloaded, sign up for an account.

# Getting a Bot API token

Your next order of business will be to get your own Bot API token. To do this, you'll need to talk to the Botfather, which you can add to your application here: https://telegram.me/botfather

Once he's been added, you'll simply type /newbot in order to create your first bot. You'll receive an API token for it, so you'll want to copy that token and save it somewhere as you'll be using it shortly.

# Getting your Chat ID

The next step will be to get your chat ID. The easiest way I've found to do this is to send a test message in your new Bot channel, then go to the following page: https://api.telegram.org/bot<token>/getUpdates (where &lt;token&gt; is the token you got in the last step). Upon heading to the site, you'll see a JSON-formatted list of information. Look specifically for the table "chat", which has an "id" field. Copy that ID (including any negative symbols).

# Putting it all together

Now, open the plugin and make the following changes. Where it says:

chatID = &lt;your chat ID&gt;

replace &lt;your chat ID&gt; with the ID you picked up from the previous step. Where it says:

apiToken = "&lt;your bot token&gt;"

change it to say:

apiToken = "bot&lt;token&gt;"

where &lt;token&gt; again is what you received from creating your bot. It is imperative that "bot" precedes it. The plugin will not work without it.

From here on out, it should work out of the gate.

If you're wanting to add new triggers, locate the 'triggerLines' portion, and add your trigger as such:

{name = "&lt;name of your trigger&gt;", match = "&lt;the trigger pattern to match&gt;", message = "&lt;text you want sent&gt;"},

As long as you follow that format, you should be able to add as many triggers as you like. If you have any questions or difficulties, please feel free to drop me (Crowley) a tell or a note on personal board.
