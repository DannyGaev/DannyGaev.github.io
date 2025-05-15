---
layout: post
title:  "Till Death Do Us Part"
date:   2025-02-28
description: "A Question from a MetaCTF FlashCTF"
author: "OakTree"
categories: ctfs
---

<h1> This is a Question from a MetaCTF FlashCTF: </h1>

<p> "I was messing with trying to dual boot, and while trying to fix partitions, I accidentally deleted the one on my wedding flash drive I carelessly had plugged in! Please help me recover it!" </p>

*The artifact for this problem is a usb.img file*

<h2> Challenge Answer: </h2>
<p> For this challenge, I used the Autopsy Digital Forensics tool. <p>

*Autopsy can be downloaded for free at https://www.autopsy.com/download/*

<p> On opening Autopsy, I added usb.img as a "Disk Image or VM File" data source. <p>

<p> When the image is finished loading, we can see several curious things. There are some wedding photos, spreadsheets
and text files -- feel free to save them! We won't be using them, they are useless. <p>

<p> Navigating through Data Sources => usb.img_1 Host => usb.img => $CarvedFiles (1) we arrive at the 1 (36) folder <p>

**[*] THIS ^ PATH MAY LOOK DIFFERENTLY FOR YOU, BUT SHOULD GENERALLY BE THE SAME**

<p> In this folder, there *many* .fat files. Navigating to the one immediately after f0012446.jpg (f0014031.fat),
when inspecting the "Strings" tab on the "Text" view, we can see the letters "CTF" have been identified. <p>

<h2> YIPPEE!! </h2>

<p> Because MetaCTF flags generally follow the format of MetaCTF{some_more_content}, this is a very good sign -- 
we've stumbled on the beginning of the some_more_content part of the flag. If we move down the column from here,
recording the content in the Strings tab sandwiched between a [Z[Z and a [Z[Z (though not the "..."), we are 
able to assemble the whole flag: <p>

<p> CTF{N0T_EV3N_D3L3t10n_C4N_S3PART3_U5} <p>

<p> following the rules of the flag format, the flag we want to submit is: <p>

<p> MetaCTF{N0T_EV3N_D3L3t10n_C4N_S3PART3_U5} </p>