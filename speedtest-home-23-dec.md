

# A scratch of the test results



Taken over a few days in December 2021 after the Installation on a new internet connection. 

### IPerf3 testing on my local network to see if I could reach 1Gbps locally. 

IPerf test from the AppleTV to MacBook looking to establish the max possible for the equipment I have thus starting with switching *NOT routing* between the two first.


**TEST1** both are connected to the same UniFi 'switch 1'.

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
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec  1.08 GBytes   931 Mbits/sec                  sender
> [  4]   0.00-10.00  sec  1.08 GBytes   930 Mbits/sec                  receiver
>
> iperf Done.
>



**TEST2** both are connected to the GigaComm supplied NetComm router

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
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec  1.09 GBytes   933 Mbits/sec                  sender
> [  4]   0.00-10.00  sec  1.08 GBytes   932 Mbits/sec                  receiver
>
> iperf Done.
>

**TEST3** AppleTV connected to the same UniFi 'switch 1' and the MacBook connected to the same UniFi 'switch 2'. (just a baseline for test 4)

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
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec  1.09 GBytes   940 Mbits/sec                  sender
> [  4]   0.00-10.00  sec  1.09 GBytes   939 Mbits/sec                  receiver
>
> iperf Done.
>

**TEST4** - intra VLAN limit of the 1Gb trunk port hit.

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
> [ ID] Interval           Transfer     Bandwidth
> [  4]   0.00-10.00  sec   446 MBytes   374 Mbits/sec                  sender
> [  4]   0.00-10.00  sec   443 MBytes   372 Mbits/sec                  receiver
>
> iperf Done.



**TEST5** - intra VLAN limit of the 1Gb trunk port hit.

- - - - - - - - - - - - - - - - - - - - - - - -



> alexs@Alexs-MacBook Downloads % iperf3 -c 192.168.40.102 -P 4      
> Connecting to host 192.168.40.102, port 5201
> [  5] local 192.168.10.103 port 51481 connected to 192.168.40.102 port 5201
> [  7] local 192.168.10.103 port 51482 connected to 192.168.40.102 port 5201
> [  9] local 192.168.10.103 port 51483 connected to 192.168.40.102 port 5201
> [ 11] local 192.168.10.103 port 51484 connected to 192.168.40.102 port 5201
> [ ID] Interval           Transfer     Bitrate
> [  5]   0.00-1.00   sec  5.89 MBytes  49.4 Mbits/sec                  
> [  7]   0.00-1.00   sec  14.8 MBytes   124 Mbits/sec                  
> [  9]   0.00-1.00   sec  18.8 MBytes   158 Mbits/sec                  
> [ 11]   0.00-1.00   sec  43.4 MBytes   364 Mbits/sec                  
> [SUM]   0.00-1.00   sec  82.9 MBytes   695 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   1.00-2.00   sec  2.94 MBytes  24.7 Mbits/sec                  
> [  7]   1.00-2.00   sec  2.85 MBytes  23.9 Mbits/sec                  
> [  9]   1.00-2.00   sec  36.4 MBytes   306 Mbits/sec                  
> [ 11]   1.00-2.00   sec  48.3 MBytes   405 Mbits/sec                  
> [SUM]   1.00-2.00   sec  90.5 MBytes   759 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   2.00-3.00   sec  4.41 MBytes  37.0 Mbits/sec                  
> [  7]   2.00-3.00   sec  5.56 MBytes  46.6 Mbits/sec                  
> [  9]   2.00-3.00   sec  35.0 MBytes   293 Mbits/sec                  
> [ 11]   2.00-3.00   sec  46.5 MBytes   390 Mbits/sec                  
> [SUM]   2.00-3.00   sec  91.5 MBytes   768 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   3.00-4.00   sec  5.53 MBytes  46.4 Mbits/sec                  
> [  7]   3.00-4.00   sec  7.89 MBytes  66.2 Mbits/sec                  
> [  9]   3.00-4.00   sec  34.2 MBytes   287 Mbits/sec                  
> [ 11]   3.00-4.00   sec  45.6 MBytes   382 Mbits/sec                  
> [SUM]   3.00-4.00   sec  93.2 MBytes   782 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   4.00-5.00   sec  6.39 MBytes  53.6 Mbits/sec                  
> [  7]   4.00-5.00   sec  9.74 MBytes  81.7 Mbits/sec                  
> [  9]   4.00-5.00   sec  33.5 MBytes   281 Mbits/sec                  
> [ 11]   4.00-5.00   sec  44.4 MBytes   373 Mbits/sec                  
> [SUM]   4.00-5.00   sec  94.1 MBytes   789 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   5.00-6.00   sec  7.20 MBytes  60.4 Mbits/sec                  
> [  7]   5.00-6.00   sec  11.6 MBytes  97.1 Mbits/sec                  
> [  9]   5.00-6.00   sec  32.8 MBytes   275 Mbits/sec                  
> [ 11]   5.00-6.00   sec  43.7 MBytes   367 Mbits/sec                  
> [SUM]   5.00-6.00   sec  95.3 MBytes   800 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   6.00-7.00   sec  7.88 MBytes  66.1 Mbits/sec                  
> [  7]   6.00-7.00   sec  13.4 MBytes   113 Mbits/sec                  
> [  9]   6.00-7.00   sec  32.5 MBytes   273 Mbits/sec                  
> [ 11]   6.00-7.00   sec  42.9 MBytes   360 Mbits/sec                  
> [SUM]   6.00-7.00   sec  96.7 MBytes   811 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   7.00-8.00   sec  8.31 MBytes  69.7 Mbits/sec                  
> [  7]   7.00-8.00   sec  14.7 MBytes   123 Mbits/sec                  
> [  9]   7.00-8.00   sec  32.0 MBytes   269 Mbits/sec                  
> [ 11]   7.00-8.00   sec  42.3 MBytes   355 Mbits/sec                  
> [SUM]   7.00-8.00   sec  97.3 MBytes   817 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   8.00-9.00   sec  9.62 MBytes  80.7 Mbits/sec                  
> [  7]   8.00-9.00   sec  18.4 MBytes   155 Mbits/sec                  
> [  9]   8.00-9.00   sec  31.0 MBytes   260 Mbits/sec                  
> [ 11]   8.00-9.00   sec  40.1 MBytes   336 Mbits/sec                  
> [SUM]   8.00-9.00   sec  99.1 MBytes   832 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [  5]   9.00-10.00  sec  10.4 MBytes  87.2 Mbits/sec                  
> [  7]   9.00-10.00  sec  21.1 MBytes   177 Mbits/sec                  
> [  9]   9.00-10.00  sec  30.4 MBytes   255 Mbits/sec                  
> [ 11]   9.00-10.00  sec  39.6 MBytes   332 Mbits/sec                  
> [SUM]   9.00-10.00  sec   101 MBytes   851 Mbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
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



Chasing 1Gbps 

All using a MacBook 

0) https://www.speedtest.net/result/12524797215 APU2 pfSense firewall
1) https://www.speedtest.net/result/12524842243 DIRECT TO NTU 
2) https://www.speedtest.net/result/12524854984 TEST FIREWALL (pfSense)
3) https://www.speedtest.net/result/12524820479 GigaComm Supplied Router
4) https://www.speedtest.net/result/12525262017 TEST FIREWALL (opnSense)





https://adtran.com/web/page/portal/Adtran/group/4504 

https://teklager.se/en/knowledge-base/apu2-1-gigabit-throughput-pfsense/ 

https://teklager.se/en/pfsense-hardware/

https://protectli.com/about/ 

https://people.cs.clemson.edu/~westall/853/notes/pres05.pdf

https://docs.netgate.com/pfsense/en/latest/hardware/tune.html 





AWS 



**TEST5** - intra VLAN limit of the 1Gb trunk port hit.



> nb;lm
>
> ec2-user@ip-172-31-9-209 ~]$ iperf3 -s 
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
> [  5]   9.00-10.00  sec  76.4 KBytes   626 Kbits/sec                  
> [  5]  10.00-10.90  sec  73.5 KBytes   667 Kbits/sec                  
> - - - - - - - - - - - - - - - - - - - - - - - - -
> [ ID] Interval           Transfer     Bandwidth
> [  5]   0.00-10.90  sec  0.00 Bytes  0.00 bits/sec                  sender
> [  5]   0.00-10.90  sec  69.2 MBytes  53.2 Mbits/sec                  receiver
> -----------------------------------------------------------
> Server listening on 5201
> -----------------------------------------------------------



**TEST5** - intra VLAN limit of the 1Gb trunk port hit.



> hhh
>
> [ec2-user@ip-172-31-9-209 ~]$ iperf3 -c 103.138.245.113 -P 10 -d -t 60
>
> ~~~~
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
