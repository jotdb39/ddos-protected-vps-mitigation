# DDoS Protected VPS: How Much Mitigation Do You Actually Get, What Does It Cost, and Who Blackholes You First? (SixtyNet's Plans Priced, Plus a Capacity Reality Check)

SixtyNet's DDoS-protected line starts at **$200.00 USD per year** for LAX-STARTER: 2 cores, 2 GB RAM, 40 GB NVMe, a 2 Gbps premium network port, 5 TB of traffic, and DDoS protection listed on the plan itself rather than sold as a separate add-on. The same page shows a $240.00 list rate, so the annual cycle carries the advertised 17% discount.

That answers the two questions most people type into a search bar before they read anything else. What the plan listing doesn't tell you is how much attack traffic the protection actually absorbs, what happens to your IP when someone sends more than that, and whether the cheap tier is enough. Those are the parts worth spending time on, and most pages ranking for this term skip them.

> **Quick pick:** one site, one game server, or one app on a single box, under 5 TB of monthly traffic → **LAX-STARTER at $200.00/year**. It's the cheapest plan with DDoS protection and open ports 80/443. Step up only when you need more than 5 TB of traffic or a fatter network port. 👉 [Check the LAX-STARTER plan and current annual price](https://sixtynet.net/aff.php?aff=39)

## Every SixtyNet VPS plan on the price page

SixtyNet runs one data center in Los Angeles and puts the DDoS-flagged plans under an LAX prefix. All six plans below list DDoS protection as an included feature.

| Plan | CPU / RAM / Storage | Network & traffic | Price (annual) | Order |
| --- | --- | --- | --- | --- |
| LAX-STARTER | 2 cores / 2 GB / 40 GB NVMe, 12,500 IOPS | 2 Gbps premium port, 5 TB | $200.00 USD/yr (list $240.00, save 17%) | [Order LAX-STARTER](https://sixtynet.net/aff.php?aff=39) |
| LAX-MICRO | 4 cores / 4 GB / 80 GB NVMe, 12,500 IOPS | 4 Gbps premium port, 10 TB | $400.00 USD/yr (list $480.00, save 17%) | [Order LAX-MICRO](https://sixtynet.net/aff.php?aff=39) |
| LAX-MEDIUM | 8 cores / 8 GB / 160 GB NVMe, 25,000 IOPS | 10 Gbps premium port, 20 TB | $800.00 USD/yr (list $960.00, save 17%) | [Order LAX-MEDIUM](https://sixtynet.net/aff.php?aff=39) |
| LAX-LARGE | 8 cores / 16 GB / 320 GB NVMe, 25,000 IOPS | 10 Gbps premium port, 40 TB | $1,600.00 USD/yr (list $1,920.00, save 17%) | [Order LAX-LARGE](https://sixtynet.net/aff.php?aff=39) |
| LAX-Storage-500G | 4 cores / 4 GB / 500 GB RAID 10 | 10 TB | $400.00 USD/yr | [Order the 500 GB storage plan](https://sixtynet.net/aff.php?aff=39) |
| LAX-Storage-1TB | 8 cores / 8 GB / 1 TB RAID 10 | 15 TB | $700.00 USD/yr | [Order the 1 TB storage plan](https://sixtynet.net/aff.php?aff=39) |

Two details in that table matter more than the rest. LAX-LARGE doubles RAM and storage over LAX-MEDIUM but keeps the same 8 cores and the same 10 Gbps port, so you're paying for memory density rather than CPU. And the storage plans trade NVMe for RAID 10 arrays, which is the right call for backups and mail spools, the wrong one for a database with heavy random writes.

The same page sells three other lines that are not the DDoS web-hosting line, and one of them is a trap for anyone skimming:

| Line | Configurations | Traffic | The catch |
| --- | --- | --- | --- |
| Residential IP VPS | 2C/2G/40G, 4C/4G/80G, 8C/8G/160G, 16C/16G/320G NVMe | 5 / 10 / 20 / 40 TB | **Ports 80 and 443 are closed** for IP risk-control reasons |
| AS9929 China-optimized residential | 2C/2G/40G, 4C/4G/80G NVMe | 5 / 10 TB | Refunds are issued as site balance only; the box rejects external probes and scans, and access requires whitelisting or port forwarding |

SixtyNet lists those by configuration and applies quarterly and annual billing discounts across the range, so the figure moves with the cycle you pick. Neither line can host a public website because the web ports are shut. If you land on a $50/year residential plan thinking you found a cheap web host, you'll spend an evening debugging a firewall problem that isn't a firewall problem.

## What the mitigation number on a "DDoS protected VPS" is actually measuring

Hosts quote wildly different figures because they're measuring different things, and almost none of them say which.

Liquid Web is the clearest example of per-instance sizing. Its free standard tier mitigates volumetric attacks **up to 2 Gbps** and covers small targeted attacks. Large targeted attacks require the Advanced tier at **$99/month per server**, which raises the ceiling to **10 Gbps**. Complex or sustained attacks require Premium at **$499/month per account**. Those are numbers attached to a specific server's contract.

Rad Web Hosting shows both scales side by side. Its standard protection caps at **5 Gbps** with no Layer 7 coverage. The premium tier claims **up to 1+ Tbps** and roughly 1.4 billion packets per second, and adds an advanced WAF, AI-enhanced filtering and priority response. The 1+ Tbps describes the scrubbing network's total capacity. The 5 Gbps is what an individual VPS gets on the cheap tier.

OVHcloud takes a third approach and says mitigation is **unmetered**, with no limit on attack size or duration, included on every VPS. Read its own description of the toolset and you'll find traffic analysis, rate limiting and **blackholing** named as techniques. Blackholing means the provider drops all traffic to your IP to protect the rest of the network. Your server stays up. Nobody can reach it. That's the failure mode the cheerful "unmetered" wording doesn't mention.

SixtyNet sits in a fourth category: the LAX plans list "DDOS Protection" as a line item with **no published Gbps figure at all**. Third-party write-ups describe absorption capacity around 1,000 Gbps. Treat that as the size of the filtering network, not a per-VPS guarantee, because nothing on the plan page commits to a number for your instance.

What you can actually verify about your own box is the port and the traffic allowance: 2, 4 or 10 Gbps of premium network, and 5 to 40 TB of monthly traffic. Those are the ceilings your VM lives under.

Four questions worth sending to support before you pay:

1. During a volumetric flood, does my IP get scrubbed or null-routed, and at what threshold?
2. Is there a per-IP mitigation ceiling below the network capacity?
3. Is Layer 7 filtering included, or is protection Layer 3/4 only?
4. Does mitigation traffic count against my monthly 5 TB?

A host that answers those in specifics is worth the money. A host that answers "unlimited" to all four is telling you it hasn't thought about it.

## Free protection versus paid protection: what the upgrade actually buys

Every provider in this space includes some protection at no extra cost, so "DDoS protected" on a plan page is table stakes, not a differentiator. The useful question is where the free tier stops.

Rad's tier comparison is the cleanest public framework for that. Layer 3 and Layer 4 filtering appears on both tiers. Layer 7 HTTP/HTTPS protection with an advanced WAF, AI-driven bot and attack-pattern detection, custom traffic rules, a real-time analytics dashboard and priority response appear only on premium. Liquid Web draws the same line with capacity instead of features: free handles small attacks, paid handles large ones, and only the top tier handles sustained campaigns.

Applied to SixtyNet, the LAX line tells you it includes DDoS protection and that ports 80/443 are open, which means it's built for public-facing services. It does not advertise a WAF, per-domain HTTP rules or an attack dashboard. Assume Layer 3/4 volumetric filtering and plan accordingly. If HTTP floods, credential stuffing or scrapers hammering your login form are your actual worry, put Cloudflare's free tier in front of the box. That covers the Layer 7 gap for nothing, and it hides your origin IP as a bonus.

## Who needs this, and who is lighting money on fire

Liquid Web's own writeup says a protected VPS is often enough for small to mid-sized sites, SaaS apps and ecommerce stores, and then adds the line most vendors omit: it is not a silver bullet. Finance, healthcare and online gaming face attacks that need dedicated hardware or a managed security contract on top.

That splits buyers cleanly.

**Buy the cheapest plan that fits your traffic.** A personal blog, a docs site, a side project with no revenue, a staging box. LAX-STARTER at $200/year gives you the same DDoS line item as the $1,600 plan. Paying more buys port speed and terabytes you won't use, not better protection.

**Buy for headroom if you're a target.** Game servers (someone will absolutely try to ruin a ranked match), stores during a product launch or a holiday sale, API endpoints, proxy and scraping fleets, agencies hosting client sites on one box. LAX-MICRO at $400/year is the sensible middle for most of these, and LAX-MEDIUM at $800/year if you expect to push past 10 TB.

**Don't buy a VPS at all if you're a hard target.** Sustained, well-funded attacks against a payment processor or a public-facing government service don't get solved by a $200 annual plan from anyone, SixtyNet included.

And if you're shopping for residential IPs for TikTok accounts, scraping or SEO work, the LAX line isn't what you want, but the residential line isn't a web host either. Match the product to the job before you compare prices.

## How SixtyNet's pricing sits next to two well-known options

All figures below are the vendors' own published rates at the time of writing, listed for context. Monthly billing changes the math considerably.

**Liquid Web** sells VPS from **$17/month** for a memory-oriented box (1 vCPU, 4 GB RAM, 120 GB storage, 2 TB bandwidth) and **$22/month** for a CPU-oriented one (3 vCPU, 2 GB RAM, 60 GB, 2 TB). Both include the standard protection; bigger mitigation costs $99 or $499 per month on top.

**Rad Web Hosting** starts at **$15.96/month** for 1 CPU, 1 GB RAM, 16 GB SSD in RAID 10 and 1 TB of traffic, deployed in Dallas with a 99.9% uptime SLA and a standard protection ceiling of 5 Gbps.

SixtyNet's LAX-STARTER works out to roughly **$16.70/month equivalent** for 2 cores, 2 GB RAM, 40 GB NVMe and 5 TB of traffic, which is competitive on paper against both. The trade is the billing shape: you prepay a year, you get one location in Los Angeles, and there's no monthly escape hatch if the box doesn't suit you. If you need monthly billing or a European or Asian location, SixtyNet isn't the answer yet, and the company itself frames expansion as planned rather than available.

## What you still have to do after the box is provisioned

DDoS protection covers one failure mode. It does nothing about the attacker who logs in with your password.

- Switch to SSH key authentication and disable password logins.
- Change default ports for SSH and any admin panel.
- Whitelist admin access by IP, or geo-block management interfaces entirely.
- Put a CDN or reverse proxy in front so your origin IP isn't public knowledge.
- Enable WAF rules at the edge, and rate-limit login endpoints and APIs.
- Keep the OS and every dependency patched.
- Watch traffic graphs for anomalies you didn't cause.
- Keep off-site backups and actually test a restore.

Rad states plainly that it doesn't pre-configure port blocks or firewall rules on its protected VPS plans, and points customers at CSF. Assume SixtyNet leaves the same work to you, and arrive with a firewall plan. A server with a 10 Gbps port and no firewall rules is a very fast way to serve someone else's traffic.

## FAQ

**Will my server go offline during an attack?**

That depends on the provider's mitigation policy, which SixtyNet doesn't publish in the material available on its plan pages. Blackholing is a common industry fallback, and OVHcloud names it openly as one of its techniques. Ask support directly what happens to your IP above the mitigation threshold before you commit a year of prepaid hosting.

**Can I buy more mitigation later?**

There's no separate mitigation add-on listed on SixtyNet's pricing page. The visible upgrade path is moving up the LAX line, which raises the network port from 2 to 4 to 10 Gbps and the traffic allowance from 5 to 40 TB. If your protection needs are unusual, ask before ordering rather than after.

**Is annual billing cheaper?**

Yes. The LAX plans show a 17% saving on the annual cycle, and SixtyNet advertises quarterly and annual discounts across the range. Semi-annual sits in between. The catch is that prepaying a year concentrates your risk in a vendor you haven't tested yet.

**What's the refund policy?**

SixtyNet's page states that refunds on the China-optimized residential line are issued as website balance only, not back to your payment method. Third-party reviews mention a 3-day money-back window, which is far shorter than the 30 days most hosts offer. Confirm the current terms for the LAX line in writing before you pay, and check the checkout page for which payment methods are live, since a third-party review notes card payments were suspended at one point for fraud prevention.

## How to decide

- **One site, one game server, under 5 TB/month** → LAX-STARTER, $200.00/year. 👉 [Start with LAX-STARTER](https://sixtynet.net/aff.php?aff=39)
- **Several sites or client projects, 10 TB range** → LAX-MICRO, $400.00/year.
- **Heavy traffic, databases, or you want the 10 Gbps port** → LAX-MEDIUM, $800.00/year.
- **Bulk storage with redundancy** → LAX-Storage-500G at $400.00/year.
- **Residential IPs for scraping or social accounts** → the residential line, with the understanding that 80/443 are closed.
- **Need monthly billing, a non-US location, or enterprise-grade attack response** → none of these plans, and no $200/year VPS from anyone.

Two things to confirm at checkout before you enter payment details: the exact annual total and renewal rate for the plan you picked, and the refund terms in writing. Everything else on this page you can verify yourself in about ten minutes.

👉 [Compare all SixtyNet VPS plans and current annual pricing](https://sixtynet.net/aff.php?aff=39)
