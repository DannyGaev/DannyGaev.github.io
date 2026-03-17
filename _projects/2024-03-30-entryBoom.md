---
layout: post
title:  "entryB00M"
date:   2024-03-30
desc: "Muddying The Phisher's Net"
author: "OakTree"
categories: projects
hide_preview: true
---

entry.B00M is an anonymous, easy-to-use tool for impeding scammers' phishing attempts through POST requests en-masse. The goal of the project is to populate scammers' Google Forms with large amounts of false data such that real responses from victims are not apparent, and scammers become unwilling to trudge through their data to look for genuine responses. 

The tool initially scrapes the Google Form's HTMl for instances of 'entry.ID', where the ID is a unique value that must be saved in order to send data to it.

All payload data is generated via a mixture of sources: more general information (job title, etc.) is psuedo-randomly derived from arrays of hardcoded values, while more sensitive data that may correspond to real people is generated as randomly as possible with external libaries and third-party API queries. The result is a faux profile consisting of information that cannot be attributed to any one actual individual, and therefore further inhibits the scammers' datasets.

entry.B00M's combines these elements through four modules:

![entry.B00M Diagram](/assets/images/entryBoom/diagram.png)

entry.B00M serves as the primary module through which the auxiliary modules are funnelled: one for information generation, payload delivery, and form scraping respectively. entry.B00M requires that the Tor Browser be installed on the user's machine, such that a Tor session may be opened to send and receive payload data with increased anonymity.

Separately from impeding a scammer's imemdiate ability to either compromise accounts or sell collected data, entry.B00M strives to inject distrust into the economy of information selling. For every dataset containing large amounts of fraudulent data, the seller will be forced to restablish their credibility -- a trait always in devicit in such areas of the Internet.