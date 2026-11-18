# Best VPS for China: Which Route Survives Peak Hours, Which Location Cuts Latency, and What You Should Actually Pay (LightLayer Plan Table + Real Numbers)

Route first, location second, specs third. That order decides whether a China-facing server stays usable at 9 PM Beijing time, and it is the order almost no host puts on its order form.

LightLayer does put it there. The same 1 GB / 50 GB box is sold on a Global, a Standard and a Premium route that names CN2 and CMIN2, at **$29.99, $39.99 and $49.99 per year**. Monthly entry plans start at **$4.00**. If you want the short version: a website serving mainland visitors should take the Los Angeles Premium annual plan, and anything that needs single-digit latency to Guangdong needs a Hong Kong box with the route confirmed in writing before you pay.

> **Quick pick.** For a site or API aimed at mainland users where 150 ms is tolerable, the **Los Angeles Premium (CN2/CMIN2) plan at $49.99/year** is the cheapest documented way into a China-optimized route from this provider. For latency-sensitive work, the Hong Kong monthly plan starts at **$5.00**. Budget one hour in your first week to test both at 9 PM, not at noon.
> 👉 [See LightLayer's current plan list and prices](https://account.lightlayer.net/?affid=74)

## The full LightLayer lineup, and why the same 1 GB costs five different prices

LightLayer prices by location and route tier rather than by spec sheet, so a 1-core/1 GB/50 GB configuration appears at five prices. Nothing below has a different amount of RAM between the $24.99 and the $49.99 rows. What changes is the network path.

| Plan | vCPU / RAM / disk | Port and transfer | Price | Order |
| --- | --- | --- | --- | --- |
| Startup | 1 / 1 GB / 50 GB SSD | 100 Mbps, unmetered | $4.00/mo | [Order Startup](https://account.lightlayer.net/?affid=74) |
| Pay As You Go (base) | 2 / 2 GB / scalable | 200 Mbps, unmetered | from $5.60/mo | [Configure Pay As You Go](https://account.lightlayer.net/?affid=74) |
| Business | 32 / 32 GB / scalable | 200 Mbps, unmetered | $53.60/mo | [Order Business](https://account.lightlayer.net/?affid=74) |
| Manila, annual | 1 / 1 GB / 50 GB SSD | Premium, Standard or Global | $24.99/yr | [Order Manila annual](https://account.lightlayer.net/?affid=74) |
| Taiwan, annual | 1 / 1 GB / 50 GB SSD | Premium, Standard or Global | $24.99/yr | [Order Taiwan annual](https://account.lightlayer.net/?affid=74) |
| Los Angeles, Global | 1 / 1 GB / 50 GB SSD | Global route | $29.99/yr | [Order LA Global](https://account.lightlayer.net/?affid=74) |
| Los Angeles, Standard | 1 / 1 GB / 50 GB SSD | Standard route | $39.99/yr | [Order LA Standard](https://account.lightlayer.net/?affid=74) |
| Los Angeles, Premium | 1 / 1 GB / 50 GB SSD | Premium (CN2 / CMIN2) | $49.99/yr | [Order LA Premium](https://account.lightlayer.net/?affid=74) |

Two monthly SKUs sit outside that table and are worth knowing about. Hong Kong entry runs **$5.00/month** for 1 core, 1 GB and 50 GB SSD with 1 TB of transfer; the route on that specific SKU is listed as unclassified, so ask support which line it rides before you commit. San Jose entry is **$4.90/month** with 50 GB of HDD rather than SSD, which makes it a poor fit for anything database-shaped.

The Pay As You Go tier is the one worth a second look if you dislike preset menus. You set cores and RAM yourself and pay from $5.60, which suits a workload that needs 3 GB and no more. The 32-core Business plan at $53.60 has an audience: CI runners, game servers, Windows RDP boxes. A WordPress site is not that audience.

One caveat on the annual rows. LightLayer runs frequent promotions on annual and dedicated stock, and the entry price moves with them. Treat the figures above as the current published spread and confirm the final number in the cart. Also note the brand is young, dated to 2024 as a sub-brand of Megalayer, so there is no decade of uptime history to lean on. The price reflects that.

## Route names decoded: what you are actually paying for

China Telecom's default consumer path is **AS4134**, usually called ChinaNet or 163. It is fine at 3 AM and miserable at 9 PM. A traceroute taken during off-peak hours will show clean numbers and tell you nothing.

**CN2 GT (AS4809 Global Transit)** was the original fix for AS4134 congestion, and it stopped being a fix around 2019. It now performs close to standard routes during peak hours while costing meaningfully more. Some readers are still paying a premium for the letters "CN2" without knowing which CN2 they bought.

**CN2 GIA (AS4809 Global Internet Access)** rides a separate backbone with far less traffic on it. This is the tier people mean when they say a server "feels local" from Shanghai.

**CTGNet (AS23764)** is China Telecom's newer premium option and lands roughly equivalent to CN2 GIA on both price and performance.

The other two carriers have their own equivalents: China Unicom's **AS9929 / AS10099** and China Mobile's **CMIN2 (AS58807)**. A "three-network optimized" plan means all three carriers get premium routing from one location, which matters because you cannot choose your visitors' ISP.

Why the tier gap is worth money: during peak hours, standard-route servers routinely show 30% packet loss on a traceroute while users watch a spinner. An independent test in March 2026 measured a CN2 GIA-E Los Angeles plan at roughly **158 ms average to mainland China with zero packet loss between 8 and 10 PM**, against 300 ms+ and 15–30% loss on standard-routing competitors measured in the same window.

That is the whole argument in one number pair. The cheap line is not slower by 20%. At the hour your users are actually awake, it is unusable in a way the off-peak test never predicted.

## Where to put the server: Hong Kong, Tokyo, or Los Angeles

Distance sets a floor that no routing upgrade can beat. Hong Kong to Guangdong can measure in single-digit milliseconds. Tokyo sits in the middle. Los Angeles lands around 120–160 ms to most of the mainland.

That floor tells you when to stop paying for proximity. A blog or a standard web app at 150 ms is fine; users do not notice. Live streaming, financial dashboards, online games and real-time collaboration tools do notice, and for those the Hong Kong premium is not an upsell, it is the product.

For proxy use during a China trip, the calculation changes again. You are not serving users, you are one user with a laptop. A Tokyo or Hong Kong node gives you a shorter round trip, but the more valuable property is having a second IP ready when the first one stops answering.

## Pick by workload, not by spec sheet

**Website or API serving mainland visitors, 150 ms acceptable.** Los Angeles Premium annual, $49.99. It is the lowest documented entry into a CN2/CMIN2 route here and it handles normal traffic volumes.

**Sub-50 ms needed for south China.** Hong Kong monthly at $5.00, but only after support confirms the route on that SKU. The annual rows for Manila and Taiwan at $24.99 include a Premium option, which is worth pricing out if Hong Kong stock is thin.

**Team travel proxy for GitHub, Google Workspace, Slack, Docker Hub.** 1 GB of RAM carries a handful of people running Xray or Hysteria2. The $5.60 Pay As You Go tier gives you 2 GB of headroom for the same reason you would want it on any server: memory pressure is the usual cause of a proxy falling over mid-afternoon.

**Personal blog with no China audience.** Buy the $4.00 Startup plan and stop reading. A premium route buys you nothing your readers will feel.

Independent peak-hour testing of LightLayer's own Premium route is not published anywhere I could verify. The label is a claim, not a guarantee, and it deserves a one-week trial before you move production onto it.

## Protocols that still work, and the argument that none do

OpenVPN, plain WireGuard and basic IPSec get fingerprinted by deep packet inspection quickly now. That part is settled.

The current self-hosted stack under discussion is Xray with VLESS and XTLS Reality, or Hysteria2 and TUIC over UDP, managed through a panel like 3X-UI so you can hand out configs and QR codes. Clients are Nekoray, v2rayN, Clash variants, Sing-box, Shadowrocket and Hiddify.

Whether any of it holds is genuinely contested. One camp reports a working setup: a Tokyo node with Hysteria2 on a China Unicom connection, stable throughout a business trip. The other camp reports the opposite: a Japan server running Xray Reality where every test region timed out except one, and Hysteria2 traffic dropped outright. One reply argues that any self-built tunnel gets detected fast and the sane answer is an international roaming data plan or eSIM used as a hotspot, since that traffic never crosses the firewall in the same way.

Both reports are real and neither is comprehensive. The practical conclusion the community keeps arriving at is redundancy: two servers in different locations, two protocols, and a fallback plan that does not depend on your VPS staying reachable. Before you commit, ask support how IP replacement works if an address gets blocked, because that single policy matters more than a benchmark.

## ICP filing, in one paragraph

If the site is hosted in mainland China, you need an ICP license or the domain gets filtered. If it is hosted in Hong Kong, Taiwan or anywhere offshore, you do not. That is the industry norm and it is the reason so many China-facing sites run from Hong Kong. Confirm it against LightLayer's own terms rather than taking it as universal.

## How LightLayer compares on price

The obvious yardstick is BandwagonHost, which has run CN2 GIA plans for years. Its base KVM plan is **$49.99/year** for 1 GB RAM, 2 cores, 20 GB SSD and 1 TB of transfer on CN2 GT, which is the tier that stopped helping after 2019. The CN2 GIA-E 20G plan is **$169.99/year** (about $14.17/month) with 2 cores, 1 GB RAM, 20 GB SSD, 1 TB and a 2.5 Gbps port, plus free migration across 13 or 17 datacenters depending on which guide you read, including DC9, Japan Softbank and the Netherlands. Its Hong Kong CN2 GIA 40G plan runs **$89.99/month** with a claimed 30–40 ms to the mainland.

DMIT sits on the same AS4809 backbone with comparable latency and a better reputation for handling DDoS, at the cost of fewer locations, no free migration and prices that do not undercut BandwagonHost's premium tiers. Forum users quote a Hong Kong CN2 GIA starter plan around $70/month, a figure that has not been checked against DMIT's official page. RackNerd goes the other way entirely: sub-$20/year plans on ChinaNet/163, fine for everything except serving China.

Against that field, **$49.99/year** for LightLayer's Los Angeles Premium is roughly a third of BandwagonHost's CN2 GIA-E annual price. What the cheaper plan does not buy you is a long track record or a migration network, and BandwagonHost's own weakness is worth knowing too: its CN2 GIA IPs get null-routed under attack rather than cleaned, which takes you offline either way.

One naming caution. LightLayer and LightNode are separate companies with separate pricing. Search results mix them freely, and the plan tables do not transfer between them.

## Before you order: three rules and two checks

Match the plan to the job: a mainland-facing site at 150 ms tolerance takes the **$49.99/year Los Angeles Premium**; sub-50 ms work needs Hong Kong with the route confirmed; a trip proxy takes the **$5.60 Pay As You Go** tier and a second server somewhere else.

Then check two things. First, the route has to be named on the order page or in a support reply. "Premium" on its own is a marketing word, and CN2 GT has been selling under the CN2 banner for years. Second, the refund policy is provider-fault only; change-of-mind refunds are not offered on regular or promotional stock. That is a reason to start monthly even when the annual price is tempting, and to spend the first week testing at 9 PM Beijing time rather than at noon.

👉 [Compare LightLayer's plans and start with a monthly box](https://account.lightlayer.net/?affid=74)
