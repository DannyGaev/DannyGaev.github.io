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

![entry.B00M Diagram](/assets/images/entryBoom/entryBoomDiagram.png)

entryBoom.py serves as the primary module through which the auxiliary modules are funnelled: form scraping, payload generation, and payload delivery. entry.B00M requires that the Tor Browser be installed on the user's machine, such that a Tor session may be opened to send and receive payload data with increased anonymity.

formScrape.py loads an HTML version of the targeted Google Form, and searches for each specific ID value corresponding to present entries:

![Google Form Diagram](/assets/images/entryBoom/googleFormDiagram.png)

once all the IDs are collected, each reespective type of input field (text, multiple choice, etc.) is identified and the appropriate type of information is generated for the payload. Prior to actual payload delivery, a sample payload is presented to the user as a means to verify the data being sent and the fields that have been identified.

When entry.B00M is finished running, succesfull payloads are tabulated and statistics are returned to the user relating the duration of the delivery and successful vs. denied requests. A sample of a 100% successful delivery may appear as follows:

![Sample Run](/assets/images/entryBoom/sampleRun.png)

Separate from impeding a scammer's immediate ability to compromise accounts or sell victim data, entry.B00M strives to inject distrust into the economy of information selling. For every dataset containing fraudulent data, the seller will be forced to re-establish their credibility -- a trait always in devicit amongst information traffickers.