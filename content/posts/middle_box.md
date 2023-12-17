---
title: How Middleboxs Identify Proxy Traffics
date: 2022-10-22 23:36:11
author: Coia
showtoc: ture
tags:
- http
- tls
---
# Abstract
There is no absolute safe disguise, all protocols have risks of detected. 

## Common attack made by middle box 
- Passive analysis (Traffic characteristic, PoC vulnerability)
Usually use for plain text protocol or TLS handshake.

- Active analysis
Usually use for Shadowsocks, V2Ray, TLS v1.3 (obtian svers's SSL certificate)

- replay package

## Some obvious charecteristics of proxy traffic. 
- Long connection 
Most HTTP traffic is short connection.

- bidireaction flow 
99% of Web traffic(HTTP) is one-way flow, which is a group of request match a group of response, few website use websocket.

- High traffic
Lack of reasons to justify large traffic.

- High connection numbers
Normally a website will only create one websocket connection, hard to explain why there are 20-30 connections existed. 

- Point to point
IP to IP, high encryption, high traffic, thus ---- high suspiciousness

Those charecteristics are always exist in proxy protocols, it will be hard to erase. 

## TLS traffic risk analysis

- ClientHello

TLS ClientHello have [fingerprint](https://fingerprint.com/blog/what-is-tls-fingerprinting-transport-layer-security/)
 
If access website using programs default fingerprint(for example: Go TLS) and match the features above. The risk that will be recongized by proxy will be high. 

> Iran firewall will reject curl and wget fingerprint request for non-whitelist, Go TLS and browsers fingerprint will be allowed. 
Recommende to connect by using browser's fingerprint. (Go project [uTLS](https://github.com/refraction-networking/utls))
> Note: this repository is disrepair and the chrome fingerprint remain at Chrome 83, it may be a risk. 
> A changable option of the above is [here](https://gitlab.com/CoiaPrant/tls) , Chrome 104 fingerprint is currently added. 

- Server Name Idication (SNI)
Highest risk for free domains, cheap domains will also contain risk. 

- TLS connection version
TlS v1.3 has the highest risk, all contents after the Server Hello will be all encrypted, middlebox need active detection to obtain server certificate. 

TLS v1.2 will be considered as median risk. All certificates exchange will be in plain text, middle box can verify it through intercept traffic. 

SSL v3/TLS v1.0/TLS v1.1 have the lowest risk , there is few traffic here, in other words, fewer sample. However, using out-dated encryption have risk of being attacked, not recommended. 

- TLS server certificate

Self-signed certificate have the highest risk. 
Second are cloudflare certificate and Let's Encrypt because they are free. 
> Almost no people will spent hunders of dollars on certificate.

## Report: New detection method that  capable to detect Fake TLS traffic
**Analysis**
Both MTPRoto FakeTLS and Shadow TLS(v1/v2) are simulate a TLS handshake with trusted certificate to circumvent whitelist. Both two protocols are nearly perfect, they can be verified as valid client while handshake. 

- How to verify client of MTProto FakeTLS 
ClientHello package remove ramdom field and make a whole package for hmac, key will be secret, also use the hmac on sevrer to verify client, random have one-time processing, it will fallback to real web server if failed. 
>  Indentification method: TLS handshake of MTProto not standardize, firewall can intercept the hostCert package and judge the length.  The lenght of hostCert will be ramdon, between 1024-4096 bit. ([mtg-faketls](https://github.com/9seconds/mtg/tree/master/mtglib/internal/faketls))

- Shadow TLS v1 won't verify client
> Identification method: send a request to the sever through curl, curl will failed. 

- How Shadow TLS v2 verify client
After client request, sever will return the orgin data as challenge response and use password to hmac. The server can verif the client using same hmac. 
Due to the return data have randomness and can also achieve one-time verification, middlebox can not react the challenge response if they don't have password, hence, it will be more safer compare with MTproto handshake.

## New measure to detect client
Most protocols security are based on server verify the client, but the client will not verify sever's validity. 
In other words, one-way authentication 
Firewall can detect the server reaction by using fake server package. Using reverse dectection to check if the clients are real browser 
> MTProto use hmac algorithm in ServerHello and will not affected by this measure. 

## How PoC identify the Shadow TLS v2
>protocol desigin [Github docs](https://github.com/ihciah/shadow-tls/blob/master/docs/protocol-cn.md)
Firewall will intercept a normal TCP connection randomly. After they get TLS ClientHello, they will hijack the request content's SNI field to real SNI server. After the TLS handshake finished, client of Shadow TLS will incert server's challenge response 8 bit before the Application Data. 

At this moment, because the opposite side is a real real TLS server, handshake with Shadow TLS client will be successful. But afer the hmac sent, server will drop an Alert(Encrypted Application Data) bacause it is not a negotiated TLS encryption. After that, the server will FIN or RST the TCP connection, at this time the ShadowTLS will be identified and can be block by ip precisely. 
> Proxy procotols will normally use multi connection. Middlebox can precisely identify the client by merely pick one of those connection. 

## Currently recommend proxy protocol
- Hystertia, TUIC(QUIC)
The firewall does not block or interfere with QUIC, so you can use it with confidence.


> "This article is translate from [Coia channel](https://telegra.ph/%E6%8A%A5%E5%91%8A-%E4%B8%AD%E9%97%B4%E7%9B%92%E5%A6%82%E4%BD%95%E8%AF%86%E5%88%AB%E4%BB%A3%E7%90%86%E6%B5%81%E9%87%8F-10-17) ,some emotional expressions have been deleted. This article not represent personal opinion "
