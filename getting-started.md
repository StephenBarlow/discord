# Getting started with the Discord API (Python)

You want to build cool bots 'n' stuff for Discord?
Sweet. Let's do this.

## Setup

Before you can do all the cool stuff, you need to do a little
boring stuff. It won't take long, honest.

### 1. Register your Discord application

Your totally sweet application will need totally sweet
 __credentials__ so it can identify itself to Discord. To get
 those credentials, you need to register it:

1. Go to [discordapp.com/developers/applications/me](https://discordapp.com/developers/applications/me) in another tab.

2. Sign in to your Discord account if you haven't already. Um,
you do _have_ a Discord account, right?

  ___Of course I do. I rule.___  Nice.

  ___Uhh...about that...___ What?! [Let's fix that pronto.](https://discordapp.com/register) Return to the link in step 1 after you're done registering.

3. Behold, you've arrived at the majestic My Applications page:

  [img]

  See the giant **New Application** button? Click it, _if you dare_.

4. The New Application form appears.

  ___Oh no, now there's a bunch of buttons and text fields!
  TIME TO PANIC.___ Stay cool! For now, the only thing you need to put in here is your __app name__ at the top, like so:

  [img]

  Then, click __Save Changes__ at the bottom of the form.

Just like that, your app has been REGISTERED! But don't leave this page just yet, because you still need to...

### 2. Obtain your app credentials

After you register your app, a couple new sections appear on
its details page:

[img]

First things first, copy down your app's __Client ID__. You'll need
it later in the tutorial. Next, you'll also need some __bot
 credentials__:

1. Click the __Create a Bot User__ button.

  ___Ahhh! A warning appeared! I'm scared.___ Don't worry!
  Click __Yes, do it!__ and everything will be fine.

2. Your app bot user details appear:

  [img]

  For this tutorial, the only info you'll need is your bot
  user's __Token__. This is hidden on the page by default,
  because it's private. Anybody who has this token can
  make your bot do stuff that you probably don't want it to.
  __Keep it secret. Keep it safe.__

### 3. Create a test Discord server

Before you unleash your brilliant new bot upon the world, you'll
want to make sure it works in a more...contained...environment.

So! Create a new Discord server
[the typical way](https://support.discordapp.com/hc/articles/204849977).
If you're building an app with other people, be sure to invite them.

### 4. Install the Discord client library for Python

Working with a web API like Discord's is a lot easier with an
SDK, don't you think so? We do. Here's how to install our Python
SDK from the command line:

    pip install disco-py

Boom. Done.

## Add your bot's first feature

You've got a registered app! You've got a server to test it in!
You've even got a shiny SDK! __Let's write some code.__

Create a `hype-bot.py` file and slam this code in there:

    from disco.bot import Plugin

    class HypePlugin(Plugin):

      @Plugin.command('hype')
      def get_hype(self, event):
        event.msg.reply('THE HYPE IS REAL')

Don't forget to save!

__So what does this code do?__
* The `@Plugin.command` annotation instructs your bot to
call a particular function when it receives a particular message.
In this case, if you send your bot the chat message `hype`, the
 `get_hype` function is called.

* The `get_hype` function instructs the bot to respond with the
message `THE HYPE IS REAL` in the channel where the `hype`
 message was received.


## Add your bot to your test server

### 1. Assemble your authorization URL
In order to add a bot to a server, an admin for the server needs
to __authorize__ the bot. Lucky for you, you're the admin of the
test server you just created!

Paste the following URL into a text file and replace `YOUR_CLIENT_ID`
with your app's Client ID:

     https://discordapp.com/oauth2/authorize?client_id=YOUR_CLIENT_ID&scope=bot&permissions=3072

___What the heck is this?___

This is your app's __OAuth authorization URL__. You direct the admin of
a server to this URL so they can authorize your bot for their server.

___Okay. Uh, why are you sending it the number 3072?___

When you request bot authorization from an admin, you specify a set of
__permissions__ that your bot needs. Each possible permission has a
 different numeric value, and you add up the permissions you want.
The number `3072` is the sum of the permission values for:

* Reading text chat messages
* Writing text chat messages

That's all we need, so that's all we're asking for! Don't worry, these
permissions are covered in much greater detail later on.


### 2. Visit your authorization URL
Paste your assembled authorization URL into your browser and hit the
big ol' Enter key. Lo and behold, it's your bot's __permissions form__:

[img]

This lets an admin verify which permissions a bot is requesting before
they decide whether to authorize it.

Select your server from the dropdown menu and click __Authorize__.

Now, check out your test server! Look who's hanging out with you:

[img]

Sweet. Now, try typing the following into the channel chat:

    @hype-bot hype

Surprise, nothing happens!

___What?! Why?___

Because your bot isn't _running_! __Bots are listed in the channels
they're authorized for, even if they aren't actually running.__

With that in mind, let's...

### 3. Actually run your bot
Paste the following command into a text file and replace
`YOUR_BOT_TOKEN` with your app's bot token:

    python -m disco.cli --token="YOUR_BOT_TOKEN" --run-bot --plugin hype-bot

Then, _run_ that command from the directory that contains `hype-bot.py`.

You'll see a couple of warnings, followed by the following lines:

    INFO:GatewayClient:Opening websocket connection to URL `wss://gateway.discord.gg?v=6&encoding=json`
    INFO:GatewayClient:WS Opened: sending identify payload
    INFO:GatewayClient:Recieved HELLO, starting heartbeater...
    INFO:GatewayClient:Recieved READY

Holy heck, your bot is running! Right now! Seriously! Don't believe me?

### 4. Try it out!
Go back to your test server one more time and type the following again:

    @hype-bot hype

OH SNAP, LOOK:

[img]

Yes it is, hype-bot. Yes it is.


## Next steps

Check out a bunch of other docs I'm not going to
write right now!
