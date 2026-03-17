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

--IN-PROGRESS--