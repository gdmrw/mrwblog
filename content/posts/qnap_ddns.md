---
title: How to make QNAP NAS DDNS functional while using Tproxy
date: 2023-03-08 21:55:34
tags: 
- qnap nas
- ddns
- openwrt
- HBS
pic: qnap.jpeg
---

>Prerequisite: Before proceeding, it is essential to have a static public IP. If you do not already have one, kindly reach out to your ISP for assistance. Please note that if you are unfamiliar with QNAP NAS, this article may not cater to your requirements.

---


For several reasons, you cannot connect to many cloud storage server like google drive in China, which make it difficult to fully function the HBS3(Hybrid Backup Sync). To solve those problem, I add a proxy gateway to my family network and make some configuration to make sQure the Transparent proxy working properly. However, this led to troubles with the Dynamic Domain Name System (DDNS) due to the changes in configuration. This issue had persisted for quite some time until I finally discovered the solution to the mystery. 

Initially, I encountered issues with Myqnapcloud DDNS not functioning despite correctly configuring port forwarding or DMZ on my router. However, upon inspecting the DDNS IP address and comparing it with my public IP, I discovered that they did not match. I was surprised to find that the DDNS was erroneously pointing to my proxy IP. After couples of searches, finally I realized that I was not fully familiar with the working principle of DDNS, and the proxy routing function treated the DDNS server data as a flow requiring proxy, causing the issue.

In order to solve the above problems,you need to take the following steps:

* **1.Filed a ticket with QNAP to obtain a list of their ddns name servers.**

* **2.Added these servers to your routing rules to ensure a direct connection when the ddns name server tries to trace the correct IP.**

* **3.Ensured that the port mapping/port forwarding function is enabled and properly configured in both the router and proxy gateway. This needs to be done twice to ensure that the correct ports are open on both sides.**

>https://auth.api.myqnapcloud.com
>https://auth.myqnapcloud.io
>https://edge.api.myqnapcloud.com
>https://edge.myqnapcloud.io
>https://core2.api.myqnapcloud.com
>https://core2.myqnapcloud.io

The above list is what I know QNAP use for DDNS, if no, raise a ticket to ask them again. 

Your myqnapcloud may functioning now. Overall, it is not a formidable cases when you know the running theory of DDNS and Tproxy. Myqnapcloud is a good app, it help me save a lot of configuration step, but at the same time, it also makes me omit some underlying logic of DDNS and hinder me to solve the wrong pointing issue. 
