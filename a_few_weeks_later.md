

## A few weeks later 🪞

#### How's the service going❓

**TL;DR good not great but credit to GigaComm they were transparent, responsive and showed a lot more ownership than my previous ISPs have.** 

I'm ok with problems because cloud, technology, network and solving problems has been my 'bread and butter' for many years, we'll just say twenty years so I don't feel as old as I am.... Below is a journal for the period 28th Dec 21 to 20th Jan 22, I believe it is a fair and balanced view. There were some small problems that GigaComm got all over and fixed along with a firewall upgrade as predicted in [part3](https://github.com/alexanderswift/public-gigacom/blob/main/testing_and_final_thoughts.md).

----

#### 28th Dec 2021:

I noticed my VPN's (work) dropped and pausing / dropping in my online streaming pausing, The thing with Internet so fast you notice the slightest pauses 🤷‍♂️. Problems started during the morning and my upload speed had taken noticeable hit. 

Tests indicted the line is limited to 50Mbps then drops off so I contacted [GigaComm via there Support email](https://github.com/alexanderswift/public-gigacom/blob/main/pics/emailtogigacomm-28thDec2021.pdf) and they said; *"We’ve had some issues overnight with a link that was running errors."*



<img src="https://github.com/alexanderswift/public-gigacom/blob/main/pics/packet-loss-28thDec21.png" alt="packet-loss-28thDec21" style="zoom: 25%;" />

<img src="https://github.com/alexanderswift/public-gigacom/blob/main/pics/slow-upload-28thDec21.png" alt="slow-upload-28thDec21" style="zoom:25%;" />

---

#### 4th Jan 2022:

Surprise text from GC Support! I always appreciate the transparency, it's the first time an ISP has sent me a text about service. 👏



<img src="https://github.com/alexanderswift/public-gigacom/blob/main/pics/gigacomm-txt-4thJan22.jpeg" alt="gigacomm-txt-4thJan22" style="zoom:25%;" />

---

#### 5th to 6th Jan 2022:

More problems on the service (and yes everything has had a reboot), I noticed more dropouts and the youtube ‘*wheel of wait*’ from about 8pm on the 5th Jan. This time there was a slight oddity that the speedtest.net site thinks I’m in Melbourne and selects a Melbourne server and the speed is woeful, **as low as 20Mbps.**

Time to perform a few tests and from my observation it looked like a problem on just a few paths through the GigaComm network. During my testing (locally and interstate) selecting the Launtel Sydney & Melbourne speed test servers the results are as you'd expect for a Gigabit service but to the GigaComm Sydney and Melbourne speed test servers, eek, they returned some woeful speeds.



**Tests**

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

---

#### 7th Jan 2022 - 09:30:

##### As the saying goes...

~~~
		“You can't optimise it until you can measure it”!!
~~~

I dusted off and plugged in my usual network troubleshooting toolkit, a PoE powered ASUS Tinker Board running [DietPI](https://dietpi.com), it's a [Telegraf collector](https://docs.influxdata.com/influxdb/v2.1/write-data/no-code/use-telegraf/) and an open-source time series database [InfluxDB](https://www.influxdata.com/products/influxdb/) that is the data for [Grafana](https://grafana.com) (observability platform). In simple terms the raspberry pi device monitors and tests using the [speedtest cli](https://www.speedtest.net/apps/cli) a single test every two hours and writes the results in to a lightweight database and the graphs are produced as you'll see below. 

Hot tip: You can get an ASUS Tinker Board kit for about A$75, Influx & Telegraf open source and Grafana Cloud offers a [free tier](https://grafana.com/products/cloud/pricing/) option and this means you don't need the 'home server' running up that power bill. There's also no additional noise, heat, it's PAT (partner acceptance test) certified and you can learn skills in a popular cloud tool stacks along the way.

- Firewall / Router stats show a utilised but okay firewall.

![7th Jan 24hr firewall](https://github.com/alexanderswift/public-gigacom/blob/main/pics/7thJan2021-24hr-firewall-stat.png)



- SpeedTest stats show the results of one test every sixty minutes to the best available SpeedTest server.

![7th Jan 24hr speedtest](https://github.com/alexanderswift/public-gigacom/blob/main/pics/7thJan2021-24hr-speedtest-stat.png)

---

#### **7th Jan 2022 - 14:00:** Are GigaComm traffic shaping the service❓

TL;DR they state in there [Acceptable & Fair Use Policy](https://www.gigacomm.net.au/hubfs/GigaComm%20Website/PDF%20Fact%20Sheets/GigaComm-Acceptable-Fair-Use-Policy-21102020.pdf) "we may"

![](https://github.com/alexanderswift/public-gigacom/blob/main/pics/GigaComm-Acceptable-Fair-Use-Policy-21102020.png)



It's **<u>possible</u>** (**and I could be wrong**) that some traffic shaping is slowing down my traffic during tests and if so I'd take a guess **based on my traceroute etc** it's in the core of the GigaComm network.

- If there was congestion on a network the latency / ping times would increase because by design and router/firewall software implementations of ICMP means ICMP is treated as low priority thus the latency and jitter increases.  
- Traffic to some hosts like the Launtel Melbourne & Sydney SpeedTest servers are not slowed down because they are connected to GigaComm over the equinix peering lan and it's my understanding (**and I could be wrong**) that traffic shaping is not often required or even discouraged on open-peering networks (not billed) thus the route to Launtel in Melbourne routes via Launtel's network. During **[my testing](https://github.com/alexanderswift/public-gigacom/blob/main/pics/6th-Jan-evening.png)** I captured the IP address (you're looking for many connections on :8080) and performing a traceroute to each hosts when that host was not connected via equinix peering lan the speed was significantly reduced.

---

#### **7th Jan 2022 - 16:30:**

**I was wrong GigaComm aren't traffic shaping** or slowing and down my traffic during tests. On another positive for GigaComm, they're transparent, responsive and they're owning it 👍.

I've received a [GigaComm Planned Network Outage](https://github.com/alexanderswift/public-gigacom/blob/main/pics/PlannedNetworkOutage-10thJan22.pdf) notification for Monday 10th Jan 2021, eek lots more WFH this year so 🤞this goes well and doesn't 🧱 my day. I still have my TPG line connected as a backup but have submitted my cancellation.

---

#### 10th Jan 2021

GigaComm emailed back to say "*confirming we've successfully rectified the errors and packet loss issues here. If you're still having issues let us know so we can investigate further*". Looking at the results of a ping test and Grafana panel for the past 12 hours it looks like a significant improvement..  

- Ping shows zero loss% so it looks like the GigaComm has fixed the problem 🤞

![10th Jan ping](https://github.com/alexanderswift/public-gigacom/blob/main/pics/10th-Jan-evening.png)

- SpeedTest stats show the results of one test every one hundred and twenty minutes to the best available SpeedTest server.

![10th Jan 12hr speedtest](https://github.com/alexanderswift/public-gigacom/blob/main/pics/10thJan2022-12hr-speedtest-stat.png)

---

#### 16th Jan 2022

Looking back 7 days and there's a significant improvement in the speed and there's no unknown drops in service.

![16th Jan 7d speedtest](https://github.com/alexanderswift/public-gigacom/blob/main/pics/16thJan2021-7d-speedtest-stat.png)

![16th Jan 7 day uptime](https://github.com/alexanderswift/public-gigacom/blob/main/pics/16thJan2021-7d-uptime.png)

---

#### 20th Jan 2022

Looking back 14 days there's few things to note in the graphs, 

- The scale on the graph, the first bar is 250Mb/s so although there was an issue I still had a very usable ~100Mbps in both directions.
- 7th to 10th Jan the period where GigaComm acknowledged there was an issue in upthe improvement on the 10th Jan 22
- 14th Jan my new firewall arrived, thus the as discussed and predicted in [part3](https://github.com/alexanderswift/public-gigacom/blob/main/testing_and_final_thoughts.md) there's a difference between switching, routing and inspecting (firewall) traffic at 1Gbps. 

![19th Jan 7d speedtest](https://github.com/alexanderswift/public-gigacom/blob/main/pics/19thJan2022-7d-speedtest-stat.png)

![19th Jan 14d speedtest](https://github.com/alexanderswift/public-gigacom/blob/main/pics/19thJan2022-14d-speedtest-stat.png)

---



### Summary 

I still highly recommend GigaComm as a provider because they are transparent, responsive and owned their (small) problems and I believe it's how you respond and learn from problems that builds a better network and experience for your customers. 

The low latency, zero point nothing jitter and Gigabit speed enabled by their infrastructure approach is awesome for domestic and international video calling, working from home, uploading / downloading my work from the Cloud and 🤞subtracting a few days ~7th to 10th Jan it has been reliable and fast.

