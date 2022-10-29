# Random outage - 28th Oct 2022 at 16:24

### 16:24 

Very specific I know thats benefit on top of the obvious security + learning of having your own pfSense firewall (or other) device at the edge of your network...

```
Oct 28 16:24:59  kernel    igb0: link state changed to DOWN
```

So on the phone I get to GigaComm support and let them do their thing, they could logon too their NTU & G.Fast bridge  so they must have an out of band method from their equipment in the MDF room.  We spoke for a while and confirmed that the my firewall WAN_DHCP gateway X.X.X.1 is down and the support person will talk to engineers and call me back.. (16:30)

```
-- Outside of firewall ✅
alexs@alexs-MacBookPro ~ % ping -c 2 x.x.x.17
PING x.x.x.17 (x.x.x.17): 56 data bytes
64 bytes from x.x.x.17: icmp_seq=0 ttl=64 time=1.336 ms
64 bytes from x.x.x.17: icmp_seq=1 ttl=64 **time=7.744 ms <<< Umm**

--- x.x.x.17 ping statistics ---
2 packets transmitted, 2 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = **1.336/4.540/7.744/3.204 ms <<< Umm**
alexs@alexs-MacBookPro ~ %

-- GigaComm router 🌵
alexs@alexs-MacBookPro ~ % ping -c 2 x.x.x.1
PING x.x.x.1 (x.x.x.1): 56 data bytes
Request timeout for icmp_seq 0

--- x.x.x.1 ping statistics ---
2 packets transmitted, 0 packets received, **100.0% packet loss <<< Ohhh**
alexs@alexs-MacBookPro ~ %

-- DNS 🌵
alexs@alexs-MacBookPro ~ % host google.com
Host google.com not found: 2(**SERVFAIL**)

```

### 16:51

Support called back for a light check on the NTU, routers and modem, OK we've been here but if it helps the tech get their flow and my line up lets go! We rebooted and disconnected everything and (my choice) I connected a laptop direct to the AdTran and the interface was DHCP assigned x.x.x.37 but still not internet or ping reply from x.x.x.1 and we faffed about for a while and call was handed over to I assume level X support of engineer. 

I emailed in a screenshot and photos (phone on 5G) of the current simple setup.

<img src="/pics/IMG_3524.jpeg" alt="IMG_3524" style="zoom:50%;" />

### 18:10

Engineer phoned at 18:10 and they had seen the support emails and photos so asked if I was running pfSense was technical, nice to see they aren't phoning cold. I explained I'd started at the bottom of the stack trouble shooting upwards and tried two devices, different ethernet dongles and cables and we got the supplied router our of the cupboard and connected to it to the AdTran and no 🌮. 

The engineer de-provision and re-provision the service the interface was DHCP assigned x.x.x.58 and again no 🌮, yep it's dinner time but before we quit for dinner he asked if I had Wireshark and could captured packets.  There it is, GigaComm has called it as dead AdTran and arranging a replacement. 

What you should be seeing in the below capture is response to the ARP broadcast 'Who has x.x.x.1? Tell x.x.x.58', curiously though I don't own a Synology!! I guess the service is a EtherHaul to the ISP's gateways BUT yep, thats a Synology with a Public IP address 🤯 (⚠️rant coming⚠️) data breaches happen in Australia because humans do human things like plug it in and call it done (she'll be right), is someone even hacking you if you aren't even trying to keep data safe?

![capture-28thOct2022](/pics/capture-28thOct2022.png)

### End of Play - Friday 28th Oct (so I thought). 

Field Engineer called 7pm and said he could come out and drop another AdTran for me now 🚀 and he was on the other side of the harbour so he'd be about an hour.. There's no sense in getting someone to drive across the city on a Friday night so I said tomorrow is fine, relax and enjoy your Friday evening.

It's an awesome commitment to service and 💩 happens as they say hardware fails so it's all good from my perspective, we spent a bit of time on the phone but they were fairly .

### Saturday 29th Oct 

I was expecting the field engineer at about 4pm and the service engineer texted an ETA 👏, 🥇again great communication and service to even make a service call at the weekend. He arrived with the replacement AdTran but unfortunately no 🎲, same as with the old NTU when I pugged in DHCP assigned x.x.x.238 and again many devices broadcasting ARP and x.x.x.1 was not responding. 

![Screenshot 2022-10-29 at 21.48.46](/pics/Screenshot 2022-10-29 at 21.48.46.png)

For comparison (not actual device I captured another router) with a functioning ARP broadcast and response as below, one device says [*Who has 192.168.20.3? Tell 192.168.20.1* and the next line is *192.168.20.3 is at 58:ef: 68:7c: c3:27*] . 

![Screenshot 2022-10-29 at 21.58.16](/pics/Screenshot 2022-10-29 at 21.58.16.png)

Time to call GigaComm but unfortunately they 

