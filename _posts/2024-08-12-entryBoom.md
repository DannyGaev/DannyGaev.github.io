---
layout: post
title:  "entryB00M"
date:   2024-08-12
description: "Muddying The Phisher's Net"
author: "OakTree"
categories: projects
hide_preview: true
---

entry.B00M is an anonymous, easy-to-use tool for impeding scammers' phishing attempts through POST requests en-masse. The goal of the project is to populate scammers' Google Forms with large amounts of false data such that real responses from victims are not apparent, and scammers become unwilling to trudge through their data to look for genuine responses. 

The tool initially scrapes the Google Form's HTMl for instances of 'entry.ID', where the ID is a unique value that must be saved in order to send data to it.

All data that is sent is generated via a mixture of sources: information that is more general (job title, etc.) are psuedo-randomly derived from a mixture of hardcoded values, while more sensitive data that may correspond to real people is generated as randomly as possible with external libaries and API queries. The result is a faux profile consisting of information that cannot be attributed to any one actual individual, and therefore further inhibits the scammers' datasets.

Separately from impeding a scammer's imemdiate ability to either compromise accounts or sell collected data, entry.B00M strives to inject distrust into the economy of information selling. For every dataset containing large amounts of fraudulent data, the seller will be forced to restablish their credibility -- a trait always in devicit in such areas of the Internet.