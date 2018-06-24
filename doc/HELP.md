# Bitlbee Mastodon
This document was generated from the help text for the plugin.

Mastodon is a free, open-source social network server. A decentralized solution to commercial platforms, it avoids the risks of a single company monopolizing your communication. Anyone can run Mastodon and participate in the social network seamlessly.

* *[register](#register)* - Registering an account
* *[connect](#connect)* - Connecting to an instance
* *[read](#read)* - Reading your timeline
* *[post](#post)* - Posting a new status
* *[undo](#undo)* - Undo and redo
* *[context](#context)* - Showing a status in its context
* *[reply](#reply)* - Replying to a status
* *[delete](#delete)* - Deleting a status
* *[favourite](#favourite)* - Favouring a status
* *[follow](#follow)* - Following an account
* *[block](#block)* - Blocking an account
* *[mute](#mute)* - Muting an account
* *[boost](#boost)* - Boosting a status
* *[more](#more)* - Getting more information about things
* *[search](#search)* - Searching for accounts and hashtags
* *[spam](#spam)* - Reporting a status
* *[control](#control)* - Commands in the control channel
* *[hashtag](#hashtag)* - Following a hashtag
* *[public](#public)* - Following the local or federated timeline
* *[set](#set)* - Settings affecting Mastodon accounts

## register
You need to register your Mastodon account on an **instance**. See https://instances.social/ if you need help picking an instance. It's a bit like picking a mail server and signing up. Sadly, there is currently no way to do this from IRC. Your need to use a web browser to do it. Once you have the account, see **help account add mastodon** for setting up your account.

## set
These settings will affect Mastodon accounts:

* **set auto_reply_timeout** - replies to most recent messages in the last 3h
* **set base_url** - URL for your Mastodon instance's API
* **set commands** - extra commands available in Mastodon channels
* **set message_length** - limit messages to 500 characters
* **set mode** - create a separate channel for contacts/messages
* **set show_ids** - display the "id" in front of every message
* **set target_url_length** - an URL counts as 23 characters
* **set name** - the name for your account channel
* **set hide_sensitive** - hide content marked as sensitive
* **set sensitive_flag** - text to flag sensitive content with

Use **help** to learn more about these options.

## set name
> **Type:** string  
> **Scope:** account  
> **Default:** empty  

Without a name set, Mastodon accounts will use host URL and acccount name to create a channel name. This results in a long channel name and if you prefer a shorter channel name, use this setting (when the account is offline) to change it.

> **&lt;kensanata&gt;** account mastodon offline  
> **&lt;kensanata&gt;** account mastodon set name masto  
> **&lt;kensanata&gt;** account mastodon online  
> **&lt;kensanata&gt;** save  

## set hide_sensitive
> **Type:** boolean  
> **Scope:** account  
> **Default:** false  
> **Possible Values:** true, false, rot13, advanced_rot13  

By default, sensitive content (content behind a content warning) is simply shown. The content warning is printed, and then the sensitive content is printed.

> **&lt;somebody&gt;** [27] [CW: this is the warning] \*NSFW\* this is the text  

If you set this variable, sensitive content is not printed. Instead, you'll see "[hidden: &lt;the URL&gt;]". If you still want to read it, visit the URL.

> **&lt;kensanata&gt;** account mastodon set hide_sensitive true  
> **&lt;kensanata&gt;** save  

Don't forget to save your settings.

The result:

> **&lt;somebody&gt;** [27] [CW: this is the warning] \*NSFW\* [hidden: https://social.nasqueron.org/@kensanata/100133795756949791]  

Additionally, when using **rot13**:

> **&lt;somebody&gt;** [27] [CW: this is the warning] \*NSFW\* guvf vf gur grkg  

And when using **advanced_rot13**:

> **&lt;somebody&gt;** [27] [CW: this is the warning] \*NSFW\*   
> **&lt;somebody&gt;** CW1 guvf vf gur grkg  

All sensitive content is also marked as Not Safe For Work (NSFW) and flagged as such. You can change the text using an option, see **help set sensitive_flag**).

## set sensitive_flag
> **Type:** string  
> **Scope:** account  
> **Default:** "\*NSFW\* "  

This is the text to flag sensitive content with. The default is Not Safe For Work (NSFW). If you wanted to simply use red for the sensitive content, you could use "^C5", for example. Be sure to use an actual Control-C, here. This might be challenging to enter, depending on your IRC client. Sadly, that's how it goes. For more information, see https://www.mirc.com/colors.html.

## account add mastodon
> **Syntax:** account add mastodon &lt;handle&gt;  

By default all the Mastodon accounts you are following will appear in a new channel named after your Mastodon instance. You can change this behaviour using the **mode** setting (see **help set mode**).

To send toots yourself, just write in the groupchat channel.

Since Mastodon requires OAuth authentication, you should not enter your Mastodon password into BitlBee. The first time you log in, BitlBee will start OAuth authentication. (See **help set oauth**.)

In order to connect to the correct instances, you must most probably change the **base_url** setting. See *[connect](#connect)* for an example.

## connect
In this section, we'll sign in as **@kensanata@mastodon.weaponvsac.space**. This section assumes an existing account on an instance! Replace username and Mastodon server when trying it.

In your **&bitlbee** channel, add a new account, change it's **base_url** to point at your instance, and switch it on:

> **&lt;kensanata&gt;** account add mastodon @kensanata  
> **&lt;root&gt;** Account successfully added with tag mastodon  
> **&lt;kensanata&gt;** account mastodon set base_url https://mastodon.weaponvsac.space/api/v1  
> **&lt;root&gt;** base_url = `https://mastodon.weaponvsac.space/api/v1'  
> **&lt;kensanata&gt;** account mastodon on  
> **&lt;root&gt;** mastodon - Logging in: Login  
> **&lt;root&gt;** mastodon - Logging in: Parsing application registration response  
> **&lt;root&gt;** mastodon - Logging in: Starting OAuth authentication  

At this point, you'll get contacted by the user **mastodon_oauth** with a big URL that you need to visit using a browser. See *[connect2](#connect2)* for the OAuth authentication.

## connect2
Visit the URL the **mastodon_oauth** user gave you and authenticate the client. You'll get back another very long string. Copy and paste this string:

> **&lt;mastodon_oauth&gt;** Open this URL in your browser to authenticate: https://.......  
> **&lt;mastodon_oauth&gt;** Respond to this message with the returned authorization token.  
> **&lt;kensanata&gt;** \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  

Once you do that, your login should complete in the **&bitlbee** channel:

> **&lt;root&gt;** mastodon2 - Logging in: Requesting OAuth access token  
> **&lt;root&gt;** mastodon2 - Logging in: Connecting  
> **&lt;root&gt;** mastodon2 - Logging in: Verifying credentials  
> **&lt;root&gt;** mastodon2 - Logging in: Getting home timeline  
> **&lt;root&gt;** mastodon2 - Logging in: Logged in  

You should now have a channel called **#mastodon.weaponsvsac.space@localhost** where all the status updates and notifications get shown. We'll call this your **account channel**. See **help set name** to change it's name.

Mastodon gives BitlBee a permanent authentication token, which will be saved in your configuration.

You should probably save this configuration.

> **&lt;kensanata&gt;** save  
> **&lt;root&gt;** Configuration saved  

## read
The default **mode** setting is **chat**. This means that each Mastodon account you add will result in a new channel in your IRC client.

Use **help set mode** in your Bitlbee control channel (**&bitlbee**) to read up on different modes.

## post
The default **commands** setting is **true**. This means that anything you type is a toot unless it looks like command, in which case it is handled as such. In addition to that, you can use the **post &lt;message&gt;** command. If you set the **commands** setting to **strict**, using the **post** command is mandatory.

Use **help set commands** in your Bitlbee control channel (**&bitlbee**) to read up on the various commands.

A well behaved Mastodon client will limit your toots to 500 characters even though the underlying protocols allow for longer messages. By default, Bitlbee does the same. Use **help set message_length** in your Bitlbee control channel (**&bitlbee**) to read up on the hairy details. Basically, some aspects of of your message will count for less: URLs, domain names for mentioned user accounts and the like. See **help set target_url_length** for more information on how URLs are counted.

Note also that Bitlbee itself does word-wrapping to limit messages to 425 characters. That is why longer messages may look like extra newlines have been introduced but if you check the status on the web, you'll see that everything is OK.

## undo
Use **undo** and **redo** to undo and redo recent commands. Bitlbee will remember your last 10 Mastodon commands and allows you to undo and redo them.

Use **history** to see the list of commands you can undo. There is a pointer (**&gt;**) showing the current position.

Use **history undo** if you are interested in seeing the commands that will be used to undo what you just did.

## favourite
Use **fav &lt;id|nick&gt;** to favour a status or the last status by a nick. Synonyms: **favourite**, **favorite**, **like**.

Use **unfav &lt;id|nick&gt;** to unfavour a status or the last status by a nick. Synonyms: **unfavourite**, **unfavorite**, **unlike**, **dislike**.

## context
Use **context &lt;id|nick&gt;** to show some context for a status or the last status by a nick. This will display the ancestors and descendants of a status.

Use **timeline &lt;nick&gt;** to show the most recent messages by a nick.

## reply
If you use the default IRC conventions of starting a message with a nickname and a colon (**:**) or a comma (**,**), then your message will be treated as a reply to that nick's last message. As is custom, the recipient and all the people they mentioned in their toot will get mentioned in your reply.

This only works if that nick's last message was sent within the last 3h. For more information about this time window use **help set auto_reply_timeout** in your Bitlbee control channel (**&bitlbee**).

You can also reply to an earlier message by referring to its id using the **reply &lt;id&gt; &lt;message&gt;** command. Again, the recipient and all the people they mentioned in their toot will get mentioned in your reply.

If you set the **commands** setting to **strict**, using the **reply** command is mandatory.

## delete
Use **del &lt;id&gt;** to delete a status or your last status. Synonym: **delete**.

## favourite
Use **fav &lt;id|nick&gt;** to favour a status or the last status by a nick. Synonyms: **favourite**, **favorite**, **like**.

Use **unfav &lt;id|nick&gt;** to unfavour a status or the last status by a nick. Synonyms: **unfavourite**, **unfavorite**, **unlike**, **dislike**.

## follow
Use **follow &lt;nick|account&gt;** to follow somebody. This determines the nicks in your channel. Verify the list using **/names**.

Usually you'll be providing a local or remote account to follow. In the background, Bitlbee will run a search for the account you provided and follow the first match. Sometimes there will be nicks in the channel which you are not following, e.g. a nick is automatically added to the channel when a status of theirs mentioning you is shown.

Use **unfollow &lt;nick&gt;** to unfollow a nick. Synonyms: **allow**.

## block
Use **block &lt;nick&gt;** to block a nick on the server. This is independent of your IRC client's **/ignore** command, if available.

Use **unblock &lt;nick&gt;** to unblock a nick.

## mute
Use **mute user &lt;nick&gt;** to mute a nick on the server.

Use **unmute user &lt;nick&gt;** to unmute a nick.

Use **mute &lt;id|nick&gt;** to mute the conversation based on a status or the last status by a nick. Muting a status will prevent replies to it, favourites and replies of it from appearing.

Use **unmute &lt;id|nick&gt;** to unmute the conversation based on a status or the last status by a nick.

## boost
Use **boost &lt;id|nick&gt;** to boost a status or the last status by a nick.

Use **unboost &lt;id|nick&gt;** to unboost a status or the last status by a nick.

## more
Use **url &lt;id|nick&gt;** to get the URL to a status or the last status by a nick.

Use **whois &lt;id|nick&gt;** to show handle and full name by a nick, or of all the nicks mentioned in a status.

Use **bio &lt;nick&gt;** to show the bio of a nick.

Use **pinned &lt;nick&gt;** to show the pinned statuses of a nick.

Use **info instance** to get debug information about your instance.

Use **info user &lt;nick|account&gt;** to get debug information about an account.

Use **info relation &lt;nick|account&gt;** to get debug information about the relation to an account.

Use **info &lt;id|nick&gt;** to get debug information about a status or the last status by a nick.

## search
Mastodon allows you to search for three kinds of things: accounts, hashtags, and the URLs of a status.

Use **search &lt;what&gt;** to get debug information about the things found by a search.

## spam
Use **report &lt;id|nick&gt; &lt;comment&gt;** to report a status or the last status by a nick. Synonyms:**spam**.

Note that the comment is mandatory. Explain why the status is being reported. The administrator of your instance will see this report and decide what to do about it, if anything.

## control
As we said at the beginning, the default **mode** setting is **chat**. This means that each Mastodon account you add will result in a new channel in your IRC client. All the commands mentioned above are what you type in this "instance channel."

There are some standard root commands that only work in the control channel, **&bitlbee**.

## hashtag
This also happens from the control channel, **&bitlbee**.

Here's how to subscribe to **#hashtag** for the account **mastodon**. The **chat add** command takes the parameters **account**, **hashtag**, and **channel name**. In the example we're simply giving the channel the same name. You can name the channel whatever you want. The important part is that the channel **topic** must be the hashtag it is subscribing to.

> **&lt;kensanata&gt;** chat add mastodon hashtag #hashtag  
> **&lt;kensanata&gt;** channel #hashtag set auto_join true  
> **&lt;kensanata&gt;** /join #hashtag  

Don't forget to **save** your config.

Note that where as you can still issue commands in these hashtag channels, the output is going to appear in the original **account channel**.

## public
This also happens from the control channel, **&bitlbee**.

Here's how to subscribe to the **local** or **federated** timeline for the account **mastodon**. The **chat add** command takes the parameters **account**, **timeline**, and **channel name**. In the example we're giving the channel a similar name. You can name the channel whatever you want. The important part is that the channel **topic** must be the name of the timeline it is subscribing to.

> **&lt;kensanata&gt;** chat add mastodon local #local  
> **&lt;kensanata&gt;** channel #local set auto_join true  
> **&lt;kensanata&gt;** /join #local  

Or:

> **&lt;kensanata&gt;** chat add mastodon federated #federated  
> **&lt;kensanata&gt;** channel #federated set auto_join true  
> **&lt;kensanata&gt;** /join #federated  

Don't forget to **save** your config.

Note that where as you can still issue commands in these channels, the output is going to appear in the original **account channel**.
