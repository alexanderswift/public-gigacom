

## Testing and Final Thoughts 🧪& 🤔

#### Why test❓

Over a few rainy days in late December 2021 I decided to create a baseline of the new service with the default configuration and a single device writing it  down along the way (how these documents started) . The reason for baselining my local network is so I understand the limits of my equipment before making judgements on the new internet provider, You can't optimize it until you can measure it. I've invested in [Ubiquiti unifi](https://www.ui.com) Wi-FI / PoE switches and a BYO [pfSense](https://www.pfsense.org/download/) firewall built on [PC Engines APU2](https://www.pcengines.ch/apu2.htm) hardware and for the previous 100/40Mbs internet it has provided outstanding reliability, performance and a great features per dollar ratio while having the benifit of all being low power devices because utility rates here in Australia are some of the most expensive in the world.



~~~  
													TL;DR “You can't optimise it until you can measure it”!!
~~~



The combined power total of all my equipment is less than 20watts / 0.5amp of power at an estimated $45pa and including the purchase cost has cost an estimated AU$850 over the past four years. It's was very tempting to take the approach of shopping Grays / eBay for old Enterprise equipment that was once tens of thousands of dollars but IMHO you could 20x that power bill then you have to deal with the additional noise, heat and it risks failing the PAT (partner acceptance test) so I went the way I did.




> ~~~
> Electricity Usage Per Year = (Watts / 1000) * Hours/Day * Days/Week * Weeks/Year = kWh/year
>
> Electricity Cost Per Year = kWh/year * (cents/kWh / 100) = $/year
> ~~~





#### Devices for testing:

Pretty standard devices. 

> - [x] 2x Apple MacBook Pros (2016 / 2019) with Gigabit Ethernet adapters.
>
> - [x] 1x Apple TV (yes you can, iPerf and SpeedTest available from the AppStore).
>
> - [x] 2x Unifi US-8-60W  switches.
>
> - [ ] 1x Unifi UAP-AC-Pro Wi-FI access point.
>
> - [x] 1x pfSense **2.5.2-RELEASE** (amd64) on PC Engines APU2
>
> - [x] 1x Netcomm NF18ACV router (GigaComm Supplied)
>
> - [x] 1x AdTran 212MHz Gfast bridge modem (GigaComm Supplied)
>
> - [x] 1x AWS EC2  t3.micro instance (https://aws.amazon.com/free/)
>



Early eject on tesing with the Unifi UAP-AC-Pro Wi-F because even though the brochure says 1.7Gbps of Bandwidth the AP is wired to the switch at 1Gbps and although it has a 5 GHz Radio and a channel width of VHT 80 the MacBook's Tx/Rx Rate is ~800 Mbps in my environment❌.

---

![](https://github.com/alexanderswift/public-gigacom/blob/main/pics/side-by-side-test.jpeg)



## So can we hit 1Gbps❓

Can a Unifi network with a pfSense firewall built on a low power AMD Embedded 1GHz quad Jaguar core achieve 1Gbps at layer 4, I'm sure I can switch traffic and route traffic at 1Gbps but can I match, inspect and forward (Firewalling) at 1Gbps❓. A quick reminder of the **[Paper Shop That Never Delivers Papers](https://en.wikipedia.org/wiki/OSI_model),** but the TL;DR version is just because your ISP has delivered a 1Gb service and your switch / router / network card says it's negotiated a layer 2 at that speed it doesn't mean you will see the nirvana of 1Gbps ⚠️.

#### IPerf3 testing on my local network to see if I could reach 1Gbps locally.

Starting at the bottom of the OSI stack, we know at layer1 the interfaces are all up at 1000baseT full-duplex so I ran an IPerf test from the AppleTV to MacBook looking to establish the max possible for the equipment I have thus starting with switching *NOT routing* between the TV and MacBook first.

#### iPerf3 tests:

**TEST1** - both are connected to the same UniFi 'switch 1' on the same vLAN so are communicating directly with each other. 

> ~~~
> me@MacBook Applications % ./iperf3 -c 192.168.40.70 -p 5201 -b 1000m
> Connecting to host 192.168.40.70, port 5201
> [  4] local 192.168.40.201 port 52060 connected to 192.168.40.70 port 5201
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-1.00   sec   103 MBytes   865 Mbits/sec
> [  4]   1.00-2.00   sec   112 MBytes   939 Mbits/sec
> [  4]   2.00-3.00   sec   112 MBytes   939 Mbits/sec
> [  4]   3.00-4.00   sec   112 MBytes   939 Mbits/sec
> [  4]   4.00-5.00   sec   112 MBytes   939 Mbits/sec
> [  4]   5.00-6.00   sec   112 MBytes   938 Mbits/sec
> [  4]   6.00-7.00   sec   111 MBytes   930 Mbits/sec
> [  4]   7.00-8.00   sec   112 MBytes   941 Mbits/sec
> [  4]   8.00-9.00   sec   112 MBytes   937 Mbits/sec
> [  4]   9.00-10.00  sec   112 MBytes   941 Mbits/sec
>
> - - - - - - - - - - - - - - - - - - - - - - - - -
>
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec  1.08 GBytes   931 Mbits/sec                  sender
> [  4]   0.00-10.00  sec  1.08 GBytes   930 Mbits/sec                  receiver
>
> iperf Done.
> ~~~



**TEST2** - both are connected to the GigaComm supplied NetComm router and is pretty much the same as test 1 but i've changed the hardware so it's hub / unmanaged switch.

> ~~~
> me@MacBook Applications % ./iperf3 -c 192.168.20.2 -p 5201 -b 1000m
> Connecting to host 192.168.20.2, port 5201
> [  4] local 192.168.20.5 port 52282 connected to 192.168.20.2 port 5201
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-1.00   sec   103 MBytes   862 Mbits/sec
> [  4]   1.00-2.00   sec   112 MBytes   941 Mbits/sec
> [  4]   2.00-3.00   sec   112 MBytes   941 Mbits/sec
> [  4]   3.00-4.00   sec   112 MBytes   941 Mbits/sec
> [  4]   4.00-5.00   sec   112 MBytes   941 Mbits/sec
> [  4]   5.00-6.00   sec   112 MBytes   941 Mbits/sec
> [  4]   6.00-7.00   sec   111 MBytes   932 Mbits/sec
> [  4]   7.00-8.00   sec   113 MBytes   951 Mbits/sec
> [  4]   8.00-9.00   sec   112 MBytes   941 Mbits/sec
> [  4]   9.00-10.00  sec   111 MBytes   933 Mbits/sec
>
> - - - - - - - - - - - - - - - - - - - - - - - - -
>
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec  1.09 GBytes   933 Mbits/sec                  sender
> [  4]   0.00-10.00  sec  1.08 GBytes   932 Mbits/sec                  receiver
>
> iperf Done.
> ~~~
>
>
>



**TEST3** - AppleTV connected to the same UniFi 'switch 1' and the MacBook connected to the same UniFi 'switch 2'. Just a baseline for test 4 and I moved the two devices 40m apart to see if the trunk between switches would make a difference. 

> ~~~
> me@MacBook Applications % ./iperf3 -c 192.168.40.70 -p 5201
> Connecting to host 192.168.40.70, port 5201
> [  4] local 192.168.40.201 port 52547 connected to 192.168.40.70 port 5201
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-1.00   sec   114 MBytes   954 Mbits/sec
> [  4]   1.00-2.00   sec   112 MBytes   939 Mbits/sec
> [  4]   2.00-3.00   sec   112 MBytes   939 Mbits/sec
> [  4]   3.00-4.00   sec   112 MBytes   939 Mbits/sec
> [  4]   4.00-5.00   sec   112 MBytes   939 Mbits/sec
> [  4]   5.00-6.00   sec   112 MBytes   938 Mbits/sec
> [  4]   6.00-7.00   sec   111 MBytes   930 Mbits/sec
> [  4]   7.00-8.00   sec   112 MBytes   941 Mbits/sec
> [  4]   8.00-9.00   sec   112 MBytes   937 Mbits/sec
> [  4]   9.00-10.00  sec   112 MBytes   941 Mbits/sec
>
> - - - - - - - - - - - - - - - - - - - - - - - - -
>
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec  1.09 GBytes   940 Mbits/sec                  sender
> [  4]   0.00-10.00  sec  1.09 GBytes   939 Mbits/sec                  receiver
>
> iperf Done.
> ~~~



**TEST4** - time to move one device onto another vLAN to see if theres a limit between the vLANS and for context my vLANS are setup on the pfSense firewall aka the default Gateway for each vLAN. 

> ~~~
> me@MacBook Applications % ./iperf3 -c 192.168.40.70 -p 5201
> Connecting to host 192.168.40.70, port 5201
> [  4] local 192.168.10.104 port 52588 connected to 192.168.40.70 port 5201
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-1.00   sec  46.6 MBytes   391 Mbits/sec
> [  4]   1.00-2.00   sec  44.9 MBytes   377 Mbits/sec
> [  4]   2.00-3.00   sec  44.8 MBytes   376 Mbits/sec
> [  4]   3.00-4.00   sec  44.6 MBytes   374 Mbits/sec
> [  4]   4.00-5.00   sec  45.1 MBytes   379 Mbits/sec
> [  4]   5.00-6.00   sec  43.7 MBytes   366 Mbits/sec
> [  4]   6.00-7.00   sec  44.2 MBytes   371 Mbits/sec
> [  4]   7.00-8.00   sec  43.2 MBytes   362 Mbits/sec
> [  4]   8.00-9.00   sec  44.1 MBytes   370 Mbits/sec
> [  4]   9.00-10.00  sec  44.4 MBytes   372 Mbits/sec
>
> - - - - - - - - - - - - - - - - - - - - - - - - -
>
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec   446 MBytes   374 Mbits/sec                  sender
> [  4]   0.00-10.00  sec   443 MBytes   372 Mbits/sec                  receiver
>
> iperf Done.
> ~~~



**TEST5** - the intra VLAN limit of the 1Gb trunk port was hit so I'm experimenting with the -P (parallel) to simultaneously test with 4 threads to see if the intel NICs in the APU2 and use more processing threads.. 

> ~~~
> alexs@Alexs-MacBook Downloads % iperf3 -c 192.168.40.102 -P 4      
> [ ID] Interval           Transfer     Bitrate
> [  5]   0.00-10.00  sec  68.6 MBytes  57.5 Mbits/sec                  sender
> [  5]   0.00-10.00  sec  68.0 MBytes  57.0 Mbits/sec                  receiver
> [  7]   0.00-10.00  sec   120 MBytes   101 Mbits/sec                  sender
> [  7]   0.00-10.00  sec   119 MBytes   100 Mbits/sec                  receiver
> [  9]   0.00-10.00  sec   317 MBytes   266 Mbits/sec                  sender
> [  9]   0.00-10.00  sec   315 MBytes   265 Mbits/sec                  receiver
> [ 11]   0.00-10.00  sec   437 MBytes   366 Mbits/sec                  sender
> [ 11]   0.00-10.00  sec   435 MBytes   365 Mbits/sec                  receiver
> [SUM]   0.00-10.00  sec   942 MBytes   790 Mbits/sec                  sender
> [SUM]   0.00-10.00  sec   938 MBytes   786 Mbits/sec                  receiver
>
> iperf Done.
> ~~~



#### Layer 2/3 iPerf3 testing summary 📈: 

When both hosts are in the same vlan the hosts boadcast and then communicated directly with each outher and the results show. 

✅ 940Mbps for switched and routed traffic and although this isn't 1000Mbps it is correct, more on that below. 

❌ 790 Mbps for multiple streams and as low as 370Mbps for a single stream when traffic is routed via the firewall. 

This doesn't mean I can't get 1Gbps from my Internet connection it means a single host with a few threads including the TCP overhead  used in my tests has a limit of about 940 Mbits/sec. 

~~~~
Here are some useful notes from others on tuning pfSense for 1Gbps and what was observed on pfSense/APU2 firewalls:
URL;S
- https://teklager.se/en/knowledge-base/apu2-1-gigabit-throughput-pfsense/
- https://teklager.se/en/pfsense-hardware/
- https://people.cs.clemson.edu/~westall/853/notes/pres05.pdf
- https://docs.netgate.com/pfsense/en/latest/hardware/tune.html
~~~~



## Internet Speed Test websites 🌏

Before we get into the GigaComm results here's a quick speed test from my iPhone on Telstra 5G at home, you can see why **it's my opinion that we need more from an Internet provider than "typical evening speeds", a reliable low latency connection is of greater value to me than typical evening speeds.** There's a silliness of having TPG FttB in an age of Gigabit but as you can see below mobile 5G latency is also why I didn't just use a 4G/5G modem, the low latency advantages of GigaComm mmWave are clear when you look at the latency differences.

| Host             | Ping (Latency) | Down   | Up    | URL                                           |
| ---------------- | -------------- | ------ | ----- | --------------------------------------------- |
| Telstra (Sydney) | **16ms**       | 946.96 | 85.67 | https://www.speedtest.net/result/i/4924116319 |

Using the GigaComm connection with speed test websites are ONLY an indication of your download speed because you've no idea what else is happening on the internet, it's a network you share with millions of other users in Australia.

##### All tests performed with a MacBook connected  ⚠️ DIRECTLY TO THE NTU ⚠️ AND I DO NOT RECOMMEND THIS ⚠️ 

| Host                                             | Ping (Latency) | Down       | Up         | URL                                                          |
| ------------------------------------------------ | -------------- | ---------- | ---------- | ------------------------------------------------------------ |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | 2ms            | 932.83Mbps | 98.36Mbps  | https://www.speedtest.net/result/12520801875                 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | 3ms            | 933.24Mbps | 98.82Mbps  | https://www.speedtest.net/result/12520804304                 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | 3ms            | 939.66Mbs  | 99.36Mbps  | https://www.speedtest.net/result/12520807098                 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | 3ms            | 936.41Mbps | 99.18Mbps  | https://www.speedtest.net/result/12520809756                 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | 2ms            | 935.34Mbps | 97.59Mbps  | https://www.speedtest.net/result/12520811933                 |
| Speedtest.net (selected Digital Pacific Sydney)  | 3ms            | 937.99Mbps | 100.11Mbps | https://www.speedtest.net/result/12509282802                 |
| TPG Speedtest Sydney                             | 3ms            | 930.8Mbps  | 100.2Mbps  | http://tpg.speedtestcustom.com/result/fe5e6de0-6452-11ec-b50d-5754f75e3cf4 |
| TPG Speedtest Sydney                             | 3ms            | 934.9Mbps  | 99.2Mbps   | http://tpg.speedtestcustom.com/result/80c0f700-66e0-11ec-90cc-bf087e229683 |
| TPG Speedtest Sydney                             | 2ms            | 940.4Mbps  | 99.9Mbps   | http://tpg.speedtestcustom.com/result/9c9cec40-66e0-11ec-90cc-bf087e229683 |
| TPG Speedtest Sydney                             | 2ms            | 917.8Mbps  | 99.8Mbps   | http://tpg.speedtestcustom.com/result/c08ff4d0-66e0-11ec-90cc-bf087e229683 |
| TPG Speedtest Sydney                             | 3ms            | 941.2Mbps  | 98.8Mbps   | http://tpg.speedtestcustom.com/result/f28913e0-66e0-11ec-90cc-bf087e229683 |
| TPG Speedtest Sydney                             | 3ms            | 934.0Mbps  | 99.2Mbps   | http://tpg.speedtestcustom.com/result/0ce4aab0-66e1-11ec-90cc-bf087e229683 |



All the below tests are using a MacBook connected to directly to each device mentioned, as the point of this is i'm creating a baseline and as I've said before Player 1's ISP/telco fundamentals have not been forgotten. When you are creating a baseline or even troubleshooting a network problem you should always breakdown the components and test (in this case) by moving the MacBook along the line starting with the NTU then the router then the firewall etc.

| Host                                             | Device                                                    | Ping (Latency) | Down       | UP        | SpeedTest URL                                |
| ------------------------------------------------ | --------------------------------------------------------- | -------------- | ---------- | --------- | -------------------------------------------- |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | APU2 pfSense firewall                                     | 2ms            | 572.72Mbps | 90.93Mbps | https://www.speedtest.net/result/12524797215 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | TEST FIREWALL dual NIC PC16GB RAM and 4Ghz CPU (pfSense)  | 1ms            | 896.28Mbps | 90.53Mbps | https://www.speedtest.net/result/12524854984 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | TEST FIREWALL dual NIC PC16GB RAM and 4Ghz CPU (opnSense) | 2ms            | 879.51Mbps | 90.75Mbps | https://www.speedtest.net/result/12525262017 |
| Speedtest.net (selected GigaComm Pty Ltd Sydney) | GigaComm Supplied Router                                  | 2ms            | 825.25Mbps | 97.83Mbps | https://www.speedtest.net/result/12524820479 |

### Testing with Cloudflare ☁️: 

All the below tests are using a MacBook connected to my Unifi network directly to a the device  mentioned and while the test results are simular final numbers if you look closely you can see once again if you push the APU2 pfSense firewall with a higher number of smaller packets the speed drops by 2/3rd's. 

- [x]  APU2 pfSense firewall - [result](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-AP2-Firewall.png ).  
- [x] DIRECT TO NTU - [result](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-Direct-To-NTU.png).  
- [x] TEST FIREWALL (pfSense) - [result](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-TestFirewall.png). 
- [x] TEST FIREWALL opnfSense) - [result](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-TestFirewallOPNSense.png).  
- [x] GigaComm Supplied Router - [result](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-GigaCommRouter.png). 

-----

##### Summary: 

The MacBook can deliver about 940Mbps for switched and routed traffic and although this isn't 1000Mbps / 1Gbps it is correct and it doesn't mean I can't get 1Gbps from my Internet connection it means a single host with a MTU of 1500 commanding four to ten threads including frame and IP overheads equals 1Gbps, I'll try expanding on this in the chasing 1Gbps below.

I hope why you can see I stated internet speed test websites are an indication ONLY of your download speed. The takeaway for me is looking at the Cloudflare tests in detail because they show you a breakdown of your results by size of the payload (Data) and (I believe) give you a weighted max speed vs an overall max speed of speedtest.net and you can see a bit of this during speedtest.net tests as the dial makes it's way to the top speed. 



🍿🕑 You should ignore the headline download speeds and look at all the above tests on Cloudflare focuing on the size of the orange bars because the further to the right (note the graph lables are scalled) and a more condensed bar indicates a consistent performance and speed overall.



💸 However it does show I need to try tune or replace the APU2 pfSense firewall because it looks like it's hitting limits as described by TekLager in their artical '[How to fine-tune pfSense for 1Gbit throughput on APU2](https://teklager.se/en/knowledge-base/apu2-1-gigabit-throughput-pfsense/)' and ''[what hardware to buy for pfSense router in 2021](https://teklager.se/en/pfsense-hardware/)' I look to be hitting the single connection performance limits.





## Chasing 1Gbps 🏃‍♂️.  

All the below tests are using a MacBook connected to my Unifi network directly to a device mentioned in the column "Device".

### AWS - Chasing 1Gb and I think we're going to need a bigger boat🦈;

So before I rush out and buy a bigger **~~boat~~** firewall I wanted to test a few things with a host I know is capable thus I deployed an Amazon Web Services EC2 t3.micro (1GiB) instance with up to 5 Gigabits of network performed to test my pfSense firewall the -s (server) mode and AWS the -c  (client) and then vice-versa. 

**TEST1** - EC2 as the -s (server) to test upload from the APU2 firewall.

> ~~~
> [ec2-user@ip-172-31-9-209 ~]$ iperf3 -s
> -----------------------------------------------------------
> Server listening on 5201
> -----------------------------------------------------------
> Accepted connection from x.x.x.x, port 58198
> [  5] local 172.31.9.209 port 5201 connected to x.x.x.x port 12555
> [ ID] Interval           Transfer     Bandwidth
> [  5]   0.00-1.00   sec   824 KBytes  6.75 Mbits/sec                  
> [  5]   1.00-2.00   sec  4.82 MBytes  40.4 Mbits/sec                  
> [  5]   2.00-3.00   sec  8.97 MBytes  74.9 Mbits/sec                  
> [  5]   3.00-4.00   sec  11.5 MBytes  96.9 Mbits/sec                  
> [  5]   4.00-5.00   sec  11.4 MBytes  95.3 Mbits/sec                  
> [  5]   5.00-6.00   sec  10.9 MBytes  91.7 Mbits/sec                  
> [  5]   6.00-7.00   sec  10.8 MBytes  90.6 Mbits/sec                  
> [  5]   7.00-8.00   sec  8.29 MBytes  69.6 Mbits/sec                  
> [  5]   8.00-9.00   sec  1.56 MBytes  13.1 Mbits/sec                  
> [  5]   9.00-10.00  sec  76.4 KBytes  626 Kbits/sec                  
> [  5]  10.00-10.90  sec  73.5 KBytes  667 Kbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [ ID] Interval           Transfer     Bandwidth
> [  5]   0.00-10.90  sec  0.00 Bytes  0.00 bits/sec                  sender
> [  5]   0.00-10.90  sec  69.2 MBytes  53.2 Mbits/sec                  receiver
> -----------------------------------------------------------
> Server listening on 5201
> -----------------------------------------------------------
> ~~~



**TEST2** - EC2 as the -c (client)  to test download to the APU2 firewall.

> ~~~~
> [ec2-user@ip-172-31-9-209 ~]$ iperf3 -c x.x.x.x -P 10 -d -t 60
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [ ID] Interval           Transfer     Bandwidth       Retr
> [  4]   0.00-60.00  sec   608 MBytes  85.1 Mbits/sec  1408             sender
> [  4]   0.00-60.00  sec   608 MBytes  85.0 Mbits/sec                  receiver
> [  6]   0.00-60.00  sec   476 MBytes  66.6 Mbits/sec  823             sender
> [  6]   0.00-60.00  sec   476 MBytes  66.5 Mbits/sec                  receiver
> [  8]   0.00-60.00  sec   458 MBytes  64.0 Mbits/sec  954             sender
> [  8]   0.00-60.00  sec   457 MBytes  63.9 Mbits/sec                  receiver
> [ 10]   0.00-60.00  sec   391 MBytes  54.7 Mbits/sec  1175             sender
> [ 10]   0.00-60.00  sec   391 MBytes  54.6 Mbits/sec                  receiver
> [ 12]   0.00-60.00  sec   445 MBytes  62.3 Mbits/sec  1240             sender
> [ 12]   0.00-60.00  sec   445 MBytes  62.2 Mbits/sec                  receiver
> [ 14]   0.00-60.00  sec   537 MBytes  75.1 Mbits/sec  1481             sender
> [ 14]   0.00-60.00  sec   537 MBytes  75.0 Mbits/sec                  receiver
> [ 16]   0.00-60.00  sec   560 MBytes  78.4 Mbits/sec  1519             sender
> [ 16]   0.00-60.00  sec   560 MBytes  78.3 Mbits/sec                  receiver
> [ 18]   0.00-60.00  sec   902 MBytes   126 Mbits/sec  2327             sender
> [ 18]   0.00-60.00  sec   902 MBytes   126 Mbits/sec                  receiver
> [ 20]   0.00-60.00  sec   744 MBytes   104 Mbits/sec  2670             sender
> [ 20]   0.00-60.00  sec   743 MBytes   104 Mbits/sec                  receiver
> [ 22]   0.00-60.00  sec   849 MBytes   119 Mbits/sec  2423             sender
> [ 22]   0.00-60.00  sec   848 MBytes   119 Mbits/sec                  receiver
> [SUM]   0.00-60.00  sec  5.83 GBytes   835 Mbits/sec  16020             sender
> [SUM]   0.00-60.00  sec  5.83 GBytes   834 Mbits/sec                  receiver
>
> iperf Done.
> ~~~~
>



![](https://github.com/alexanderswift/public-gigacom/blob/main/pics/aws-to-ap2-firewall-iperf.png)



**TEST3** - EC2 as the -c (client)  to test download to the APU2 firewall but this time **I switched to UDP** to see what is possible without the TCP handshake. .

~~~
[ec2-user@ip-172-31-47-176 ~]$ iperf3 -c x.x.x.x -P 5  -u -i 1 -d -b 250M -t 120
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Jitter    Lost/Total Datagrams
[  4]   0.00-120.00 sec  3.49 GBytes   250 Mbits/sec  0.033 ms  631827/2588270 (24%)  
[  4] Sent 2588270 datagrams
[  6]   0.00-120.00 sec  3.49 GBytes   250 Mbits/sec  0.046 ms  631132/2588264 (24%)  
[  6] Sent 2588264 datagrams
[  8]   0.00-120.00 sec  3.49 GBytes   250 Mbits/sec  0.043 ms  637851/2588269 (25%)  
[  8] Sent 2588269 datagrams
[ 10]   0.00-120.00 sec  3.49 GBytes   250 Mbits/sec  0.050 ms  634072/2588270 (24%)  
[ 10] Sent 2588270 datagrams
[ 12]   0.00-120.00 sec  3.49 GBytes   250 Mbits/sec  0.045 ms  631607/2588265 (24%)  
[ 12] Sent 2588265 datagrams
[SUM]   0.00-120.00 sec  17.5 GBytes  1.25 Gbits/sec  0.043 ms  3166489/12941338 (24%)  

iperf Done.
[ec2-user@ip-172-31-47-176 ~]$ 
~~~



![](https://github.com/alexanderswift/public-gigacom/blob/main/pics/EC2-to-firewall-UDP.png)



##### Summary: 

What I observed is by turning up the iPerf testing to 1Gbps then 1.25Gbps and switching to UDP I was starting to reach a diminishing return as the devices started to queue and/or discard frames thus leading to a slower 835Mbps. 

```
 iperf3 -c x.x.x.x -P 5 -u -i 1 -d -b 250M -t 120
```



##### Overheads using a the Beer Truck Analogy, 1 slab = 1 byte.

The truck has a capacity of 1500 slabs of beer but you deduct bottles to make way for necessary items like fuel, engine, lashing and a consignment note etc they all add up in most cases to about 60 slabs for TCP and 48 slabs for UPD and these are "encapsulated" into the payload thus subtracting from the capacity THEN we have a Frame size of 46 bytes added as overheads 🤷‍♂️. 

~~~ 
Parent interface MTU: 1500 
  Header size (overhead):** 58 bytes 
  MTU: 1442 bytes
  --
  IPv4 (20 bytes) 
  Ethernet (14 bytes) + 802.1q VLAN (4 bytes)
  TCP (20 byte)

Parent interface MTU: 9000 🐘
	Header size (overhead):** 58 bytes 
  MTU: 8942 bytes
  -- 
  IPv4 (20 bytes) 
  Ethernet (14 bytes) + 802.1q VLAN (4 bytes)
  TCP (20 byte)

 Note UDP would be 8 bytes
~~~

What about JumboFrames 🐘 then, the obvious benefit is the extra 7500 slabs on the Beer Truck but it's like real trucking, if the truck is too big, a good comparison would be a road train vs a ute there's places a road tain just cannot go. i've tried a local test with equipment lifting the MTU from 1500 to 9000 for all the devices I can administer but for JumboFrames implementation to be successful **ALL** the devices (ntu, router, firewall, switch, iPerf client & server) must be configured with the MTU of 9000 and because some of these devices are AppleTV's and GigaComm supplied etc this would  slow things down as one device sends Jumbo Frames and the other device has to send a message back asking for smaller ~~Beer Trucks~~ frames on the wire. 



## Final Thoughts 🤔



What started with was TL;DR (and thank you for reading my ramblings) was <u>*"it's a low latency gigabit fast and reliable service and IMHO it's a technology approach the NBN could have used for apartment complexes from the very beginning 🍿"*</u> 

All along i've wondered how are GigaComm decreasing the **Distance** and increase the frequency (**Time**) to deliver the **Speed** and because theres no discussion of a NTU during the sales process (that I could remember or point too) this is IMHO why there was some early GigaComm scepticism🤷‍♂️ and i've written back to GigaComm to say thank you for the support to get me online but if they had just said on their site <u>***we use mmWave to connect your building to us and inside you building Gfast and FttDP I would have signed up in half the time.***</u>. 



Anyway thank you for the addtional Mhz on the wire I guess. 



Re the APU2 firewall, I think we're going to need a bigger boat🦈 while the APU2 based firewall has provided outstanding reliability, performance and a great features per dollar ratio while having the benifit of being a low power device it looks like it's got a limits once it's in position in my network. Going back to the Cloudflare tests ocuing on the size of the orange bars because the further to the right (note the graph lables are scalled) and a more condensed bar indicates a consistent performance and  overall speed.

[APU2 Firewall](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-AP2-Firewall.png) Vs an [i7 multi-core Firewall](https://github.com/alexanderswift/public-gigacom/blob/main/pics/CF-AP2-Firewall.png) the latter does better across all measurements from 100kB to 100MB.

I thought about trying to bond two interfaces from the Firewall to the Switch to try improve the bandwidth between the firewall and switch for two reasons. 

1) The way pfSense handles frames (ver 2.5+) is to spread frames over the processors on the Intel NICs (a reason why you should use Intel NICs for this type of build) but it takes some offloading to the main CPU of the firewall and this is where you start to hit limits IMHO. 
2) More ports = more bandwidth right(?) but my options are to use LAG (link-aggregation) and while that would help with bandwidth for multiple devices the algorithm used in this implementation of LAG uses the senders and receivers HWaddress to decide on the physical media to send the Ethernet frames via a link thus isn't going to increase speed for a single device,  looks like an upgrade (will start saving now) for some 10G over RJ45 ethernet interfaces to take full advantage of a consistent performance and overall speed.



## TBC....





#### TPG connection tests run at the same time 🐢

Steedy test not really for comparison but proved to me that vDSL and Gfast on the same 4core cable doesn't interfere. 

~~~ 
Host: www.speedtest.net
0) https://www.speedtest.net/result/12505837863
1) https://www.speedtest.net/result/12505887301
2) https://www.speedtest.net/result/12505889645
3) https://www.speedtest.net/result/12505892027

Host: tpg.speedtestcustom.com
0) http://tpg.speedtestcustom.com/result/1a41b560-63bf-11ec-8bed-9336fa9df5d4
1) http://tpg.speedtestcustom.com/result/293d6490-63c1-11ec-8bed-9336fa9df5d4
2) http://tpg.speedtestcustom.com/result/489253f0-63c1-11ec-8bed-9336fa9df5d4
3) http://tpg.speedtestcustom.com/result/63e08820-63c1-11ec-8bed-9336fa9df5d4
~~~
