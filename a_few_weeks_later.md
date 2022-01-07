

## A few weeks later 

#### How's the service going❓

The TL;DR version is in short not great but credit to GigaComm(GC) they appear to be transparant and more responsive than my previous ISP. Hopefully GC



I'm ok with problems as technolgy & network problems afterall solving tech problems has been my 'bread and butter' for many years. Theres always point though where you need to see an improvement or you must consider the return on effort and when to call it quits and find another option. 



##### 28th Dec 2021: 

I noticed my VPN's (work) dropped and pausing / dropping in my online streaming pausing, The thing with Internet so fast you notice the slightest pauses 🤷‍♂️. It started during the morning and my upload speed seems to have taken noticeable hit and browser tests are indicating the line is limited to 50Mbps then drops off. 

[GigaComm Support email](https://github.com/alexanderswift/public-gigacom/blob/main/pics/emailtogigacomm-28thDec2021.pdf) said; *"We’ve had some issues overnight with a link that was running errors."*



<img src="/Users/alexs/Documents/GitHub/public-gigacom/pics/packet-loss-28thDec21.png" alt="packet-loss-28thDec21" style="zoom: 67%;" />

<img src="/Users/alexs/Documents/GitHub/public-gigacom/pics/slow-upload-28thDec21.png" alt="slow-upload-28thDec21" style="zoom:67%;" />



##### 4th Jan 2021: 

Supprise text from GC Support, it goes a way towards respecting the transparency of a provider and it's the first time an ISP has sent me a text about service. 👏



<img src="/Users/alexs/Documents/GitHub/public-gigacom/pics/gigacomm-txt-4thJan22.jpeg" alt="gigacomm-txt-4thJan22" style="zoom:33%;" />

##### 5th to 6th Jan 2021: 

More problems on the service (and yes everything has had a reboot), I noticed more dropouts and the youtube ‘wheel of wait’ from about 8pm on the 5th Jan. This time there was a slight oddity that the speedtest.net site thinks I’m in Melbourne and selects a Melbourne server and the speed is woeful, as low as 20Mbps.



So I started to perform a few tests and from my observation it looks like it's just a few paths through the GigaComm network where there's potential issues. It's the case that in my testing locally and interstate on the Launtel Sydney is as i'd expect for a Gigabit service but to the GigaComm Sydney and Melbourne speedtest servers returned some woeful speeds. 



Tests

~~~ 
To the GigaComm Sydney speedtest server.
		
		Using My Firewall / Router
		https://www.speedtest.net/result/12564763066 3ms, 122.40Mbps down, 98.90 Mbps up.
		https://www.speedtest.net/result/12564776406 3ms, 105.49Mbps down, 99.83Mbps up.

To the GigaComm Melbourne speedtest server.

		Using GigaComm supplied Router
		https://www.speedtest.net/result/12564954750 16ms, 30.87Mbps down, 100.12Mbps up.
		https://www.speedtest.net/result/12564962079 17ms, 17.48Mbps down, 100.17Mbps up.

		Using My Router
		https://www.speedtest.net/result/12564844577 15ms, 16.31Mbps down, 99.36Mbps up.
		https://www.speedtest.net/result/12564851210 15ms, 15.12Mbps down, 84.25Mbps up.

As I'd expect on a 1Gbps connection.

		To the Launtel Sydney speedtest server..
		https://www.speedtest.net/result/12564782010 4ms, 681.74Mbps down, 95.53 Mbps up.
		To the Launtel Melbourne speedtest server..
		https://www.speedtest.net/result/12564876115 15ms, 675.29Mbps down, 98.65Mbps up.

~~~



[GigaComm Support email](https://github.com/alexanderswift/public-gigacom/blob/main/pics/emailtogigacomm-6thJan22.pdf) said; *Thanks for this information Alex, I've run some tests and can see some errors and packet loss on the link that was recently connected. We are prioritizing getting someone out to resolve the errors. I'll keep you updated on progress of this.*



##### 7th Jan 2021: 

As I've said before... 

~~~
		“You can't optimise it until you can measure it”!!
~~~

So I've plugged in my usual toolkit a PoE powerder ASUS Tinker Board running [DietPI](https://dietpi.com), it's a Telegraf collector / InfluxDB open-source time series database that is the data source for Grafana (observability platform, integrating metrics, traces and logs). Hot tip: Grafana Cloud offer a [free tier](https://grafana.com/products/cloud/pricing/) option that means you don't need the 'home server' running up that power bill, there's no additional noise, heat and it's PAT (partner acceptance test) certified.

- Firewall / Router stats show a utilised but okay firewall. 

![7thJan2021-24hr-firewall-stat](/Users/alexs/Documents/GitHub/public-gigacom/pics/7thJan2021-24hr-firewall-stat.png)



- SpeedTest stats show the results of one test every sixty minutes to the best avaiable speedtest server. 

![7thJan2021-24hr-speedtest-stat](/Users/alexs/Documents/GitHub/public-gigacom/pics/7thJan2021-24hr-speedtest-stat.png)



#### Are GigaComm traffic shaping the service❓

It's **<u>possible</u>** that some traffic shaping is slowing down traffic and if I had the take a guess **based on my traceroutes etc** it's in the core of the GigaComm network. 

- If there was congestion on a network the latency / ping would increase becuase by design and router/firewall software implientations ICMP is treated as low priority thus the latency and jitter increases.  
- Traffic to some hosts like the Launtel Melbourne & Sydney speedtest servers are not slowed down becuase they are connected to GigaComm over the equinix peering lan and it's my understanding (and I could be wrong) that traffic shaping is not often required or even discouraged on open-peering networks (not billed) thus the route to Launtel in Melbourne routes via Launtel's network. During **[my testing](https://github.com/alexanderswift/public-gigacom/blob/main/pics/6th-Jan-evening.png)** I captured the IP address (you're looking for many connections on :8080) and performing a traceroute to each hosts when that host was not connected via equinix peering lan the speed was significantly reduced. 

 

##### 7th Jan 2021: 

TBC.. [GigaComm Support email](https://github.com/alexanderswift/public-gigacom/blob/main/pics/emailtogigacomm-6thJan22.pdf) said; *Thanks for this information Alex, I've run some tests and can see some errors and packet loss on the link that was recently connected. We are prioritizing getting someone out to resolve the errors. I'll keep you updated on progress of this.*
