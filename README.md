# cheapest vps: what's actually worth it under $15/month, and when DMIT's entry plan makes sense

Let's be honest about the phrase "cheapest vps" before we go anywhere. If your only criterion is the lowest number on a checkout page, the answer is well known and not very interesting: RackNerd drops a 1GB KVM box to roughly $10–11 per *year* during promos, IONOS has a $1/month starter, and Contabo's 4GB entry sits around $3.71/month. None of those are secrets, and none of them are what this article is really about.

The more useful question is the one most people are actually asking when they type "cheapest vps": *where do I get a server that's cheap enough not to hurt, but doesn't fall apart the moment I need it to do something real?* That's a harder question, and the answer depends heavily on where your traffic is going. If your users are in mainland China or anywhere in the Asia-Pacific region, "cheap" stops being just a price tag — it becomes a routing problem. And that's the gap where a provider like DMIT enters the conversation, even though its cheapest plan lands around $10.90/month rather than $2.

## Why "cheap" looks different depending on where your users are

Most cheap VPS providers sit in U.S. or European data centers on generic Tier 1 transit. For sites serving North America or Europe, that's fine — bandwidth is cheap, latency is low, and you can get a perfectly serviceable 2GB box for less than the price of a coffee.

The moment your audience is in China, though, generic transit turns into a gamble. International gateways into China are congested at peak hours, and standard BGP routes from cheap U.S. providers often take 200–400ms with meaningful packet loss. That's the kind of performance that makes a blog feel broken and a game server unplayable.

This is why there's a whole subcategory of "cheap-ish VPS with decent China routing" that doesn't show up on most generic "cheapest vps" lists. Providers in this niche — DMIT, BandwagonHost's CN2 GIA line, HostDare's CKR series — charge more than RackNerd, but they buy premium transit like China Telecom CN2 GIA, CMIN2, and direct peering with China Unicom (AS9929) and China Mobile International. You're paying for the path, not the silicon.

So the honest framing for this article: if you literally just want the absolute cheapest box on the internet, skip ahead to the alternatives section. If you want the cheapest *thing that still works well for APAC traffic*, DMIT's entry plan is worth understanding.

## DMIT, in one paragraph

DMIT (dmit.io) is a U.S.-incorporated hosting provider operating KVM-based VPS out of Los Angeles, Hong Kong, and Tokyo on AMD EPYC hardware. The thing that distinguishes it from the pack of budget providers is network engineering — they've built out dedicated peering with all three major Chinese carriers and offer three distinct network "series" per location so you can pick how much China optimization you're willing to pay for. It's not the cheapest provider on the market, and they don't pretend to be. Their pitch is that a $10.90 box on a properly engineered network beats a $2 box on a congested one for any workload that touches Asia.

## The three network series, and why they matter for "cheap"

This is the part most comparison articles gloss over, and it's the actual key to understanding DMIT's pricing. Within each location, you pick a network series, and that choice drives both price and routing quality.

**Premium Network** combines Tier 1 transit with China Telecom CN2 GIA, DMIT's own backbone, and dedicated peering with all three major Chinese carriers (AS4809, AS9929, AS58807). Official reference latency is around 15ms from Hong Kong to Shenzhen and ~28ms from Tokyo to Shanghai, with packet loss under 0.1%. This is what you buy when your users are in mainland China and you need it to feel fast.

**Eyeball Network** pairs Tier 1 transit with "reasonable-effort" China routing via CMIN2/CMI and other Chinese eyeball ISPs. No premium guarantees, but noticeably better for Chinese residential users than plain Tier 1. Aimed at mixed China/global audiences — blogs, API backends, SaaS, dev servers.

**Tier 1 Network** is the cheapest tier: clean, optimized routing across APAC and the Americas with no China-specific enhancements. This is what you buy for backup servers, CI/CD runners, VPN relays bridging regions, bulk storage — anything where raw bandwidth matters more than which Chinese ISP your packets land on.

There's also a hardware-platform axis: AN5 (AMD EPYC 9005, Zen 5, DDR5, NVMe Gen5 — the flagship), AN4 (EPYC 9004, Zen 4 — the workhorse), and AS3 (EPYC 7003, Zen 3 — best price-per-core, mature platform). Not every combination of location × series × platform is offered; you pick from what's available at each location.

## What DMIT actually charges — full plan table

The prices below come directly from DMIT's current pricing and location pages. I've kept the monthly figures exactly as published and noted which location and network each row belongs to, because the same plan name (TINY, STARTER, etc.) means different hardware depending on where you deploy.

### Los Angeles — Premium Network (AS3 platform)

| Plan | CPU | RAM | Storage | Transfer | Port | Price (monthly) | Buy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 vCore | 2GB | 20GB SSD | 1000GB | 1Gbps | $10.90 | [ Get this plan](https://bit.ly/DmiT) |
| Pocket | 2 vCore | 2GB | 40GB SSD | 1500GB | 4Gbps | $16.90 | [ Get this plan](https://bit.ly/DmiT) |
| STARTER | 2 vCore | 2GB | 80GB SSD | 3000GB | 10Gbps | $34.90 | [ Get this plan](https://bit.ly/DmiT) |
| MINI | 4 vCore | 4GB | 80GB SSD | 5000GB | 10Gbps | $62.90 | [ Get this plan](https://bit.ly/DmiT) |
| MICRO | 4 vCore | 4GB | 160GB SSD | 7000GB | 10Gbps | $87.90 | [ Get this plan](https://bit.ly/DmiT) |
| MEDIUM | 6 vCore | 8GB | 160GB SSD | 15000GB | 10Gbps | $199.90 | [ Get this plan](https://bit.ly/DmiT) |

Note from DMIT: the LAX AS3 series is still being built out, so you may see reduced disk performance and a lower SLA than their mature platforms during this period.

### Los Angeles — Premium Network (AN5 platform, curated selection)

| Plan | CPU | RAM | Storage | Transfer | Port | Price (monthly) | Buy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| LAX.AN5.Pro.MINI | 4 vCore | 4GB DDR4 | 80GB SSD | 5000GB | 10Gbps | $79.90 | [ Get this plan](https://bit.ly/DmiT) |
| LAX.AN5.Pro.MICRO | 4 vCore | 4GB DDR4 | 160GB SSD | 7000GB | 10Gbps | $110.90 | [ Get this plan](https://bit.ly/DmiT) |
| LAX.AN5.Pro.MEDIUM | 6 vCore | 8GB DDR4 | 160GB SSD | 15000GB | 10Gbps | $289.90 | [ Get this plan](https://bit.ly/DmiT) |

### Hong Kong — Premium Network (AN5 platform)

| Plan | CPU | RAM | Storage | Transfer | Port | Price (monthly) | Buy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| MINI | 4 vCore | 4GB | 80GB SSD | 1500GB | 1Gbps | $149.90 | [ Get this plan](https://bit.ly/DmiT) |
| MICRO | 4 vCore | 4GB | 160GB SSD | 2000GB | 1Gbps | $199.90 | [ Get this plan](https://www.dmit.io/aff=18446) |
| MEDIUM | 6 vCore | 8GB | 160GB SSD | 2500GB | 1Gbps | $279.90 | [ Get this plan](https://bit.ly/DmiT) |
| LARGE | 8 vCore | 16GB | 320GB SSD | 3000GB | 1Gbps | $359.90 | [ Get this plan](https://bit.ly/DmiT) |
| GIANT | 12 vCore | 24GB | 640GB SSD | 6000GB | 1Gbps | $759.90 | [ Get this plan](https://bit.ly/DmiT) |

Hong Kong Premium is the most expensive entry point in DMIT's lineup because the data center (Equinix HK2, Kwai Chung) is a Tier IV carrier-neutral facility with direct CN2 GIA and CMI cross-border links. The ~15ms latency to mainland China is the lowest in their network. AN5 plans in Hong Kong are only available on Premium.

### Tokyo — Premium Network (AS3 platform)

| Plan | CPU | RAM | Storage | Transfer | Port | Price (monthly) | Buy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 vCore | 1GB | 20GB SSD | 500GB | 1Gbps | $21.90 | [ Get this plan](https://bit.ly/DmiT) |
| STARTER | 1 vCore | 2GB | 40GB SSD | 1000GB | 1Gbps | $45.90 | [ Get this plan](https://bit.ly/DmiT) |
| MINI | 2 vCore | 4GB | 60GB SSD | 2000GB | 1Gbps | $89.90 | [ Get this plan](https://bit.ly/DmiT) |
| MICRO | 4 vCore | 4GB | 80GB SSD | 4000GB | 1Gbps | $189.90 | [ Get this plan](https://bit.ly/DmiT) |
| MEDIUM | 4 vCore | 8GB | 160GB SSD | 6000GB | 1Gbps | $320.90 | [ Get this plan](https://bit.ly/DmiT) |
| LARGE | 8 vCore | 16GB | 320GB SSD | 8000GB | 1Gbps | $429.90 | [ Get this plan](https://bit.ly/DmiT) |
| GIANT | 8 vCore | 24GB | 640GB SSD | 15000GB | 1Gbps | $829.90 | [ Get this plan](https://bit.ly/DmiT) |

Tokyo Premium is built on CN2 GIA (AS23764) with ~28ms average latency to Shanghai and packet loss under 0.1%. Equinix TY8 in Shinagawa, Tier IV, 1.4Tbps Tier 1 transit, 50+ carriers. Tokyo also has Tier 1 Network plans available for cheaper global-only routing, but those aren't shown on the public pricing page — you configure them through the cloud instance builder.

A couple of things worth flagging before you pick a row from any of these tables:

- Prices are listed as monthly, but DMIT typically bills quarterly, semi-annually, or annually — the standard rate is what you pay regardless of billing cycle, but discount codes (more on those below) often apply only to longer prepayments.
- Tier 1 product IPs are *not* guaranteed to be reachable in all countries or regions, per DMIT's own note. If your use case depends on IP geo-reach, verify before committing to a long billing cycle.
- DMIT explicitly says "the products and prices in the table may not be updated in time due to adjustment, for reference only." So treat these as the current published prices and double-check at checkout.

## The honest verdict on the TINY plan

At $10.90/month for 1 vCPU, 2GB RAM, 20GB SSD, and 1TB transfer on a 1Gbps port, the LAX Premium TINY is DMIT's cheapest offering. By the strict "cheapest vps" definition, it isn't cheap — it's 5–10× the price of a RackNerd Black Friday box. But you're getting a fundamentally different product:

- AMD EPYC (Zen 3 on AS3, Zen 5 if you go AN5) instead of the consumer-grade or older Xeon hardware you'll find in the $2/month bracket.
- NVMe SSD storage, not the SATA SSDs or HDDs common at the bottom of the market.
- Premium CN2 GIA + dedicated peering with China Telecom, Unicom, and Mobile — the kind of routing that generic Tier 1 providers simply don't buy.
- Full root access on KVM, instant setup, snapshots, automated backups, SSH key authentication.

For someone running a personal blog, a small web app, or a proxy that needs to actually work for users in China, $10.90/month is the realistic floor for "decent" — not because DMIT is overcharging, but because CN2 GIA transit genuinely costs more per megabit than generic Tier 1. The $2 providers aren't buying it.

Where the TINY stops making sense: if your traffic is overwhelmingly U.S./Europe with no China component, you're paying for routing you'll never use. In that case, go to Hetzner, Contabo, or RackNerd and pay half as much (or less) for the same or more hardware.

## Where DMIT sits in the broader cheap VPS landscape

If I'm being straight with you, here's how DMIT compares to the providers that actually show up when you search "cheapest vps":

**RackNerd** — $1–2/month promotional plans, often under $15/year. Unbeatable on raw price. Generic U.S. data centers, generic transit. Fine for VPN endpoints, learning Linux, low-stakes sites. Don't expect miracles for Asia traffic.

**Hetzner** — ~€4/month for a 2GB CX22 in Europe. Excellent price-to-hardware ratio. No meaningful China optimization. Best choice if your users are in Europe.

**Contabo** — 4GB VPS around $3.71/month with generous bandwidth. Germany-based, slow support, oversold nodes from time to time. Good for bulk storage and CPU-light tasks.

**BandwagonHost CN2 GIA** — the direct competitor to DMIT in the China-optimized niche. Entry CN2 GIA plans typically start around $49.99/year on promotion. Comparable routing philosophy, slightly different plan structure and locations.

**HostDare CN2 GIA / CKR** — entry CN2 GIA around $35–49/year on promo. Cheaper than DMIT for similar routing, but smaller provider with fewer locations.

**DigitalOcean / Vultr / Linode** — $4–6/month entry plans, clean interfaces, lots of locations including Tokyo and Singapore. Generic transit though — their Tokyo/Singapore nodes will *not* give you CN2 GIA routing into China.

The pattern: DMIT is not competing on the "cheapest" axis. It's competing on the "cheapest *with serious APAC routing*" axis, and within that specific niche, the $10.90 TINY is actually on the lower end. BandwagonHost and HostDare can be cheaper on promo, but DMIT's hardware (EPYC + NVMe) and network engineering (multi-carrier peering, three network tiers) are arguably more consistent.

## Choosing a plan if you do go with DMIT

A practical decision tree:

1. **Personal blog or small site, mostly U.S. audience, occasional China visitors** — LAX Premium TINY ($10.90) is the entry. You get 1TB transfer which is plenty for a low-traffic site, and the Premium routing kicks in when Chinese users do show up. If you outgrow 20GB storage, the Pocket ($16.90) doubles your disk and gives you a second core plus 4Gbps port.

2. **Site or API with a meaningful China audience, budget matters** — LAX Premium STARTER ($34.90). 2 vCPU, 2GB RAM, 80GB SSD, 3TB transfer on a 10Gbps port. This is the sweet spot where you stop hitting transfer caps on a real workload.

3. **Game server, live streaming, anything latency-critical to China** — Hong Kong Premium MINI ($149.90). 4 vCPU, 4GB RAM, ~15ms to mainland. The price hurts, but you're paying for the lowest latency in DMIT's lineup and direct CN2 GIA + CMI cross-border links out of Equinix HK2.

4. **Tokyo-facing East Asia audience (Japan/Korea/Taiwan, some China)** — Tokyo Premium TINY ($21.90) for testing the waters, STARTER ($45.90) for something real. Tokyo gives you ~28ms to Shanghai, which is competitive if you can't justify Hong Kong pricing.

5. **Backup server, dev box, CI/CD runner, no China traffic** — don't buy DMIT. Go to Hetzner or Contabo. The Tier 1 Network series in LAX is technically the cheapest DMIT option for this kind of workload, but you're still paying a premium for hardware and network quality you don't need.

If you're unsure, the LAX Premium TINY is the lowest-risk way to try DMIT. You get full root access, instant setup, snapshots, and a 3-day full-refund window (minus payment-gateway fees) as long as you haven't used more than 30GB transfer — enough to actually test routing to your real users before committing.

👉 [You can grab the LAX Premium TINY or browse all current plans here.](https://bit.ly/DmiT)

## Promo codes and discounts: what's actually verifiable

DMIT does release discount codes from time to time. Their TOS is explicit that discount codes apply only to new customers (with exceptions for codes issued as business compensation), and using someone else's targeted code can get your service suspended until you pay the full order. So you want to be careful about which codes you apply.

A few that appear in current coupon aggregator listings as of mid-2026:

- **Recurring 20% off on LAX Tier 1 Annual plans** (excluding WEE & TINY) — appears across multiple coupon sites.
- **Recurring 45% off on certain LAX Premium Annual plans** — listed on hostingcouponspot.com.
- **"SPRO-20OFF" — 20% off**, referenced on HotDeals as a current best code.
- **A 10% recurring discount on LAX Tier 1 plans** plus 5% credit back, listed on couponswift.com.
- A general additional 5% off code (`7L8O3PQTHNXCFS2TXPLP`) referenced in a GitHub-hosted promo roundup.

I'd treat all coupon-aggregator codes as "try at checkout, don't rely on" — promotional periods vary, and DMIT can revoke codes without notice. The most reliable source is DMIT's own promotional pages (they run Black Friday and similar events) and the banner on their homepage when active promos are running. Don't paste a code from a random coupon site into a multi-year prepay without testing it on a short cycle first.

## Things to know before you commit

A few items from DMIT's TOS that affect the value calculation and don't always make it into reviews:

- **Refund window is narrow.** Full refund within 3 days and under 30GB transfer (new orders only). Partial refund within 30 days, calculated against either remaining transfer or remaining service time, whichever is lower. Renewals are non-refundable. If your IP isn't globally reachable, you have to contact sales *the same day you bought* — after 3GB used, no refund on those grounds.

- **No refunds if you're DDoS'd.** Targeted DDoS attacks are explicitly listed as a non-refundable scenario. If you're running anything that attracts attacks, budget for that risk.

- **Service is unmanaged.** Support tickets have a 72-hour SLA. This is a real server, not managed hosting — you're responsible for security, backups, and configuration. DMIT does offer automated backups and snapshots as features, but their TOS makes clear you're responsible for your own data.

- **OFAC-restricted countries are blocked.** Orders from Cuba, Iran, Lebanon, Libya, Myanmar, North Korea, Somalia, Sudan, and Syria aren't accepted.

- **Bandwidth overage handling.** Exceed your monthly transfer and you can choose to reset, suspend, or be speed-limited. DMIT also has a Fair Use Policy that lets them rate-limit, adjust pricing to standard bandwidth rates, or suspend service if your usage pattern is inconsistent with normal individual-machine use.

- **Price-lock is per-term only.** The price you sign up for won't increase during your current billing term, but DMIT can change listed prices and plan resources anytime between terms. They won't auto-upgrade you.

## Cheapest isn't always cheapest

The trap with "cheapest vps" as a search is that the cheapest box on the spreadsheet often costs you more in time and lost users than you save on the bill. A $2/month VPS that routes through congested gateways and drops packets during Chinese peak hours isn't cheap — it's an expensive way to make your site feel broken to the people you actually wanted to reach.

DMIT's LAX Premium TINY at $10.90/month isn't going to win any absolute-cheapest awards, and it's dishonest to pretend otherwise. But if you're picking a server for a workload that touches Asia, particularly China, it's about the lowest realistic entry point for hardware (EPYC + NVMe) and routing (CN2 GIA + multi-carrier peering) that will actually deliver the performance you're paying for. Below that price, you're either giving up routing quality, giving up hardware quality, or giving up both.

For pure U.S./Europe workloads, skip DMIT and go cheaper. For anything where Asia routing matters, the TINY is the floor — and the STARTER at $34.90 is where the value actually starts for a real workload.

👉 [If you want to check live availability and current pricing across all DMIT locations and network tiers, the plans page is the place to start.](https://bit.ly/DmiT)
