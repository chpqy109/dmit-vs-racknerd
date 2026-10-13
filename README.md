# dmit vs racknerd: premium CN2 GIA routing or cheap annual specs — how to pick the right VPS without overpaying

Put these two names side by side and the first thing you notice is that they aren't priced like competitors at all.

DMIT's cheapest China-optimized plan is around $10.90/month. RackNerd's entry annual plan is $21.99/year — about $1.83/month. Roughly six times apart, for boxes that both look like "1 core, 1–2 GB RAM, 20 GB SSD" on paper.

So "which one is better" is the wrong question. The useful question is: what are you actually going to run on it, and is the person using it sitting in Los Angeles or in Zhengzhou at 9pm?

## They're selling two different things

RackNerd sells capacity per dollar. Founded in 2019, US-based, offers VPS, shared hosting, dedicated servers and colocation, and runs specials across seven US cities — Los Angeles, San Jose, Seattle, Chicago, Dallas, Atlanta, New York. Its whole pitch is annual prepay, a 1Gbps port, and a traffic quota most people never touch. Virtualization is KVM, root access and one dedicated IPv4 included, and deployment is close to instant.

DMIT sells the route. It operates LA, Hong Kong and Tokyo, and splits every location into three network tiers: Premium (CN2 GIA), Eyeball (CMIN2/9929), and Tier 1 (plain international BGP). Same hardware generation, same control panel, wildly different paths back to China. The pricing follows the route, not the core count.

If you're hosting a blog for readers in Frankfurt, RackNerd's model is the better deal and there's nothing to argue about. The comparison only gets interesting when mainland China is in the picture.

## Why RackNerd feels fine at noon and dead at 9pm

RackNerd's standard LA plans ride plain BGP. There's no dedicated optimized path — outbound from China runs over the shared, congested transit that everyone else uses. That's not a defect; it's what $21.99/year buys.

The complaints show up in the same shape everywhere. Users report evening speeds collapsing to unusable, or describe RackNerd as fine for landing traffic and backends but not for direct connections from China. There was also a reported migration in Los Angeles from DC02 to DC03 that left some IPv4 routes detouring through Europe at close to 300ms, while IPv6 on the same box stayed normal. If your latency numbers suddenly double for no reason, check which DC you landed in and whether v4 is taking a scenic route.

DMIT's Premium tier takes a different path. Traffic from China Telecom goes out over GIA (AS4809), Unicom goes out direct on AS4837, Mobile goes out via Hong Kong Mobile (AS58453), and all three return over GIA AS4809. Eyeball balances Telecom across AS9929 and AS58807, sends Unicom over AS9929 and Mobile over AS58807. Third-party reviewers have published latency around 150ms average from China on LAX Pro, with per-city figures in the 124–155ms range depending on where you're testing from, and — the part that matters — evening peak numbers landing within a handful of milliseconds of daytime numbers.

That stability is the entire product. Not the disk speed.

## The short version

|  | DMIT | RackNerd |
| --- | --- | --- |
| Entry price | $6.90/mo (Tier 1) or $36.90/year | $21.99/year |
| Route to China | CN2 GIA / CMIN2 / 9929 on Pro & EB | No China-specific optimization |
| Locations | Los Angeles, Hong Kong, Tokyo | 7 US cities |
| Port speed | 1–10 Gbps depending on plan | 1 Gbps |
| Over-quota behavior | Throttled, server stays online | Plan traffic quota |
| Stock | Fluctuates hard, popular plans sell out | Specials rotate, popular tiers sell out |
| Payments | Card, Alipay, PayPal | Card, Alipay, PayPal |
| Fits | China-facing sites, latency-sensitive apps | Landing boxes, backups, CI, US/global apps |

## DMIT's current Los Angeles lineup, in full

DMIT's LA catalog runs on three hardware platforms — AS3 (AMD EPYC 7003), AN4 (EPYC 9004) and AN5 (EPYC 9005). AS3 is the cheap one and the one most third-party price lists quote; AN5 is the newest and carries a visible premium. Everything below is the AS3 pricing.

### Premium (LAX.Pro) — CN2 GIA, all three carriers

| Plan | CPU | RAM | SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| Pro.TINY | 1 vCore | 2 GB | 20 GB | 1 TB @ 1 Gbps | $10.90/mo | [Order LAX.Pro.TINY](https://www.dmit.io/aff.php?aff=12046) |
| Pro.Pocket | 2 vCore | 2 GB | 40 GB | 1.5 TB @ 4 Gbps | $16.90/mo | [Order LAX.Pro.Pocket](https://www.dmit.io/aff.php?aff=12046) |
| Pro.STARTER | 2 vCore | 2 GB | 80 GB | 3 TB @ 10 Gbps | $34.90/mo | [Order LAX.Pro.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MINI | 4 vCore | 4 GB | 80 GB | 5 TB @ 10 Gbps | $62.90/mo | [Order LAX.Pro.MINI](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MICRO | 4 vCore | 4 GB | 160 GB | 7 TB @ 10 Gbps | $87.90/mo | [Order LAX.Pro.MICRO](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MEDIUM | 6 vCore | 8 GB | 160 GB | 14 TB @ 10 Gbps | $199.90/mo | [Order LAX.Pro.MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

Over-quota behavior on Pro: the box gets throttled instead of suspended — 4 Mbps on TINY/Pocket/STARTER, 8 Mbps on MINI/MICRO, 10 Mbps from MEDIUM up. It stays online and keeps serving at reduced speed.

### Eyeball (LAX.EB) — CMIN2, more traffic per dollar

| Plan | CPU | RAM | SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| EB.TINY | 1 vCore | 2 GB | 20 GB | 1.5 TB @ 2 Gbps | $10.90/mo | [Order LAX.EB.TINY](https://www.dmit.io/aff.php?aff=12046) |
| EB.Pocket | 2 vCore | 2 GB | 40 GB | 3 TB @ 4 Gbps | $16.90/mo | [Order LAX.EB.Pocket](https://www.dmit.io/aff.php?aff=12046) |
| EB.STARTER | 2 vCore | 2 GB | 80 GB | 5 TB @ 10 Gbps | $34.90/mo | [Order LAX.EB.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| EB.MINI | 4 vCore | 4 GB | 80 GB | 10 TB @ 10 Gbps | $62.90/mo | [Order LAX.EB.MINI](https://www.dmit.io/aff.php?aff=12046) |
| EB.MICRO | 4 vCore | 4 GB | 160 GB | 14 TB @ 10 Gbps | $87.90/mo | [Order LAX.EB.MICRO](https://www.dmit.io/aff.php?aff=12046) |
| EB.MEDIUM | 6 vCore | 8 GB | 160 GB | 30 TB @ 10 Gbps | $199.90/mo | [Order LAX.EB.MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

Compare STARTER in the two tiers: identical $34.90, identical CPU and RAM and disk — but EB gives you 5 TB instead of 3 TB. If your audience skews Unicom or Mobile, EB is simply the better buy at the same price. Pro's edge is concentrated in Telecom users and in return-path consistency.

### Tier 1 (LAX.T1) — international BGP, no China optimization

| Plan | CPU | RAM | SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| T1.WEE | 1 vCore | 1 GB | 20 GB | 1 TB @ 4 Gbps (annual only) | $36.90/year | [Order LAX.T1.WEE](https://www.dmit.io/aff.php?aff=12046) |
| T1.TINY | 1 vCore | 1 GB | 20 GB | 2 TB @ 4 Gbps | $6.90/mo | [Order LAX.T1.TINY](https://www.dmit.io/aff.php?aff=12046) |
| T1.STARTER | 2 vCore | 2 GB | 40 GB | 4 TB @ 10 Gbps | $12.90/mo | [Order LAX.T1.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| T1.MINI | 2 vCore | 4 GB | 80 GB | 8 TB @ 10 Gbps | $21.90/mo | [Order LAX.T1.MINI](https://www.dmit.io/aff.php?aff=12046) |
| T1.MICRO | 4 vCore | 4 GB | 120 GB | 16 TB @ 10 Gbps | $32.90/mo | [Order LAX.T1.MICRO](https://www.dmit.io/aff.php?aff=12046) |

T1 throttles far more generously than Pro/EB when you burn through traffic — 100 Mbps on WEE, 200 Mbps up to MINI, 500 Mbps on MICRO — because there's no premium route to protect.

DMIT also sells the same three tiers in Hong Kong and Tokyo. Hong Kong T1 starts at $36.90/year for the 1C/1G/20G/1 TB WEE plan, with monthly plans from $6.90; Tokyo Premium starts considerably higher, with the entry TINY at $21.90/mo. Those make sense for specific latency targets, not for general hosting.

## RackNerd's current annual lineup

| Plan | CPU | RAM | SSD | Traffic | Price | Daily cost |
| --- | --- | --- | --- | --- | --- | --- |
| 1 GB KVM VPS | 1 vCore | 1 GB | 20 GB | 3 TB @ 1 Gbps | $21.99/year | ~$1.83/mo |
| 2 GB KVM VPS | 2 vCore | 2 GB | 35 GB | 5 TB @ 1 Gbps | $35.99/year | ~$3.00/mo |
| 4 GB KVM VPS | 3 vCore | 4 GB | 60 GB | 7 TB @ 1 Gbps | $59.99/year | ~$5.00/mo |
| 6 GB KVM VPS | 6 vCore | 6 GB | 100 GB | 12 TB @ 1 Gbps | $89.99/year | ~$7.50/mo |
| 8 GB KVM VPS | 7 vCore | 8 GB | 150 GB | 20 TB @ 1 Gbps | $119.99/year | ~$10.00/mo |

All five include full root, a dedicated IPv4, KVM/SolusVM, and a 1Gbps port. RackNerd regularly pushes seasonal sales below these numbers — a New Year promotion listed 1 GB at $11.29/year and 2 GB at $18.29/year — but those are limited-stock events, not the standing catalog, and they sell out.

## The price math, plainly

Put the closest equivalents next to each other:

- **1C/1G, ~20 GB SSD:** RackNerd $21.99/year (3 TB) vs DMIT T1 WEE $36.90/year (1 TB). RackNerd is cheaper and gives you three times the traffic. T1 has no China optimization, so here you're paying $15 more per year for DMIT's network and support, not for a route upgrade.
- **2C/2G:** RackNerd 2 GB at $35.99/year vs DMIT T1 STARTER at $154.80/year equivalent. That's roughly four times the price.
- **1C/2G with CN2 GIA:** DMIT Pro TINY at $10.90/mo works out to about $130.80/year for 1 TB of optimized traffic. Against RackNerd's $21.99 for 3 TB of unoptimized traffic, you're paying a six-fold premium.

If that last line looks absurd, it is only absurd if your users aren't in China. If they are, the question is whether a page that loads in 140ms at 9pm is worth six times a page that doesn't load at all.

## Which one to actually buy

**A site with a real mainland China readership.** Premium if your traffic leans Telecom, Eyeball if it leans Unicom or Mobile or you want more headroom per dollar. Start with the TINY tier of whichever one fits — 1 vCore and 2 GB handles a modest WordPress site or a small API fine, and you can measure your own evening peak before committing to a bigger plan.

**A site with a global audience.** RackNerd, or DMIT T1 if you want the same provider's hardware and support. Neither needs CN2 GIA to be fast for someone in Berlin.

**Backups, sync targets, media storage, CI runners.** T1 or RackNerd. Traffic here is machine-to-machine and doesn't care about routing, and both throttle rather than cut you off.

**Development and test environments.** RackNerd's annual pricing is hard to argue with when the box exists to be thrown away.

**A relay in front of a cheap backend.** This is the configuration the forum regulars keep describing, and it's the smartest use of both providers. A small DMIT LAX box takes the China-facing connection and forwards to a RackNerd box holding the actual application or files. The hop between the two is a US domestic transfer, which is cheap and fast, and you get good return latency without paying DMIT prices for storage you don't need.

If you want to test before buying, both providers publish Looking Glass endpoints — DMIT's is at `lg.dmit.sh`. Run a trace from your own ISP during evening peak rather than trusting anyone else's numbers, mine included.

## Things worth knowing before you pay

**Tier 1 does not mean "slightly worse CN2".** It means no China optimization at all. Every guide that recommends T1 for China traffic is recommending the wrong plan.

**Stock is the real constraint with DMIT.** Popular Pro and Eyeball plans sell out and restock in waves, sometimes within days. If the plan you want shows as unavailable, it's not a browsing error.

**Platform matters to the price.** AS3 (EPYC 7003) is the budget generation. AN5 (EPYC 9005) is newer and costs meaningfully more — the same Pro TINY that runs $10.90/mo on AS3 lists at $14.90/mo on AN5, and every larger tier scales up similarly. Unless you know you need EPYC 9005 throughput, the older platform is better value.

**DMIT replaces your IPv4 for free under specific conditions** on LAX Pro and EB: the instance has been active at least 7 days, at least 15 days have passed since the last replacement, ICMP and all TCP ports are unreachable, and you have at least 7 days of service left. That matters if you're doing anything where a blocked IP ends the project.

**RackNerd can move you between data centers.** When DC02 shifted to DC03 in Los Angeles, some users saw IPv4 take a long route while IPv6 stayed clean. If latency jumps without warning, test both stacks before assuming the provider got slower.

**Prices in third-party listicles lag behind reality.** Deal blogs copy each other for months. DMIT's own order page is the only number that counts, and the same goes for RackNerd's specials page.

## FAQ

**Is RackNerd good enough for a China-facing website?** For an audience that reads over Cloudflare, or for a site where occasional slow pages are tolerable, yes. For a paid product, a login flow, or anything latency-sensitive, the evening peak reports are consistent enough that you should expect trouble.

**Can I start small and upgrade later?** Both providers let you move up a tier. Starting on the smallest plan and measuring your own traffic for a month beats guessing at the config.

**Which DMIT tier is right for Unicom or Mobile users?** Eyeball. It routes Unicom over AS9929 and Mobile over AS58807, and gives you more traffic per dollar at the same price point.

**Is the DMIT premium actually worth six times the price?** Only if your users are in mainland China and your business depends on their load times. If the answer is no, put the money elsewhere — a bigger RackNerd box will serve you better than a smaller optimized one.

**Why is DMIT out of stock so often?** Because it doesn't oversell the way cheap annual VPS providers do. Limited stock is the mechanism that keeps evening performance stable.

## Bottom line

RackNerd wins on cost per gigabyte, traffic per dollar, and datacenter choice. For anything not aimed at a Chinese audience, it's the correct answer and the gap isn't close.

DMIT wins on the only thing that's hard to fix later: the path your packets take back into China at peak hours, plus a throttling policy that keeps a server online instead of cutting it off. You pay three to six times more for that, and if your traffic mix is Chinese, it's usually money well spent.

The honest recommendation for most people staring at this comparison: buy a small DMIT plan for anything China-facing and a cheap RackNerd box for everything else. Running both costs less than a single mid-tier plan from either one, and you stop having to choose.
# dmit vs racknerd: premium CN2 GIA routing or cheap annual specs — how to pick the right VPS without overpaying

Put these two names side by side and the first thing you notice is that they aren't priced like competitors at all.

DMIT's cheapest China-optimized plan is around $10.90/month. RackNerd's entry annual plan is $21.99/year — about $1.83/month. Roughly six times apart, for boxes that both look like "1 core, 1–2 GB RAM, 20 GB SSD" on paper.

So "which one is better" is the wrong question. The useful question is: what are you actually going to run on it, and is the person using it sitting in Los Angeles or in Zhengzhou at 9pm?

## They're selling two different things

RackNerd sells capacity per dollar. Founded in 2019, US-based, offers VPS, shared hosting, dedicated servers and colocation, and runs specials across seven US cities — Los Angeles, San Jose, Seattle, Chicago, Dallas, Atlanta, New York. Its whole pitch is annual prepay, a 1Gbps port, and a traffic quota most people never touch. Virtualization is KVM, root access and one dedicated IPv4 included, and deployment is close to instant.

DMIT sells the route. It operates LA, Hong Kong and Tokyo, and splits every location into three network tiers: Premium (CN2 GIA), Eyeball (CMIN2/9929), and Tier 1 (plain international BGP). Same hardware generation, same control panel, wildly different paths back to China. The pricing follows the route, not the core count.

If you're hosting a blog for readers in Frankfurt, RackNerd's model is the better deal and there's nothing to argue about. The comparison only gets interesting when mainland China is in the picture.

## Why RackNerd feels fine at noon and dead at 9pm

RackNerd's standard LA plans ride plain BGP. There's no dedicated optimized path — outbound from China runs over the shared, congested transit that everyone else uses. That's not a defect; it's what $21.99/year buys.

The complaints show up in the same shape everywhere. Users report evening speeds collapsing to unusable, or describe RackNerd as fine for landing traffic and backends but not for direct connections from China. There was also a reported migration in Los Angeles from DC02 to DC03 that left some IPv4 routes detouring through Europe at close to 300ms, while IPv6 on the same box stayed normal. If your latency numbers suddenly double for no reason, check which DC you landed in and whether v4 is taking a scenic route.

DMIT's Premium tier takes a different path. Traffic from China Telecom goes out over GIA (AS4809), Unicom goes out direct on AS4837, Mobile goes out via Hong Kong Mobile (AS58453), and all three return over GIA AS4809. Eyeball balances Telecom across AS9929 and AS58807, sends Unicom over AS9929 and Mobile over AS58807. Third-party reviewers have published latency around 150ms average from China on LAX Pro, with per-city figures in the 124–155ms range depending on where you're testing from, and — the part that matters — evening peak numbers landing within a handful of milliseconds of daytime numbers.

That stability is the entire product. Not the disk speed.

## The short version

|  | DMIT | RackNerd |
| --- | --- | --- |
| Entry price | $6.90/mo (Tier 1) or $36.90/year | $21.99/year |
| Route to China | CN2 GIA / CMIN2 / 9929 on Pro & EB | No China-specific optimization |
| Locations | Los Angeles, Hong Kong, Tokyo | 7 US cities |
| Port speed | 1–10 Gbps depending on plan | 1 Gbps |
| Over-quota behavior | Throttled, server stays online | Plan traffic quota |
| Stock | Fluctuates hard, popular plans sell out | Specials rotate, popular tiers sell out |
| Payments | Card, Alipay, PayPal | Card, Alipay, PayPal |
| Fits | China-facing sites, latency-sensitive apps | Landing boxes, backups, CI, US/global apps |

## DMIT's current Los Angeles lineup, in full

DMIT's LA catalog runs on three hardware platforms — AS3 (AMD EPYC 7003), AN4 (EPYC 9004) and AN5 (EPYC 9005). AS3 is the cheap one and the one most third-party price lists quote; AN5 is the newest and carries a visible premium. Everything below is the AS3 pricing.

### Premium (LAX.Pro) — CN2 GIA, all three carriers

| Plan | CPU | RAM | SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| Pro.TINY | 1 vCore | 2 GB | 20 GB | 1 TB @ 1 Gbps | $10.90/mo | [Order LAX.Pro.TINY](https://www.dmit.io/aff.php?aff=12046) |
| Pro.Pocket | 2 vCore | 2 GB | 40 GB | 1.5 TB @ 4 Gbps | $16.90/mo | [Order LAX.Pro.Pocket](https://www.dmit.io/aff.php?aff=12046) |
| Pro.STARTER | 2 vCore | 2 GB | 80 GB | 3 TB @ 10 Gbps | $34.90/mo | [Order LAX.Pro.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MINI | 4 vCore | 4 GB | 80 GB | 5 TB @ 10 Gbps | $62.90/mo | [Order LAX.Pro.MINI](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MICRO | 4 vCore | 4 GB | 160 GB | 7 TB @ 10 Gbps | $87.90/mo | [Order LAX.Pro.MICRO](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MEDIUM | 6 vCore | 8 GB | 160 GB | 14 TB @ 10 Gbps | $199.90/mo | [Order LAX.Pro.MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

Over-quota behavior on Pro: the box gets throttled instead of suspended — 4 Mbps on TINY/Pocket/STARTER, 8 Mbps on MINI/MICRO, 10 Mbps from MEDIUM up. It stays online and keeps serving at reduced speed.

### Eyeball (LAX.EB) — CMIN2, more traffic per dollar

| Plan | CPU | RAM | SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| EB.TINY | 1 vCore | 2 GB | 20 GB | 1.5 TB @ 2 Gbps | $10.90/mo | [Order LAX.EB.TINY](https://www.dmit.io/aff.php?aff=12046) |
| EB.Pocket | 2 vCore | 2 GB | 40 GB | 3 TB @ 4 Gbps | $16.90/mo | [Order LAX.EB.Pocket](https://www.dmit.io/aff.php?aff=12046) |
| EB.STARTER | 2 vCore | 2 GB | 80 GB | 5 TB @ 10 Gbps | $34.90/mo | [Order LAX.EB.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| EB.MINI | 4 vCore | 4 GB | 80 GB | 10 TB @ 10 Gbps | $62.90/mo | [Order LAX.EB.MINI](https://www.dmit.io/aff.php?aff=12046) |
| EB.MICRO | 4 vCore | 4 GB | 160 GB | 14 TB @ 10 Gbps | $87.90/mo | [Order LAX.EB.MICRO](https://www.dmit.io/aff.php?aff=12046) |
| EB.MEDIUM | 6 vCore | 8 GB | 160 GB | 30 TB @ 10 Gbps | $199.90/mo | [Order LAX.EB.MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

Compare STARTER in the two tiers: identical $34.90, identical CPU and RAM and disk — but EB gives you 5 TB instead of 3 TB. If your audience skews Unicom or Mobile, EB is simply the better buy at the same price. Pro's edge is concentrated in Telecom users and in return-path consistency.

### Tier 1 (LAX.T1) — international BGP, no China optimization

| Plan | CPU | RAM | SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| T1.WEE | 1 vCore | 1 GB | 20 GB | 1 TB @ 4 Gbps (annual only) | $36.90/year | [Order LAX.T1.WEE](https://www.dmit.io/aff.php?aff=12046) |
| T1.TINY | 1 vCore | 1 GB | 20 GB | 2 TB @ 4 Gbps | $6.90/mo | [Order LAX.T1.TINY](https://www.dmit.io/aff.php?aff=12046) |
| T1.STARTER | 2 vCore | 2 GB | 40 GB | 4 TB @ 10 Gbps | $12.90/mo | [Order LAX.T1.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| T1.MINI | 2 vCore | 4 GB | 80 GB | 8 TB @ 10 Gbps | $21.90/mo | [Order LAX.T1.MINI](https://www.dmit.io/aff.php?aff=12046) |
| T1.MICRO | 4 vCore | 4 GB | 120 GB | 16 TB @ 10 Gbps | $32.90/mo | [Order LAX.T1.MICRO](https://www.dmit.io/aff.php?aff=12046) |

T1 throttles far more generously than Pro/EB when you burn through traffic — 100 Mbps on WEE, 200 Mbps up to MINI, 500 Mbps on MICRO — because there's no premium route to protect.

DMIT also sells the same three tiers in Hong Kong and Tokyo. Hong Kong T1 starts at $36.90/year for the 1C/1G/20G/1 TB WEE plan, with monthly plans from $6.90; Tokyo Premium starts considerably higher, with the entry TINY at $21.90/mo. Those make sense for specific latency targets, not for general hosting.

## RackNerd's current annual lineup

| Plan | CPU | RAM | SSD | Traffic | Price | Daily cost |
| --- | --- | --- | --- | --- | --- | --- |
| 1 GB KVM VPS | 1 vCore | 1 GB | 20 GB | 3 TB @ 1 Gbps | $21.99/year | ~$1.83/mo |
| 2 GB KVM VPS | 2 vCore | 2 GB | 35 GB | 5 TB @ 1 Gbps | $35.99/year | ~$3.00/mo |
| 4 GB KVM VPS | 3 vCore | 4 GB | 60 GB | 7 TB @ 1 Gbps | $59.99/year | ~$5.00/mo |
| 6 GB KVM VPS | 6 vCore | 6 GB | 100 GB | 12 TB @ 1 Gbps | $89.99/year | ~$7.50/mo |
| 8 GB KVM VPS | 7 vCore | 8 GB | 150 GB | 20 TB @ 1 Gbps | $119.99/year | ~$10.00/mo |

All five include full root, a dedicated IPv4, KVM/SolusVM, and a 1Gbps port. RackNerd regularly pushes seasonal sales below these numbers — a New Year promotion listed 1 GB at $11.29/year and 2 GB at $18.29/year — but those are limited-stock events, not the standing catalog, and they sell out.

## The price math, plainly

Put the closest equivalents next to each other:

- **1C/1G, ~20 GB SSD:** RackNerd $21.99/year (3 TB) vs DMIT T1 WEE $36.90/year (1 TB). RackNerd is cheaper and gives you three times the traffic. T1 has no China optimization, so here you're paying $15 more per year for DMIT's network and support, not for a route upgrade.
- **2C/2G:** RackNerd 2 GB at $35.99/year vs DMIT T1 STARTER at $154.80/year equivalent. That's roughly four times the price.
- **1C/2G with CN2 GIA:** DMIT Pro TINY at $10.90/mo works out to about $130.80/year for 1 TB of optimized traffic. Against RackNerd's $21.99 for 3 TB of unoptimized traffic, you're paying a six-fold premium.

If that last line looks absurd, it is only absurd if your users aren't in China. If they are, the question is whether a page that loads in 140ms at 9pm is worth six times a page that doesn't load at all.

## Which one to actually buy

**A site with a real mainland China readership.** Premium if your traffic leans Telecom, Eyeball if it leans Unicom or Mobile or you want more headroom per dollar. Start with the TINY tier of whichever one fits — 1 vCore and 2 GB handles a modest WordPress site or a small API fine, and you can measure your own evening peak before committing to a bigger plan.

**A site with a global audience.** RackNerd, or DMIT T1 if you want the same provider's hardware and support. Neither needs CN2 GIA to be fast for someone in Berlin.

**Backups, sync targets, media storage, CI runners.** T1 or RackNerd. Traffic here is machine-to-machine and doesn't care about routing, and both throttle rather than cut you off.

**Development and test environments.** RackNerd's annual pricing is hard to argue with when the box exists to be thrown away.

**A relay in front of a cheap backend.** This is the configuration the forum regulars keep describing, and it's the smartest use of both providers. A small DMIT LAX box takes the China-facing connection and forwards to a RackNerd box holding the actual application or files. The hop between the two is a US domestic transfer, which is cheap and fast, and you get good return latency without paying DMIT prices for storage you don't need.

If you want to test before buying, both providers publish Looking Glass endpoints — DMIT's is at `lg.dmit.sh`. Run a trace from your own ISP during evening peak rather than trusting anyone else's numbers, mine included.

## Things worth knowing before you pay

**Tier 1 does not mean "slightly worse CN2".** It means no China optimization at all. Every guide that recommends T1 for China traffic is recommending the wrong plan.

**Stock is the real constraint with DMIT.** Popular Pro and Eyeball plans sell out and restock in waves, sometimes within days. If the plan you want shows as unavailable, it's not a browsing error.

**Platform matters to the price.** AS3 (EPYC 7003) is the budget generation. AN5 (EPYC 9005) is newer and costs meaningfully more — the same Pro TINY that runs $10.90/mo on AS3 lists at $14.90/mo on AN5, and every larger tier scales up similarly. Unless you know you need EPYC 9005 throughput, the older platform is better value.

**DMIT replaces your IPv4 for free under specific conditions** on LAX Pro and EB: the instance has been active at least 7 days, at least 15 days have passed since the last replacement, ICMP and all TCP ports are unreachable, and you have at least 7 days of service left. That matters if you're doing anything where a blocked IP ends the project.

**RackNerd can move you between data centers.** When DC02 shifted to DC03 in Los Angeles, some users saw IPv4 take a long route while IPv6 stayed clean. If latency jumps without warning, test both stacks before assuming the provider got slower.

**Prices in third-party listicles lag behind reality.** Deal blogs copy each other for months. DMIT's own order page is the only number that counts, and the same goes for RackNerd's specials page.

## FAQ

**Is RackNerd good enough for a China-facing website?** For an audience that reads over Cloudflare, or for a site where occasional slow pages are tolerable, yes. For a paid product, a login flow, or anything latency-sensitive, the evening peak reports are consistent enough that you should expect trouble.

**Can I start small and upgrade later?** Both providers let you move up a tier. Starting on the smallest plan and measuring your own traffic for a month beats guessing at the config.

**Which DMIT tier is right for Unicom or Mobile users?** Eyeball. It routes Unicom over AS9929 and Mobile over AS58807, and gives you more traffic per dollar at the same price point.

**Is the DMIT premium actually worth six times the price?** Only if your users are in mainland China and your business depends on their load times. If the answer is no, put the money elsewhere — a bigger RackNerd box will serve you better than a smaller optimized one.

**Why is DMIT out of stock so often?** Because it doesn't oversell the way cheap annual VPS providers do. Limited stock is the mechanism that keeps evening performance stable.

## Bottom line

RackNerd wins on cost per gigabyte, traffic per dollar, and datacenter choice. For anything not aimed at a Chinese audience, it's the correct answer and the gap isn't close.

DMIT wins on the only thing that's hard to fix later: the path your packets take back into China at peak hours, plus a throttling policy that keeps a server online instead of cutting it off. You pay three to six times more for that, and if your traffic mix is Chinese, it's usually money well spent.

The honest recommendation for most people staring at this comparison: buy a small DMIT plan for anything China-facing and a cheap RackNerd box for everything else. Running both costs less than a single mid-tier plan from either one, and you stop having to choose.
