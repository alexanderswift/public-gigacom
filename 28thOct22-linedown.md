# Random outage - 28th Oct 2022 at 16:24

### Friday 16:24 

Very specific I know thats benefit on top of the obvious security + learning of having your own pfSense firewall (or other) device at the edge of your network...

```
Oct 28 16:24:59  kernel    igb0: link state changed to DOWN
```

So on the phone I get to GigaComm support and let them do their thing, they could logon to their NTU & G.Fast bridge  so they must have an out of band method from their equipment in the MDF room.  We spoke for a while and confirmed that the my firewall WAN_DHCP gateway X.X.X.1 is down and the support person will talk to engineers and call me back.. (16:30)

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

### Friday 16:51

Support called back for a light check on the NTU modem and router, OK we've been here but if it helps the tech get their flow and my line up lets go! We rebooted and disconnected everything and (my choice) I connected a laptop direct to the AdTran and the interface was DHCP assigned x.x.x.37 but still no internet or ping reply from x.x.x.1 and we faffed about for a while and call was handed over to I assume level X support of engineer. 

I emailed in a screenshot and photos (phone on 5G) of the current simple setup.

<img src="/pics/IMG_3524.jpeg" alt="IMG_3524" style="zoom:33%;" />

### Friday 18:10

Engineer phoned at 18:10 and they had seen the support emails and photos so asked if I was running pfSense and was I technical, nice to see they aren't phoning cold. I explained I'd started at the bottom of the stack trouble shooting upwards and tried two devices, different ethernet dongles and cables and we got the supplied router our of the cupboard and connected to it to the AdTran and no 🌮. 

The engineer de-provision and re-provision the service the interface was DHCP assigned x.x.x.58 and again no 🌮, yep it's dinner time but before we quit for dinner he asked if I had Wireshark and could captured packets.  There it is, GigaComm has called it as dead AdTran and arranging a replacement. 

What you should be seeing in the below capture is response to the ARP broadcast 'Who has x.x.x.1? Tell x.x.x.58', curiously though I don't own a Synology!! I guess the service is a EtherHaul to the ISP's gateways BUT yep, thats a Synology with a Public IP address 🤯 (⚠️rant coming⚠️) data breaches happen in Australia because humans do human things like plug it in and call it done (she'll be right), is someone even hacking you if you aren't even trying to keep data safe?

![capture-28thOct2022](/pics/capture-28thOct2022.png)

### End of Play - Friday 28th Oct (so I thought). 

Field Engineer called 7pm and said he could come out and drop another AdTran for me now 🚀 and he was on the other side of the harbour so he'd be about an hour.. There's no sense in getting someone to drive across the city on a Friday night so I said tomorrow is fine, relax and enjoy your Friday evening.

It's an awesome commitment to service 💩 happens as they say, hardware fails so it's all good from my perspective, we spent a bit of time on the phone but they were good.

------

### Saturday 16:51

I was expecting the service engineer at about 4pm and the service engineer texted an ETA 👏, 🥇again great communication and to even make a service call at the weekend. He arrived with the replacement AdTran but unfortunately no 🎲, same as with the old NTU when I pugged in DHCP assigned x.x.x.238 and again many devices broadcasting ARP and x.x.x.1 was not responding so we put the old AdTran back. 

![Screenshot-1](/pics/screenshot-2022-10-29-1.png)

For comparison (not actual device I captured another router) with a functioning ARP broadcast and response as below, one device says [*Who has 192.168.20.3? Tell 192.168.20.1* and the next line is *192.168.20.3 is at 58:ef: 68:7c: c3:27*] . 

![Screenshot-2](/pics/screenshot-2022-10-29-2.png)

Time to call GigaComm but unfortunately they don't have a support line open at the weekends, but they clearly do work weekends.. Anyway the field engineer jumped on what I assume is an internal chat tool and the on call engineer was troubleshooting with the field engineer, they tested my line to the MDF and even moved the router to the MDF and unfortunately more of the same, no 🎲.

They even tried to re-jumper and provision the service on a new port but nothing, we even connected the NetComm NF18ACV router they supplied to go with the NTU. By this point there was a bit of head scratching  but what was concerning me a little I kept asking although I have an IP address that doesn't mean the gateway and the DCHP host are the same device so what and where is the gateway. 

They seemed a little confused because they could logon to the supplied NF18ACV router (likely through TR-069 Device Management) so it threw them a red-herring I suspect because the on-call engineer was falling back to it's an issue with your laptop, ok we've plugged in the NF18ACV router in and your field engineer is using his own laptop, no 🎲.

By this point someone else in my building had logged a support ticket with the same problem so they put my line back to it's original state and went off validate if the same was happening for my neighbour. 

And thats where it was left today, the original AdTran NTU and NF18ACV router connected and nothing else connected so GigaComm could keep doing whatever they need. 

### End of Play - Saturday  29th Oct 

------

### Sunday 14:30 

I've not heard anything from GigaComm but when I got home this afternoon I noticed the activity lights on the NF18ACV router flashing as normal,  we have 🎲 and a working internet connection :rocket:. Checking the router time it's about a hour off so the line came back at 12:18 and DHCP assigned x.x.x.164

```
Oct 30 11:18:56
kernel: Intrusion -> IN=eth4.1 OUT= MAC=f8:ca:59:4c:e1:6d:22:22:22:22:00:11:08:00:45:00:00:28:8e:2d:00:00:f1:06:15:e7:9d:e6:e6:67
SRC=157.230.230.103 DST=x.x.x.164 LEN=40 TOS=0x00 PREC=0x00 TTL=241 ID=36397 PR
```

RightO (great Aussie saying), so now to connect my MacBook directly to the NTU again because I'm curious what ARP broadcasts I can see on that segment. 

### Sunday 15:30 

As expected with a working internet connection the ARP broadcasts are as I expected, [*Who has x.x.x.1? Tell x.x.x..164* and the reply *x.x.x..164 is at 22:22:22:22:00:11*] . I'm still curious as to *CiscoMer 62:ed: 85* broadcasting maybe that a PoE injector for the fixed wireless equipment Or it's another customer on the same L2 segment:eyes:, hope not :crossed_fingers: because I'd be hoping for L2 isolation but then again that's why I have a pfSense firewall between me and my ISP... 

![screenshot-2022-10-30-1](/pics/screenshot-2022-10-30-1.png)

### Sunday 16:15

I don't think it's fixed yet but it's a great temporary fix :laughing: whatever GigaComm has done! 

![speedtest-30oct2022](/pics/speedtest-30oct2022.png)

Well that answers the question what speed is possible on the on the FttDP and Fixed Wireless service:question:, it will do 1Gbps symmetrical :rocket: :rocket::rocket: https://www.speedtest.net/result/13870864665.png 

Now back to my normal 1Gbps down 100Mbps up.  https://www.speedtest.net/result/13889905450.png 

### Sunday 16:30 

That's me for today I'm heading to the pub for a late Sunday Roast :plate_with_cutlery: :chicken: + :beer:. 

------

### Monday 15:00 

Network Operations person I was talking too on Friday night drops me an email to say.. 

> Just following up on the outage over the weekend.
>
> I’ve been caught up on {field engineers} visit on Saturday, and was involved in the subsequent maintenance that occurred on the site on Saturday night to remedy the issue.
>
> I thought I should check in and see if your service has been restored since these events, and if you have any remaining issues with your connection after these events!
>
> Hope you’re doing well, and hope we didn’t impact your weekend too much,
>
> Thanks,

My reply *Thanks for the follow up all is well, no worries about the weekend but a big thank you to everyone at Gigacomm who gave their weekends to a bloke without internet*.  Technology, networks and cloud has been and still is my bread and butter so I understand things go wrong but as the saying goes *:poop: happens but it's what you do next that matters and subsequently what you learn from it* and GigaComm owned the issue and kept things moving :clap:

What GigaComm learn from an outage is up to them. 

------

###  Thursday 3rd November 

04:00 Line down again and GigaComm not having 24x7 support is pretty frustrating, knowing that nothing will be looked at until 9am means I now need drive to the office today. 

### Thursday 09:30 

Called GigaComm to report the fault.

### Thursday 11:08 

GigaComm called to say the line was up again but didn't say what the problem was. 

I've turned on my line monitoring Docker and will see what happens for the next fruit weeks. 

### 1 Week later

All good nice a stable the blip at 11/07 was because my suburb had a had a power cut this morning caused by the road sinking away and taking a power cable with it but thats another story of government outsourcing for another day.  

![2022-11-08-7days](/pics/2022-11-08-7days.png)
