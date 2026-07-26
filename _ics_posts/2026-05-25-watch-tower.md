


---
layout: post
title:  "Factory"
date:   2026-06-03
description: "Our infrastructure is under attack! The HMI interface went offline and we lost control of some critical PLCs in our ICS system. Moments after the attack started we managed to identify the target but did not have time to respond. The water storage facility's high/low sensors are corrupted thus setting the PLC into a halt state. We need to regain control and empty the water tank before it overflows. Our field operative has set a remote connection directly with the serial network of the system."
author: "OakTree"
categories: writeups
---

<h2> This is an Easy Hack The Box challenge from the ICS category </h2>

<p> "Our infrastructure is under attack! The HMI interface went offline and we lost control of some critical PLCs in our ICS system. Moments after the attack started we managed to identify the target but did not have time to respond. The water storage facility's high/low sensors are corrupted thus setting the PLC into a halt state. We need to regain control and empty the water tank before it overflows. Our field operative has set a remote connection directly with the serial network of the system."</p>


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