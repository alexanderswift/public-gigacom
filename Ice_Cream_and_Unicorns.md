ISP promised and delivers Gigabit over single-pair copper!

Yes, I was sceptical of the claims too but TL;DR. It's Gigabit fast, reliable and IMHO it's a technology approach the NBN could have used for FTTB apartment complexes from the beginning.

Who is player 1?

An enthusiast level rusty ex-ISP network engineer and ~15 years ago I stopped cat herding for an ISP/telco and started herding cats a public cloud company because they said 'we are fanatical about support', so yes average customer support gets my back up, but anyway those ISP/telco fundamentals of **💩 in 💩 out**, the **beer truck analogy** and **internet speed = distance/time (frequency )** has not been forgotten.

Previous ISP:

  Used TPG's FttB (since the pre NBN days) with vDSL syncing at 100/40Mbps for $59 a month, it's cheap and it’s not the NBN because the service uses the TPG network the whole way from the TPG equipment installed in the MDF room of my apartment complex (~200 units) to the internet so whats not to love? Creeping up latency and their customer service & support, it's my opinion that it sucks, really sucks.

    -- I've spent weeks in the past pleading with their support to help me improve the 8bit Minecraft like WebEx calls and random dropouts.
    All rhetorical questions but why is traffic routing traffic via the USA from my home in Pyrmont to WebEx Sydney (13445.syd.equinix.com).
    Why is the latency on my connection getting worse.
    Why do I get dropouts during busy times, why after an interruption does the line sync at a lower speed.
    Why does it take a customer to point out issues on the core network,
    and I quote "it's your router sir, you need to reboot" & "sometime the internet doesn't give the speeds" 🤐🤐🤐. Maybe (using the beer truck analogy) your driver is lost and hasn't heard of the **💩 in 💩 out** fundamental of networking.

  Being an enthusiast level rusty ex-ISP network engineer I connected a 4G LTE modem (thank you employer) to my pfSense router/firewall and routed WebEx traffic over it HD audio and video calls FTW at zero cost (to me) but it annoyed me that I needed to do this. WFH is a thing why can't the 3rd largest telco in the country just peer directly with AS13445 🤷‍♂️. Anyway there's no point 🙅‍♂️ trying to rationalise those points I'll just take my business elsewhere.

  Annnnnnd breath 🧘🏼, now that's out of the system I'll move on 🤣.

**The search for a new provider begins 🚀:**

  *'It's OK until it’s not OK'* has never been truer when it comes to the way we now rely upon and use the Internet because of how and where we work (WFH + 🦠), the way we've shopped, consumed services like FaceTime, WebEx, Zoom and Netflix (my parents now use daily 🤯) to stay connected with each other. It's my opinion that  need more from a provider than *typical evening speeds*, ** a reliable low latency connection is of greater value to me than typical evening speeds** and on a side-note my fingers are crossed for more Aussie consumers thinking this way creating the market demand in-turn creating a better internet for all Australians 🇦🇺.

  My building constraints; The was (pre GigaComm) FTTB available from the NBN or TPG and from the MDF room to my unit an estimated 220 to 250 meters of 4core 26AWG copper cable and a single RJ11 (phone socket). I asked the  NBN for a FTTP quote and in my opinion that's an unethical amount of money for a building that already has NBN FTTB thus it's a lot on money for a consumer to pay, it's almost like I was been quoted for an MDF room upgrade and optic fibre cable for all my neighbours needless to say NBN can jog-on. At this stage I thought I was stuck with FTTB providers an in that case, it's my opinion that Aussie Broadband came out tops in research and recommendations from friends/colleagues (if I had to choose FTTB).

      Oh maybe now is the time to explain my perspective on **internet speed = distance/time**. I promise I'll try be succinct with this using the beer truck analogy, for this example the beer truck is...
      - limited to 100kph,
      - can carry 33,600 bottles of amber nectar,
      - it's 100km between you and the brewery aka about 1hr away.

      It's just an analogy but a brewery produces the amber nectar in great volumes and theres pubs & bottle shops that a distribute it for consumption in smaller amounts 'please drink responsibly'.
      Thus if you could imagine the journey a single 6-pack has taken to on its way to you it involves packing four 6-packs into a slab, then packing 70 slabs onto 20 pallets and all 20 pallets are loaded onto the beer truck at the brewery. Then the truck is unloaded at the pubs & bottle shops to be efficient due to the beer truck operating costs they want to mutually agree a delivery frequency and time slots between the brewery, pubs & bottle shops so the cost of delivering 6 or 33,600 bottles of amber nectar is bottles is efficient and costs less per bottle delivered.

  As we know frequency is generally defined as the number of cycles which occur in a given interval of **time**, lots of delivery cycles (more beer trucks, more costs) could deliver more amber nectar in 1 hour but the brewery is still 100km away. Building another brewery closer to me would reduce the **distance** but could also be very expensive so generally we all agree to share the beer truck and wait (latency).  


Early GigaComm Scepticism:

The network & tech enthusiast in me obviously upgraded the iPhone when Telstra 5G was launched and thus experienced an oddity that my mobile internet is faster than fixed-line internet 🤷‍♂️ and about par on latency tipping in favour of the fixed-line. I've also seen via technology news sites the auctions of the mmWave (pronounced as millimetre wave) 5G spectrum has completed, well network providers have paid all that money so someone must be selling a short-range (distance), high-frequency (time) network technology that delivers higher speeds.

Researching who and whats available I discovered what looks like a smaller but experienced & growing company who are combining mmWave and optical fibre technology to build "a network built for the Gigabit Age".  

- 'A new non-NBN network for the Gigabit age'
- '10x Faster than the Australian download average'
- '24/7 Consistent speeds you can rely on'

They even said I could run my NBN / current internet provider side-by-side AND they use the current copper-pair from the basement to my unit! I gave them a call and they described the technology as (think I heard correctly) “a bit of secret source technology” and that seemed too good to be true so I sent GigaComm a follow up email to seek further clarification. Always one for transparency I said.

  **"Hello this all sounds great but when an ISP or telco promises unicorns & ice cream you need to ask more questions because 26AWG copper pair has its physical limits, current vDSL technology is distance constrained and to get a higher speeds the frequency needs to increase. From what you guys as says / not saying it looks like you found a way to get the $ per consumer down with a mix of vectoring and fibre in the building.

  I will order the 1000/100 please, if the line sync cannot hold up I’ll downgrade..** I also asked GigaComm to confirm their ASN so I could research their network and peering to avoid a repeat of the WebEx issues (20+ hours a week on WebEx you need it to work flawlessly).

The reason FTTB is limited to 100/40Mbps (in my building) is because the frequency used by vDSL profile 17a is 17 MHz and the distance to the brewery sorry the DSLAM equipment in the MDF room to my unit an estimated 220 to 250 meters when the max is considered to be 300 meters and in some apartment complexes that could be the full 300 meters. To deliver a 1000/100Mbps service with low latency service needs more MHz of frequency **time**, a lot more MHz of vectoring over a shorter length of line needs to be a shorter **distance** to the equipment.

![vectoring](vectoring.jpeg)

Peering 🤝:
GigaComm are AS139049 and there's a number of ways to find out who they peer with and good news for me the look to learn the route to WebEx from Vocus and good news for everyone else for company of their size they are will connected and connect with both Equinix peering LAN ASN's giving them access to all the Equinix buildings in the region and connected on the IX Australia NSW & VIC carrier-neutral internet exchanges shortening the distance and time to hundreds of ISP's, MSP's, Amazon & Google clouds and CDN's like Akamai and Cloudflare etc.  

    Useful sites to work this out;
    - GIGACOMM-AU https://bgp.he.net/AS139049#_asinfo  
    - WebEx https://bgp.he.net/AS13445
    - Akamai https://bgp.he.net/AS20940#_asinfo
    - Cloudflare https://bgp.he.net/AS13335
    - Vocus https://bgp.he.net/AS4826#_peers
    - Another option is https://www.peeringdb.com/
    - AS139049 traffic on the IX https://metrics.ix.asn.au/d/fY3FT5Mnk/ix-peer?orgId=2&var-Customer=746&var-polling_interval=1m&var-Device=All&var-ASN=AS139049&var-ASNRAW=139049

Slight side-topic, I use Apple devices with iCloud Private Relay (iCloud subscription required) and the public IP addresses (at the time of writing this) I've observed have been 2606:54c0:820:b0::1a:7f, 104.28.125.4 (Cloudflare) and 172.225.60.23 (Akamai) and these are two very very well connected networks so  GigaComm  

**The install and what i've tested so far 🔎:**

    My own speed testing comparing the old and the new.
    From TPG
    Host: speedtest.net (selected GigaComm Pty Ltd Host a server)
    0) https://www.speedtest.net/result/12509282802
    1) https://www.speedtest.net/result/12505837863
    2) https://www.speedtest.net/result/12505887301
    3) https://www.speedtest.net/result/12505889645
    4) https://www.speedtest.net/result/12505892027
    5) https://www.speedtest.net/result/12505894579

    Host: tpg.speedtestcustom.com
    0) http://tpg.speedtestcustom.com/result/fe5e6de0-6452-11ec-b50d-5754f75e3cf4
    1) http://tpg.speedtestcustom.com/result/1a41b560-63bf-11ec-8bed-9336fa9df5d4
    2) http://tpg.speedtestcustom.com/result/293d6490-63c1-11ec-8bed-9336fa9df5d4
    3) http://tpg.speedtestcustom.com/result/489253f0-63c1-11ec-8bed-9336fa9df5d4
    4) http://tpg.speedtestcustom.com/result/63e08820-63c1-11ec-8bed-9336fa9df5d4
    5) http://tpg.speedtestcustom.com/result/7caf8b80-63c1-11ec-8bed-9336fa9df5d4