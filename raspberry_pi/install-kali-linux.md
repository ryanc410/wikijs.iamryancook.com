---
title: Install Kali Linux on Raspberry Pi
description: 
published: 1
date: 2022-06-30T00:34:42.316Z
tags: kali, raspberry pi, how-to
editor: markdown
dateCreated: 2022-06-30T00:34:37.444Z
---

# Pre-Requisites
- Raspberry Pi 4 Single Board Computer
- Micro SD Card (atleast 8gb) preferably a Class 10
- Raspberry Pi Imager Software
- Kali Linux ISO for Raspberry Pi

# Getting Started

First thing youre going to want to do is insert the micro SD Card into a USB adapter and plug it into your computer. If you havent already, you need to download the raspberry pi imager which you can get from the <a href="https://downloads.raspberrypi.org/imager/imager_1.5.exe">Raspberry Pi Downloads Page.</a>

You will also need the latest Kali Linux ISO for the Raspberry Pi which you can get from the <a href="https://www.offensive-security.com/kali-linux-arm-images">Offensive Security Download Page.</a>

# Flashing the Micro SD Card

Open the Raspberry Pi Imager program and you should see the page below. Select Choose OS, and at the bottom of the list should be the Custom option. Next, navigate to where you downloaded the Kali Linux ISO and select it.

![imager_1.png](/imager_1.png)

Back at the main screen choose Select Storage, and select the Micro SD Card you have inserted for this installation.

![imager_3.png](/imager_3.png)

Finally, you can select the option "Write" and wait for the process to finish.