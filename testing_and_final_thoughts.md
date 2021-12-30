# Test and final thoughts 🧪& 🤔


### Why test❓

Over a a few rainy days in late December 2021 I decided to create a baseline of the new service with the default configuration and a single device and write them down (how these documents started) . The reason for baselining my local network is so I understand the limits of my equipment before making judgements on the new internet provider, it's easy to measure how you are going if you know from where you came. I've invested in [Ubiquiti unifi](https://www.ui.com) Wi-FI / PoE switches and a BYO [pfSense](https://www.pfsense.org/download/) firewall built on [PC Engines APU2](https://www.pcengines.ch/apu2.htm) hardware and for the previous 100/40Mbs internet it has provided outstanding reliability, performance and a great features per dollar ratio while having the benifit of all being low power devices because utility rates here in Australia is some of the most expensive in the world.




> ~~~
> Electricity Usage Per Year = (Watts / 1000) * Hours/Day * Days/Week * Weeks/Year = kWh/year
>
> Electricity Cost Per Year = kWh/year * (cents/kWh / 100) = $/year
> ~~~



The combined power total of all my equipment is less than 20watts / 0.5amp of power at an estimated $45pa and including the purchase cost has cost an estimated AU$850 over the past four years. It's was very tempting to take the approach of shopping Grays / eBay for old Enterprise equipment that was once tens of thousands of dollars but IMHO you could 20x that power bill then you have to deal with the additional noise, heat and it risk failing the PAT (partner acceptance test) so I went the way I did.

### Devices for testing:

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
>   

### So can we hit 1Gbps❓

Can a Unifi network with a pfSense firewall built on a low power AMD Embedded 1GHz quad Jaguar core achieve 1Gbps at layer 4, I'm sure I can switch traffic and route traffic and 1Gbps but can I match, inspect and forward (Firewalling) at 1Gbps. A quick reminder of the **[Paper Shop That Never Delivers Papers](https://en.wikipedia.org/wiki/OSI_model),** but the TL;DR version is just because your ISP has delivered a 1Gb service and the switch / router / network card says it's negotiated a layer 2 that speed it doesn't mean you will see the nirvana of 1Gbps ⚠️.

Early eject on tesing with the Unifi UAP-AC-Pro Wi-F because even though the brochure says 1.7Gbps of Bandwidth the AP is wired to the switch at 1Gbps and although it has a 5 GHz Radio and a channel width of VHT 80 the MacBook's Tx/Rx Rate is ~800 Mbps in my environment❌.

Here's some useful notes from others on tuning for 1Gbps and what was observed on pfSense/APU2 firewalls:

~~~~
URL;S
- https://teklager.se/en/knowledge-base/apu2-1-gigabit-throughput-pfsense/
- https://teklager.se/en/pfsense-hardware/
- https://people.cs.clemson.edu/~westall/853/notes/pres05.pdf
- https://docs.netgate.com/pfsense/en/latest/hardware/tune.html
~~~~



### IPerf3 testing on my local network to see if I could reach 1Gbps locally.

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



**TEST5** - intra VLAN limit of the 1Gb trunk port hit so I'm experimenting with the -P (parallel) to simultaneously test with 4 threads to see if the intel NICs in the APU2 and use more processing threads.. 

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

When both hosts are in the same vlan the hosts boadcast and then communicated directly with each outher and the results show 930 Mbits/sec switched and when I route via the firewall using multiple threads the max is about 790 Mbits/sec. It looks like my devices have some limits and TCP overhead  (****  ADD UDP TEST6****) 

That doesn't mean I can't get 1Gbps from my connection it means a single host with a a few threads and TCP used in my tests has  limits. 



Internet Speed Tests sites

These sites are an indication of your download speed but you've no idea 

### **From TPG**

Host: speedtest.net (selected GigaComm Pty Ltd Host a server)

0) https://www.speedtest.net/result/12509282802
1) https://www.speedtest.net/result/12505837863
2) https://www.speedtest.net/result/12505887301
3) https://www.speedtest.net/result/12505889645
4) https://www.speedtest.net/result/12505892027


Host: tpg.speedtestcustom.com

0) http://tpg.speedtestcustom.com/result/fe5e6de0-6452-11ec-b50d-5754f75e3cf4
1) http://tpg.speedtestcustom.com/result/1a41b560-63bf-11ec-8bed-9336fa9df5d4
2) http://tpg.speedtestcustom.com/result/293d6490-63c1-11ec-8bed-9336fa9df5d4
3) http://tpg.speedtestcustom.com/result/489253f0-63c1-11ec-8bed-9336fa9df5d4
4) http://tpg.speedtestcustom.com/result/63e08820-63c1-11ec-8bed-9336fa9df5d4

### **From GigaComm**

Host: speedtest.net (selected GigaComm Pty Ltd Host a server)

0) https://www.speedtest.net/result/12520801875
1) https://www.speedtest.net/result/12520804304
2) https://www.speedtest.net/result/12520807098
3) https://www.speedtest.net/result/12520809756
4) https://www.speedtest.net/result/12520811933

Host: tpg.speedtestcustom.com


0) http://tpg.speedtestcustom.com/result/80c0f700-66e0-11ec-90cc-bf087e229683
1) http://tpg.speedtestcustom.com/result/9c9cec40-66e0-11ec-90cc-bf087e229683
2) http://tpg.speedtestcustom.com/result/c08ff4d0-66e0-11ec-90cc-bf087e229683
3) http://tpg.speedtestcustom.com/result/f28913e0-66e0-11ec-90cc-bf087e229683
4) http://tpg.speedtestcustom.com/result/0ce4aab0-66e1-11ec-90cc-bf087e229683



Chasing 1Gbps.  

All using a MacBook

0) https://www.speedtest.net/result/12524797215 APU2 pfSense firewall
1) https://www.speedtest.net/result/12524842243 DIRECT TO NTU
2) https://www.speedtest.net/result/12524854984 TEST FIREWALL (pfSense)
3) https://www.speedtest.net/result/12524820479 GigaComm Supplied Router
4) https://www.speedtest.net/result/12525262017 TEST FIREWALL (opnSense)











### AWS - Chasing 1Gb and we're going to need a bigger boat🦈;



**TEST1** - intra VLAN limit of the 1Gb trunk port hit.

> ~~~
> [ec2-user@ip-172-31-9-209 ~]$ iperf3 -s
> -----------------------------------------------------------
> Server listening on 5201
> -----------------------------------------------------------
> Accepted connection from 103.138.245.113, port 58198
> [  5] local 172.31.9.209 port 5201 connected to 103.138.245.113 port 12555
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



**TEST5** - intra VLAN limit of the 1Gb trunk port hit.

> ~~~~
> [ec2-user@ip-172-31-9-209 ~]$ iperf3 -c 103.138.245.113 -P 10 -d -t 60
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
>





OTHER

https://adtran.com/web/page/portal/Adtran/group/4504  
