---
layout: post
title:  "Molemaker"
date:   2026-03-10
desc: "Exfiltrating Exfiltrations"
author: "OakTree"
categories: projects
hide_preview: true
---

Telegram bots are frequently used as a means of data exfiltration and C2 communication in phishing, malware, and many other flavors of both cybercrime and -- on occasion -- nation-state operations. The frequency of this tactic likely arises from the Telegram API's accessibility: any user is able to create their own bot and leverage it however they'd like (note: this is not a critique of the API's accessibility, rather an observation of a low barrier of entry).

As such, defenders can also use the Telegram API to develop methods for enumerating the details regarding who owns a particular Telegram bot, the channel(s) it interacts with, and even what data it has sent and/or received. Research has already been done into this topic:
<ul>
    <li> <a href="https://cofense.com/blog/weaponizing-telegram-bots-how-threat-actors-exfiltrate-credentials"> Cofense </a> </li>
    <li> <a href="https://checkmarx.com/blog/how-we-were-able-to-infiltrate-attacker-telegram-bots/"> Checkmarx </a> </li>
    <li> <a href="https://www.forcepoint.com/blog/x-labs/tapping-telegram-bots?utm_source=chatgpt.com"> Forecepoint </a> </li>
</ul>
 though I wanted to develop a novel Python-based CLI tool to more easily conduct such enumerations.

The crux of enumerating via the Telegram API relies on three endpoints:

```javascript
https://api.telegram.org/BOT_TOKEN/getUpdates

https://api.telegram.org/BOT_TOKEN/forwardMessage?chat_id=YOUR_CHANNEL_ID&from_chat_id=BOT_CHANNEL_ID&disable_notification=True&message_id=MESSAGE_ID

https://api.telegram.org/BOT_TOKEN/getChat?chat_id=BOT_CHANNEL_ID
```
coupled with several other endpoints that allow for covering up proof of exfiltration, digestible logging and -- most importantlt -- deleted of any doubled messages during exfiltration (more on this later).

When initiated, Molemaker will ask for the range of message IDs you wish to enumerate. This can be any range of values, though it is generally beneficial to start from 0-1000, and extend onward should this not be sufficient; the tool as it is now will continue attempting to enumerate messages even when none are detected, as the manner in which Telegram message IDs are assigned is not strictly incremental relative to the chat itself. That is to say, enumerating a message will increment the chat's message ID counter, such that to the original chat user the next message ID will appear to have skipped over one.

Molemaker is able to exfiltrate data in two modes:
<ul>
    <li>To a Defender-controlled channel</li>
    <li>In the Attacker-controlled channel</li> 
</ul>

Exfiltrating to a Defender-controlled channel is the conventional method of using the Telegram API for this task: you create your own channel, add the Attacker-controlled bot, provide your channel's unique ID to the tool, and visually see messages begin appearing in your channel. Files such as documents and videos are downloadable via this method, as you have access to all the capabilities that any normal user of the Telegram GUI would. It is important to remember that although the Attacker will not see their messages being exfiltrated, should they check the /getUpdates endpoint they will see that their bot has been added to an unkown channel, likely prompting them to remove the bot from a Defender-controlled channel or shut the bot down entirely.

However, an Attacker-controlled bot will occasionally be configured such that a Defender is unable to successfully add it to their own channel. In these instances, Molemaker allows the Defender to forgo creating their own channel entirely, instead relying on an important feature of the forwardMessage endpoint: forwarding messages to the same channel where they appeared. You are effectively doubling the message in the Attacker's channel. Naturally, this is an alarming visual for any Attacker looking at their channel, though in the event that the Attacker is not observing the channel's activity, Molemaker uses the deleteMessage endpoint to remove the extra message from the chat entirely -- in the end, the channel will look just as it did originally.

With this, we can see the pros and cons of either Molemaker mode:
<table style="table-layout: fixed; width: 100%;">
  <tr>
      <th>Mode</th>
      <th>Pros</th>
      <th>Cons</th>
  </tr>
  <tr>
    <td>To Defender-Controlled Chat</td>
    <td>Invisible to the Attacker while exfiltrating messages</td>
    <td>Risk of the Attacker noticing their bot has been added to an unknown channel</td>
  </tr>
  <tr>
    <td>In Attacker-Controlled Chat</td>
    <td>There is no need to erase traces of the bot being added to a Defender-controlled chat</td>
    <td>The Attacker is able to visually see the messages being doubled and deleted</td>
  </tr>
</table>

--IN-PROGRESS--