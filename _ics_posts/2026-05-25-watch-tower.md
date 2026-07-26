---
layout: post
title:  "Watch Tower"
date:   2026-05-25
description: "Our infrastructure monitoring system detected some abnormal behavior and initiated a network capture. We need to identify information the intruders collected and altered in the network."
author: "OakTree"
categories: writeups
---

<h2> This is a Very Easy difficulty Hack The Box challenge from the ICS category </h2>

<p> "Our infrastructure monitoring system detected some abnormal behavior and initiated a network capture. We need to identify information the intruders collected and altered in the network."</p>


```python
# https://stackoverflow.com/questions/180606/how-do-i-convert-a-list-of-ascii-values-to-a-string-in-python

import pyshark

capture = pyshark.FileCapture('tower_logs.pcapng')

# Look for each time a register is written to by 192.168.1.150. 
# If true, retrieve the regnum value of the action and add to the ascii_codes list. 
# At the end, convert the acii codes to a single String.
ascii_codes = []

for packet in capture:
    if packet.ip.src == '192.168.1.150':
        if 'modbus.regnum16' in packet.modbus._all_fields:
            data = packet.modbus._all_fields['modbus.regnum16'].split()
            ascii_codes.append(int(data[-1]))

print(''.join(chr(i) for i in ascii_codes))

# FLAG:     HTB{3nc2yp710n?_n3v32_h342d_0f_7h47!@^}
```