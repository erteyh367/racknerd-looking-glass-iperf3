# RackNerd Speed Test: How to Use the Looking Glass, Read Ping and MTR, Test 10Gbps with iperf3, and Choose the Right Datacenter (Test IPs and Plan Notes)

Open RackNerd's Looking Glass before you buy anything. The Seattle node publishes test IPv4 `192.3.253.2`, 10MB, 100MB and 1GB test files, and ping, traceroute and MTR tools. Ping two or three candidate locations, download the 100MB file from the best one, and you have a usable latency and throughput reading in about five minutes.

That covers a normal VPS purchase. It does not explain why `speedtest-cli` reports a slow number on a server that downloads fine, or how to measure a 10Gbps dedicated box. RackNerd's own help center calls `speedtest-cli` unreliable for server testing and points to a known bug in the version shipped by several Linux distributions. For high bandwidth, the company's guide recommends `iperf3` with multiple parallel streams.

Below are the official test entry points, the commands worth running, the limits of each test, and the datacenter choice that follows from the numbers. Plan prices in this article come from a third-party compilation, so confirm the final total in the cart.

> **Quick pick:** ping Los Angeles DC-02, San Jose and Seattle first. Order the location with the lowest steady latency, not the single best reading. A 1 GB annual special is enough for a static site, a personal VPN or a bot. The 2 GB special covers a small WordPress site, a few Docker containers or a light Node.js app.
>
> 👉 [See current RackNerd VPS specials and check your chosen location](https://bit.ly/RacKnerd)

## RackNerd VPS plans at a glance

RackNerd's official specials page confirms that every VPS special includes a 1Gbps port, full root access and the ctrl control panel. The prices and transfer allowances below come from a third-party guide, not an official price quote. Confirm the plan name, location, billing term and total in the cart before paying.

### Annual KVM specials

| Plan | RAM / SSD | Monthly transfer | vCPU | Price | Order |
| --- | --- | --- | --- | --- | --- |
| 1 GB KVM Special | 1 GB / 20 GB RAID-10 | 3 TB | 1 core | $21.99/yr | [ Order](https://bit.ly/RacKnerd) |
| 2 GB KVM Special | 2 GB / 35 GB RAID-10 | 5 TB | 2 cores | $35.99/yr | [ Order](https://bit.ly/RacKnerd) |
| 4 GB KVM Special | 4 GB / 60 GB RAID-10 | 7 TB | 3 cores | $59.99/yr | [ Order](https://bit.ly/RacKnerd) |
| 6 GB KVM Special | 6 GB / 100 GB RAID-10 | 12 TB | 6 cores | $89.99/yr | [ Order](https://bit.ly/RacKnerd) |
| 8 GB KVM Special | 8 GB / 150 GB RAID-10 | 20 TB | 7 cores | $119.99/yr | [ Order](https://bit.ly/RacKnerd) |

### Standard KVM plans

| Plan | RAM / SSD | Monthly transfer | vCPU | Price | Order |
| --- | --- | --- | --- | --- | --- |
| 512 MB | 512 MB / 30 GB RAID-10 | 500 GB | 1 vCore | $26.99/yr | [ Order](https://bit.ly/RacKnerd) |
| 1 GB | 1 GB / 50 GB RAID-10 | 1 TB | 2 vCores | $17.99/mo | [ Order](https://bit.ly/RacKnerd) |
| 2 GB | 2 GB / 75 GB RAID-10 | 2 TB | 3 vCores | $20.59/mo | [ Order](https://bit.ly/RacKnerd) |
| 4 GB | 4 GB / 130 GB RAID-10 | 3 TB | 4 vCores | $24.59/mo | [ Order](https://bit.ly/RacKnerd) |
| 6 GB | 6 GB / 170 GB RAID-10 | 4 TB | 5 vCores | $27.59/mo | [ Order](https://bit.ly/RacKnerd) |
| 8 GB | 8 GB / 220 GB RAID-10 | 5 TB | 6 vCores | $36.59/mo | [ Order](https://bit.ly/RacKnerd) |
| 12 GB | 12 GB / 300 GB RAID-10 | 6 TB | 7 vCores | $55.99/mo | [ Order](https://bit.ly/RacKnerd) |

If the 2 GB special matches your workload, check the annual total for the location you want:

👉 [Check the 2 GB special and confirm the annual price in the cart](https://bit.ly/RacKnerd)

## What the Looking Glass measures

The Looking Glass is a test panel at the edge of a RackNerd datacenter. It sends ping, traceroute and MTR probes from that facility to the IP you enter, and it serves 10MB, 100MB and 1GB files for a download test. It answers one question well: how far away is this datacenter from you or your users, and what does the route look like right now.

The panel lets you switch between datacenter locations, so you can compare several without hunting for separate pages. Seattle is the easiest location to verify because RackNerd publishes both its test IP and the three file sizes. The other addresses below come from a third-party guide that compiled them. Use them as a shortcut, then confirm the location in the order form.

| Location | Test IPv4 |
| --- | --- |
| Seattle, WA | `192.3.253.2` |
| Los Angeles, CA (DC-02) | `204.13.154.3` |
| Los Angeles, CA (DC-05) | `5.181.135.8` |
| New Jersey (NYC metro) | `192.3.165.30` |

The third-party guide does not publish a test IP for every location it lists, including San Jose, Dallas, Chicago, New York, Ashburn, Atlanta, Tampa, Miami, Montreal, Toronto, Utah, London, Amsterdam, Strasbourg, Frankfurt, Dublin and Singapore. The location selector in the Looking Glass is the way to test those.

### A five-minute test routine

1. Open the Looking Glass for a candidate location and click **My IP**. That fills in your public address.
2. Run **Ping** and record the average round-trip time. Under 50ms feels instant. 50–100ms is fine for most web apps. Above 150ms starts to feel laggy for interactive work.
3. Repeat the ping on two or three other locations and compare the averages.
4. If one location is much worse than expected, run **MTR**. It combines ping and traceroute and shows packet loss at each hop, which tells you whether distance or routing is the problem.
5. Download the **100MB** test file from the best location and time it. Divide 100MB by the number of seconds to get MB/s, then multiply by 8 for Mbps. Use the 1GB file only on a fast connection when you want a longer sample.

### What the test cannot tell you

A clean ping does not prove that the specific VPS host you land on will be fast. The Looking Glass runs at the network edge; it cannot see whether the physical machine behind that edge is oversubscribed. A third-party guide makes the same point. The test is useful for avoiding a bad datacenter choice, not for auditing a hypervisor.

The panel also shows the path to your IP, not every possible route. If most of your users are on one ISP or in one city, run MTR from a known address on that network during peak hours. The route at 10am can look different at 9pm.

Do not chase a 5ms difference. It is invisible to visitors. Use the test to avoid 50ms-plus mistakes, then decide on price, transfer allowance and availability.

## Why speedtest-cli reports slow speeds

`speedtest-cli` is not a reliable way to judge a server's network. RackNerd's help center says it was designed for residential connections, its public test servers often share ports that can be saturated at busy times, and the default package in CentOS, Fedora, Debian and Ubuntu repositories has a known bug that can report slow speeds inaccurately. A low number from that tool does not mean the RackNerd network is slow.

Run the standalone script instead of the distribution package. Download the standalone `speedtest.py` from the speedtest-cli project, save it on the server as `speedtest-cli`, then make it executable:

bash
chmod +x speedtest-cli
./speedtest-cli


The script's geo-IP data can place your VPS in the wrong location, and without flags it may pick a distant test server. List the available servers and choose one manually:

bash
./speedtest-cli --list
./speedtest-cli --server 21541


Not every public test server is available at all times. Maintenance, heavy test usage and geo-IP rules can remove servers from the list.

For a broader second opinion, RackNerd's help center suggests the `nws.sh` script, which uses speedtest.net infrastructure:

bash
curl -sL nws.sh | bash -s -- -r na


That is quicker than setting up `iperf3`, but it is still a third-party test. Treat it as a sanity check, not a final throughput measurement.

## Testing 10Gbps and other high-bandwidth servers

A normal speedtest cannot measure a 10Gbps port. Most public test servers sit on a 1Gbps uplink, or on a higher port that is shared, so the result tops out at the test server's capacity rather than yours. `wget` is also a poor fit because it runs a single-threaded connection on a single CPU core.

You need three things:

- SSH access to the server you are testing.
- SSH access to a second server with a dedicated 10Gbps port to act as the listener.
- `iperf3` installed on both machines.

Temporarily disable `iptables` on both servers if firewall rules would block the test ports, then re-enable it afterwards. On the listener, start server mode:

bash
iperf3 -s


On the client, run several parallel streams:

bash
iperf3 -P 10 -c $server_ip


`-P 10` opens ten simultaneous connections. You can raise that number or run several SSH sessions with separate tests. Multiple streams matter because a single TCP stream can be pinned to one CPU core and one physical uplink. A core handling several Gbps can become the bottleneck before the network does, and the test then reports a CPU limit as a network limit.

RackNerd's blog uses a Los Angeles client and a New Jersey listener as its example. The method applies to any dedicated 10Gbps server, including RackNerd's 10Gbps unmetered line. The company says those servers run on dedicated 10Gbps ports with no usage restrictions and a BGP blend of Tier 1 providers. That is a vendor claim, not an independent measurement. The commands above are how you check it on hardware you control.

If an order form describes a "10Gbps unmetered" port as shared, the throughput you can sustain around the clock will be lower than the port speed. Read that line before comparing prices.

## Which datacenter should you test?

Start with the region closest to your users, then test two or three locations inside that region. RackNerd's order page lists Los Angeles, San Jose, Seattle, Dallas, Atlanta, Chicago, New York, Ashburn, Amsterdam, France and Dublin as VPS locations. A third-party guide lists additional locations including Utah, Tampa, Miami, Montreal, Toronto, London, Strasbourg, Frankfurt and Singapore. Availability changes, so confirm the location in the order form.

The regional suggestions below come from that third-party guide. They are starting points, not RackNerd guarantees.

- **Southeast Asia, buying a US VPS:** test Los Angeles DC-02 and San Jose first. West Coast routes are usually best to Asia-Pacific, and DC-02 has historically been the China-route pick. Seattle is also worth a ping because its test IP is published.
- **Europe, buying a US VPS:** test Ashburn, New York and New Jersey. Western Europe to the US East Coast often lands around 70–90ms, which works for non-interactive workloads.
- **Australia or New Zealand:** Los Angeles or San Jose. Both usually sit around 140–160ms; the US East Coast is worse.
- **US provider serving European users:** test Amsterdam, Dublin and Strasbourg. Dublin is the newest of the three. Let the numbers decide.
- **China:** Los Angeles DC-02 is the traditional choice. Run MTR between 18:00 and 22:00 local time, when congestion is most visible.
- **IPv6:** a third-party guide says native IPv6 is allocated in Los Angeles and Strasbourg. RackNerd's order page does not make the same statement, so confirm before ordering if IPv6 is a requirement.

The common mistake is comparing two locations that differ by 5ms and treating the lower one as a victory. The useful comparison is between a location that works and one that adds 50ms or more.

## Plans, ports and limits that affect the decision

Every VPS special includes a 1Gbps port, one dedicated IPv4 address, full root access and the ctrl control panel. The differences are RAM, SSD storage, CPU cores and monthly transfer.

The 1Gbps port is enough for most websites and applications. A 10Gbps port is a dedicated-server feature, not something the VPS specials include. The ctrl panel covers reboot, reinstall, an HTML5 VNC console, one-click apps, a network firewall, root password reset and upgrades. RackNerd also advertises instant setup, usually within 5 to 15 minutes.

Monthly transfer is the number to plan against. A third-party guide describes overages on the specials as not billed but subject to a soft cap. Do not read the word "unmetered" as a guarantee of a dedicated unlimited pipe. If your project moves terabytes of video or backups, size the plan from the listed transfer allowance.

Annual specials are cheaper per month but commit you for a year. Standard monthly plans cost more and give you an exit. The 4 GB special is the first annual plan with three cores, which matters if you run several processes at once. The 1 GB and 2 GB plans are the practical entry points for a blog, a VPN or a small application.

One limitation deserves its own line. RackNerd's knowledgebase states that it does not offer refunds or a money-back guarantee. Check the terms before paying, especially on an annual plan.

👉 [Review the plan and the terms in the cart before you order](https://bit.ly/RacKnerd)

You cannot switch datacenters from the control panel after deployment. Open a support ticket and ask; the target location may not have capacity. That is another reason to run the Looking Glass test before checkout rather than after.

A third-party review reports that the annual specials renew at the same rate. Confirm the renewal price in the cart rather than assuming the first-year price is the only price.

## FAQ

### Is the RackNerd Looking Glass free?

Yes. It is a public test panel. No account, email address or payment is required.

### Does the Looking Glass test IPv6?

The panel is built around IPv4 test addresses. Native IPv6 is a separate allocation question. A third-party guide says Los Angeles and Strasbourg have it, and you should confirm at order time if IPv6 is required.

### Can I change the datacenter after I order?

Not from the control panel. Open a support ticket and ask. Capacity at the target location is not guaranteed, so test before you buy.

### How often should I rerun the test?

Once before purchase, then quarterly if latency matters. Routes change, and peak-hour behavior can differ from off-peak results.

### Why does speedtest-cli show a lower number than a download test?

It is testing a shared third-party server, sometimes through a buggy distribution build, and it may have selected a server in the wrong location. Run the standalone script, choose a nearby server manually, and compare the result with a 100MB download or `iperf3`.

### Does a good ping mean the VPS will be fast?

No. Ping measures the path to the datacenter edge. Disk I/O, CPU contention and host oversubscription sit behind that edge and are not visible in a Looking Glass test.

## A short decision rule

If you only need latency, use the Looking Glass and ping two or three locations. If you need real download speed, time the 100MB file from the best candidate. If you need to test a 10Gbps port, use `iperf3` with `-P 10` and a second 10Gbps server as the listener.

If you are buying a VPS, test Los Angeles DC-02, San Jose and Seattle, pick the lowest steady latency that fits your budget, and confirm the location, billing term, renewal price and refund terms in the cart. RackNerd does not offer refunds, so five minutes of testing is cheaper than a year in the wrong datacenter.

👉 [Check current RackNerd VPS specials and confirm pricing at checkout](https://bit.ly/RacKnerd)
