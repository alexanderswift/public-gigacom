**From TPG**
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

**From GigaComm**
0) https://www.speedtest.net/result/12520801875
1) https://www.speedtest.net/result/12520804304
2) https://www.speedtest.net/result/12520807098
3) https://www.speedtest.net/result/12520809756
4) https://www.speedtest.net/result/12520811933


0) http://tpg.speedtestcustom.com/result/80c0f700-66e0-11ec-90cc-bf087e229683
1) http://tpg.speedtestcustom.com/result/9c9cec40-66e0-11ec-90cc-bf087e229683
2) http://tpg.speedtestcustom.com/result/c08ff4d0-66e0-11ec-90cc-bf087e229683
3) http://tpg.speedtestcustom.com/result/f28913e0-66e0-11ec-90cc-bf087e229683
4) http://tpg.speedtestcustom.com/result/0ce4aab0-66e1-11ec-90cc-bf087e229683





IPerf test from the AppleTV to MacBook looking to establish the max possible for the equipment I have thus starting with switching *NOT routing* between the two first.
- TEST1 both are connected to the same UniFi 'switch 1'.
- TEST2 both are connected to the GigaComm supplied NetComm router
- TEST3 AppleTV connected to the same UniFi 'switch 1' and the MacBook connected to the same UniFi 'switch 2'. (just a baseline for test 4)
- TEST4 Connected as per TEST3 but I moved the MacBook to another VLAN to route between the two.

TEST1
me@MacBook Applications % ./iperf3 -c 192.168.40.70 -p 5201 -b 1000m
Connecting to host 192.168.40.70, port 5201
[  4] local 192.168.40.201 port 52060 connected to 192.168.40.70 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec   103 MBytes   865 Mbits/sec
[  4]   1.00-2.00   sec   112 MBytes   939 Mbits/sec
[  4]   2.00-3.00   sec   112 MBytes   939 Mbits/sec
[  4]   3.00-4.00   sec   112 MBytes   939 Mbits/sec
[  4]   4.00-5.00   sec   112 MBytes   939 Mbits/sec
[  4]   5.00-6.00   sec   112 MBytes   938 Mbits/sec
[  4]   6.00-7.00   sec   111 MBytes   930 Mbits/sec
[  4]   7.00-8.00   sec   112 MBytes   941 Mbits/sec
[  4]   8.00-9.00   sec   112 MBytes   937 Mbits/sec
[  4]   9.00-10.00  sec   112 MBytes   941 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  1.08 GBytes   931 Mbits/sec                  sender
[  4]   0.00-10.00  sec  1.08 GBytes   930 Mbits/sec                  receiver

iperf Done.

TEST2
me@MacBook Applications % ./iperf3 -c 192.168.20.2 -p 5201 -b 1000m
Connecting to host 192.168.20.2, port 5201
[  4] local 192.168.20.5 port 52282 connected to 192.168.20.2 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec   103 MBytes   862 Mbits/sec
[  4]   1.00-2.00   sec   112 MBytes   941 Mbits/sec
[  4]   2.00-3.00   sec   112 MBytes   941 Mbits/sec
[  4]   3.00-4.00   sec   112 MBytes   941 Mbits/sec
[  4]   4.00-5.00   sec   112 MBytes   941 Mbits/sec
[  4]   5.00-6.00   sec   112 MBytes   941 Mbits/sec
[  4]   6.00-7.00   sec   111 MBytes   932 Mbits/sec
[  4]   7.00-8.00   sec   113 MBytes   951 Mbits/sec
[  4]   8.00-9.00   sec   112 MBytes   941 Mbits/sec
[  4]   9.00-10.00  sec   111 MBytes   933 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  1.09 GBytes   933 Mbits/sec                  sender
[  4]   0.00-10.00  sec  1.08 GBytes   932 Mbits/sec                  receiver

iperf Done.


TEST3
me@MacBook Applications % ./iperf3 -c 192.168.40.70 -p 5201
Connecting to host 192.168.40.70, port 5201
[  4] local 192.168.40.201 port 52547 connected to 192.168.40.70 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec   114 MBytes   954 Mbits/sec
[  4]   1.00-2.00   sec   112 MBytes   939 Mbits/sec
[  4]   2.00-3.00   sec   112 MBytes   939 Mbits/sec
[  4]   3.00-4.00   sec   112 MBytes   939 Mbits/sec
[  4]   4.00-5.00   sec   112 MBytes   939 Mbits/sec
[  4]   5.00-6.00   sec   112 MBytes   938 Mbits/sec
[  4]   6.00-7.00   sec   111 MBytes   930 Mbits/sec
[  4]   7.00-8.00   sec   112 MBytes   941 Mbits/sec
[  4]   8.00-9.00   sec   112 MBytes   937 Mbits/sec
[  4]   9.00-10.00  sec   112 MBytes   941 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  1.09 GBytes   940 Mbits/sec                  sender
[  4]   0.00-10.00  sec  1.09 GBytes   939 Mbits/sec                  receiver

iperf Done.

TEST4 - intra VLAN limit of the 1Gb trunk port hit.

me@MacBook Applications % ./iperf3 -c 192.168.40.70 -p 5201
Connecting to host 192.168.40.70, port 5201
[  4] local 192.168.10.104 port 52588 connected to 192.168.40.70 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  46.6 MBytes   391 Mbits/sec
[  4]   1.00-2.00   sec  44.9 MBytes   377 Mbits/sec
[  4]   2.00-3.00   sec  44.8 MBytes   376 Mbits/sec
[  4]   3.00-4.00   sec  44.6 MBytes   374 Mbits/sec
[  4]   4.00-5.00   sec  45.1 MBytes   379 Mbits/sec
[  4]   5.00-6.00   sec  43.7 MBytes   366 Mbits/sec
[  4]   6.00-7.00   sec  44.2 MBytes   371 Mbits/sec
[  4]   7.00-8.00   sec  43.2 MBytes   362 Mbits/sec
[  4]   8.00-9.00   sec  44.1 MBytes   370 Mbits/sec
[  4]   9.00-10.00  sec  44.4 MBytes   372 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec   446 MBytes   374 Mbits/sec                  sender
[  4]   0.00-10.00  sec   443 MBytes   372 Mbits/sec                  receiver

iperf Done.
