

## A few weeks later 🪞

#### How's the service going❓

The TL;DR version, in short not great but credit to GigaComm(GC) they appear to be transparent, responsive and showing a lot more ownership than previous ISPs have. Hopefully GC get this one resolved soon because i'm back working from home and a reliable low latency connection is required.



I'm ok with problems because technology & network problems, after-all solving tech problems has been my 'bread and butter' for many years but theres always point though where you need to see an improvement or you must consider the return on effort / when to call it quits and find another option.



##### 28th Dec 2021:

I noticed my VPN's (work) dropped and pausing / dropping in my online streaming pausing, The thing with Internet so fast you notice the slightest pauses 🤷‍♂️. Problems started during the morning and my upload speed had taken noticeable hit. Tests indicted the line is limited to 50Mbps then drops off.

[GigaComm Support email](https://github.com/alexanderswift/public-gigacom/blob/main/pics/emailtogigacomm-28thDec2021.pdf) said; *"We’ve had some issues overnight with a link that was running errors."*



<img src="https://github.com/alexanderswift/public-gigacom/blob/main/pics/packet-loss-28thDec21.png" alt="packet-loss-28thDec21" style="zoom: 67%;" />

<img src="https://github.com/alexanderswift/public-gigacom/blob/main/pics/slow-upload-28thDec21.png" alt="slow-upload-28thDec21" style="zoom:67%;" />



##### 4th Jan 2022:

Surprise text from GC Support! I always appreciate the transparency, it's the first time an ISP has sent me a text about service. 👏



<img src="https://github.com/alexanderswift/public-gigacom/blob/main/pics/gigacomm-txt-4thJan22.jpeg" alt="gigacomm-txt-4thJan22" style="zoom:33%;" />

##### 5th to 6th Jan 2022:

More problems on the service (and yes everything has had a reboot), I noticed more dropouts and the youtube ‘wheel of wait’ from about 8pm on the 5th Jan. This time there was a slight oddity that the speedtest.net site thinks I’m in Melbourne and selects a Melbourne server and the speed is woeful, as low as 20Mbps.



So I started to perform a few tests and from my observation it looks like it's just a few paths through the GigaComm network where there's potential issues. It's the case that in my testing locally and interstate on the Launtel Sydney is as i'd expect for a Gigabit service but to the GigaComm Sydney and Melbourne speed test servers returned some woeful speeds.



Tests

~~~
To the GigaComm Sydney SpeedTest server.

		Using My Firewall / Router
		https://www.speedtest.net/result/12564763066 3ms, 122.40Mbps down, 98.90 Mbps up.
		https://www.speedtest.net/result/12564776406 3ms, 105.49Mbps down, 99.83Mbps up.

To the GigaComm Melbourne SpeedTest server.

		Using GigaComm supplied Router
		https://www.speedtest.net/result/12564954750 16ms, 30.87Mbps down, 100.12Mbps up.
		https://www.speedtest.net/result/12564962079 17ms, 17.48Mbps down, 100.17Mbps up.

		Using My Router
		https://www.speedtest.net/result/12564844577 15ms, 16.31Mbps down, 99.36Mbps up.
		https://www.speedtest.net/result/12564851210 15ms, 15.12Mbps down, 84.25Mbps up.

As I'd expect on a 1Gbps connection.

		To the Launtel Sydney SpeedTest server..
		https://www.speedtest.net/result/12564782010 4ms, 681.74Mbps down, 95.53 Mbps up.
		To the Launtel Melbourne SpeedTest server..
		https://www.speedtest.net/result/12564876115 15ms, 675.29Mbps down, 98.65Mbps up.

~~~



[GigaComm Support email](https://github.com/alexanderswift/public-gigacom/blob/main/pics/emailtogigacomm-6thJan22.pdf) said; *Thanks for this information Alex, I've run some tests and can see some errors and packet loss on the link that was recently connected. We are prioritising getting someone out to resolve the errors. I'll keep you updated on progress of this.*



##### 7th Jan 2022:

As I've said before...

~~~
		“You can't optimise it until you can measure it”!!
~~~

So I've plugged in my usual toolkit a PoE powered ASUS Tinker Board running [DietPI](https://dietpi.com), it's a Telegraf collector / InfluxDB open-source time series database that is the data source for Grafana (observability platform, integrating metrics, traces and logs). Hot tip: Grafana Cloud offers a [free tier](https://grafana.com/products/cloud/pricing/) option and this means you don't need the 'home server' running up that power bill. There's also no additional noise, heat, it's PAT (partner acceptance test) certified and you can learn skills in a popular cloud tool.

- Firewall / Router stats show a utilised but okay firewall.

![7thJan2021-24hr-firewall-stat](https://github.com/alexanderswift/public-gigacom/blob/main/pics/7thJan2021-24hr-firewall-stat.png)



- SpeedTest stats show the results of one test every sixty minutes to the best available SpeedTest server.

![7thJan2021-24hr-speedtest-stat](https://github.com/alexanderswift/public-gigacom/blob/main/pics/7thJan2021-24hr-speedtest-stat.png)



#### Are GigaComm traffic shaping the service❓

TL;DR they state in there [Acceptable & Fair Use Policy](https://www.gigacomm.net.au/hubfs/GigaComm%20Website/PDF%20Fact%20Sheets/GigaComm-Acceptable-Fair-Use-Policy-21102020.pdf) "we may"

![](https://github.com/alexanderswift/public-gigacom/blob/main/pics/GigaComm-Acceptable-Fair-Use-Policy-21102020.png)



It's **<u>possible</u>** (**and I could be wrong**) that some traffic shaping is slowing down my traffic during tests and if so I'd take a guess **based on my traceroute etc** it's in the core of the GigaComm network.

- If there was congestion on a network the latency / ping times would increase because by design and router/firewall software implementations of ICMP means ICMP is treated as low priority thus the latency and jitter increases.  
- Traffic to some hosts like the Launtel Melbourne & Sydney SpeedTest servers are not slowed down because they are connected to GigaComm over the equinix peering lan and it's my understanding (**and I could be wrong**) that traffic shaping is not often required or even discouraged on open-peering networks (not billed) thus the route to Launtel in Melbourne routes via Launtel's network. During **[my testing](https://github.com/alexanderswift/public-gigacom/blob/main/pics/6th-Jan-evening.png)** I captured the IP address (you're looking for many connections on :8080) and performing a traceroute to each hosts when that host was not connected via equinix peering lan the speed was significantly reduced.



##### 7th Jan 2022 - 16:30:

Well ok **GigaComm are not traffic shaping** slowing and down my traffic during testsand, on another positive for GigaComm, they're transparent, responsive and they're owning it 👍. 

I've received a [GigaComm Planned Network Outage](https://github.com/alexanderswift/public-gigacom/blob/main/pics/PlannedNetworkOutage-10thJan22.pdf) notification for Monday 10th Jan 2021, eek lots more WFH this year so 🤞this goes well and doesn't 🧱my day. I still have my TPG line connected as a backup but have submitted my cancellation.



##### 10th Jan 2021

GigaComm emailed back to say "*confirming we've successfully rectified the errors and packet loss issues here. If your still having issues let us know so we can investigate further*". Looking at the results of a ping test and Grafana pannel for the past 12 hours it looks like a significant improvement..  

- Ping shows zero loss% so it looks like the GigaComm has fixed the problem 🤞

![10th-Jan-evening](https://github.com/alexanderswift/public-gigacom/blob/main/pics/10th-Jan-evening.png)

- SpeedTest stats show the results of one test every one hundred and twenty minutes to the best available SpeedTest server.

![10thJan2021-12hr-speedtest-stat](https://github.com/alexanderswift/public-gigacom/blob/main/pics/10thJan2021-12hr-speedtest-stat.png)



16th Jan 202

**TBC...**

I'll update again if a few days time with a bit more data and observations. 
