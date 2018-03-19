---
title: "RPi_motion_surveilliance"
date: 2018-03-18T22:52:10-04:00
draft: false
tags: [Raspberry Pi]
categories: [tech]
---

After watching two online courses on **Coursera**, I'm going to put what I've learned about **Raspberry Pi** into practice. Basically, those two courses which are taught by a professor from UC Irving cover a wide range of topics related with RPi and IoT stuff including web connection, usage of GPIO, camera module, application examples like `blink.py` and `send_receive_twitter.py` and so on.

So the prototype is a **motion surveillance** app with multiple alert action functions, which will be my capstone project for current stage of RPi learning.

The code now is able to achieve a few functions like uploading photos of detected objects to my dropbox folder automatically. The final version will definitely more complicated. In my mind, there're three main parts for `BIG BRO (v1.0)`, the name that I'd like to call this IoT app:
- Camera Device
  - savor machine
- Image Processing  
  - OpenCV
- Alter Actions
  - blink
  - twitter statuses_update
  - dropbox

Hope `BIG BRO` will be born as soon as possible!
