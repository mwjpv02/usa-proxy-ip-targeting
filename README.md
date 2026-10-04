# usa proxy: how to get a real US IP with state and city targeting for scraping, SERP checks and account work

People who type "usa proxy" into a search box usually want one of four things. They want a page to render the way it does for someone sitting in Ohio. They want a pool of American IPs to pull data at volume. They want one stable US address that will survive a logged-in session. Or they want to see what their own ad looks like in a specific US city.

Those are four different products with four different price shapes, and buying the wrong one is the most common way people waste money in this category. A free proxy list, meanwhile, is shared with strangers, frequently offline, and a bad idea for anything attached to an account or a payment method. It is fine for a single throwaway geo-check and not much else.

This piece walks through what actually decides whether a US-targeted job works, and uses 9Proxy — a residential network with US targeting down to state, city, ZIP and ISP — as the concrete example of what the numbers look like.

## The four products you'll be quoted when you ask for a USA proxy

Before price, know which network class you're buying. The target site sees something different in each case.

| Type | What the target sees | Cost shape | Good for | Weak at |
| --- | --- | --- | --- | --- |
| Datacenter | A server or cloud provider (hosting ASN) | Cheapest, often unlimited bandwidth | Permissive pages, API polling, your own load testing | Heavily defended retail and search results |
| ISP / static residential | A home line registered to a real US ISP, hosted on servers | Per IP per month | Long logged-in sessions, store accounts | Fast rotation across many identities |
| Rotating residential | A normal American household, changing per request or per session | Per GB, or per IP with unlimited bandwidth | Scraping, price monitoring, ad verification, SERP checks | Speed and cost predictability on heavy JS pages |
| Mobile (US carriers) | A subscriber address on AT&T, T-Mobile or Verizon | Most expensive, per GB or per line per day | Mobile-first platforms and app testing | Precise geography — mobile IPs resolve to carrier infrastructure, not the subscriber's street |

Two things trip people up here. The first is that "US" is not a targeting setting, it's a country filter — see the next section. The second is that residential IPs are slower than datacenter IPs by design. You are paying for credibility, not latency.

## Does your job need a US residential IP, or just a US IP?

The honest test is simple: does the target behave differently for a home connection than for a server, and does it show different content based on where the visitor is?

Cases where residential earns its cost:

- **US-only pricing and inventory.** Amazon, Walmart, Target, Best Buy and travel sites change price, stock and promotional banners by region. A datacenter IP gets throttled or served placeholder content on several of these.
- **Search results.** Google personalises and rate-limits by IP. Tracking how a page ranks for "plumber Dallas" from a German datacenter tells you very little.
- **Account work.** Social platforms, marketplaces and classifieds expect consumer IPs. This is where residential or mobile is not optional.
- **Ad verification.** You cannot confirm what a campaign looks like to a real American user from a hosting range.

Cases where you should not pay the residential premium: pulling open public pages, scraping documentation, hitting your own staging environment, or validating data you already collected. A datacenter IP is faster and a fraction of the cost there.

## Country targeting, state targeting and city targeting are three different things

A lot of providers sell "USA proxies" and stop at the country level. If your work depends on geography, that's not enough.

Search results shift noticeably between states. Insurance, real estate, job listings and government portals are heavily location-dependent. Retailers show regional promotions. So if you're checking rank for a keyword set or verifying a landing page in a specific market, you need at least state-level targeting, and city-level for metro-specific checks.

With 9Proxy, targeting is encoded in the proxy username rather than configured in a form. The structure is:


<username>-country-us-st-ohio-city-newyork-isp-as22773_Cox_Communications_Inc.-sst-15-ssid-device1


- `country-us` routes traffic through the United States
- `st-ohio` narrows to a state or region
- `city-newyork` narrows to a city
- `isp-as22773_Cox_Communications_Inc.` pins the ISP or ASN
- `sst-15` holds one IP for a 15-minute sticky session
- `ssid-device1` lets you run several parallel sticky IPs from the same template

Not every field has to be used. Rotating US traffic is just `country-us`. A sticky US session is `country-us-sst-15`.

One practical warning that comes straight from 9Proxy's own documentation: over-filtering starves your pool. State plus city plus ISP means a very small slice of IPs, and availability drops. For speed, target only by country. Add geography only when the task genuinely needs it.

## Pick the billing model before you pick the provider

This decision affects your invoice more than the brand name does.

**Per-IP with unlimited bandwidth** suits jobs where you can't predict page weight. JavaScript-heavy pages run 2–5 MB each, and a project touching 100,000 pages can burn through gigabytes quickly. With per-IP billing, one IP pulling 100 pages or 10,000 pages costs the same.

**Per-GB** suits high-rotation work where each request is small: lightweight scraping, API polling, geo-checking, ad verification.

9Proxy runs both models off one balance, and the mechanics differ:

- **IP-based packages** give you individual proxies with no data cap. An IP is deducted when you forward it to a local port; unused IPs sit in your balance indefinitely and never expire. Once activated, a proxy stays online for several hours up to roughly 24 hours, which is normal for residential pool IPs. Auto Refresh swaps out dead ones automatically.
- **GB-based packages** rotate through the whole pool. Standard GB packages carry a 180-day validity window for the traffic you buy; the enterprise tiers remove expiry entirely.

There's also the Today List: any proxy you used in the last 24 hours can be re-forwarded at no extra cost, which cuts spend on recurring daily jobs.

## Setting up a US exit with 9Proxy

Three routes, depending on how you work.

**1. Rotating residential over username/password (script-friendly)**


curl -x yourproxyhost:yourport \
     -U "subuser-country-us:yourpassword" \
     https://ipinfo.io


**2. Sticky US sessions** — add `sst` in minutes, and `ssid` when you need several fixed IPs at once:


subuser-country-us-sst-15-ssid-bot01:yourpassword


**3. The desktop app (Windows, macOS, Linux)** — filter the IP list by country, state, city, ZIP code or ISP, forward a selected proxy to a port, then use it on `localhost:port`. On Linux the terminal equivalent is:


9proxy proxy -c US -p 60000


That binds a US residential proxy to port 60000; `curl -x socks5://127.0.0.1:60000 https://ipinfo.io/json` should come back with a US address.

Always verify before you scale. Checking the IP alone isn't enough — look at city and ASN too, because the point of US targeting is matching the fingerprint the site expects. If a site expects a Phoenix consumer line and you show up as an Ohio hosting range, the campaign is wasted.

For teams, 9Proxy supports sub-accounts and share codes, so an agency can distribute IP pools across clients without handing over the master account.

## What 9Proxy actually costs

9Proxy raised prices on its IP-based and bundle packages on 1 June 2026 — the first adjustment in the company's history, per its own announcement. GB-based pricing was left untouched. The tiers below reflect the post-adjustment structure; prices change, so confirm on the pricing page before you commit.

**IP-based residential (unlimited bandwidth per IP)**

| Package | Effective per-IP price | Total | Buy |
| --- | --- | --- | --- |
| 100 IPs | $0.24 | $24 | Check the 100 IP package |
| 500 IPs | $0.144 | $72 | See the 500 IP package |
| 1,000 + 500 bonus IPs | $0.084 | $126 | View the 1,500 IP package |
| 2,500 IPs | $0.084 | $210 | Compare the 2,500 IP package |
| 5,000 IPs | $0.072 | $360 | Get the 5,000 IP package |
| 15,000 IPs | $0.048 | $720 | Look at the 15,000 IP package |
| 25,000 IPs | $0.035 | $863 | Open the 25,000 IP package |
| 50,000 IPs | $0.029 | $1,438 | See the 50,000 IP package |

**Business IP packages**

| Package | Effective per-IP price | Total | Buy |
| --- | --- | --- | --- |
| 100,000 IPs | $0.023 | $2,300 | Check the 100,000 IP package |
| 200,000 IPs | $0.021 | $4,140 | View the 200,000 IP package |
| 500,000 IPs | $0.018 | $8,625 | Open the 500,000 IP package |

**GB-based residential (rotating)**

| Package | Effective per-GB price | Total | Validity | Buy |
| --- | --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days | Start with the 5 GB plan |
| 50 + 5 GB | $2.10 | $105 | 180 days | See the 55 GB plan |
| 100 GB | $1.50 | $150 | 180 days | Compare the 100 GB plan |
| 200 GB | $1.00 | $200 | 180 days | Get the 200 GB plan |
| 1,000 GB | $0.80 | $800 | 180 days | View the 1,000 GB plan |
| 2,000 GB | $0.75 | $1,500 | 180 days | Open the 2,000 GB plan |

**Enterprise GB packages (no expiry)**

| Package | Effective per-GB price | Total | Validity | Buy |
| --- | --- | --- | --- | --- |
| 3,000 GB | $0.72 | $2,160 | No expiry | Check the 3,000 GB plan |
| 6,000 GB | $0.70 | $4,200 | No expiry | View the 6,000 GB plan |
| 10,000 GB | $0.68 | $6,800 | No expiry | Open the 10,000 GB plan |

**Bundle packages (IPs + traffic)**

| Bundle | Equivalent value | Price | Buy |
| --- | --- | --- | --- |
| 100 IPs + 5 GB | Entry bundle for mixed test workloads | $30 | Get the Starter bundle |
| 1,500 IPs + 50 GB | Mid-volume bundle for agencies running several clients | $180 | See the Popular bundle |
| 5,000 IPs + 500 GB | Listed at $860, shown at 16.28% off in 9Proxy's billing docs | $720 | View the Pro bundle |

The headline "from $0.015 or $0.018 per IP" figures you'll see in ad copy only appear at the very top of the ladder. At 100 IPs you're paying $0.24 each; the per-unit price falls by roughly 88% between the smallest and largest tiers. That's the real story of the price list, and it's why committing to 50,000 IPs before you've tested success rates on your actual targets is a bad first move.

## Which US plan fits which job

**Tiny test or a single US-exit script:** the 5 GB plan ($15) or the 100 IP package ($24). Enough to run your targets for a week and find out whether your success rate justifies the next tier.

**US price monitoring at volume:** GB-based. Rotation plus small responses make bandwidth pricing more efficient than holding IPs you don't use. If your pages are heavy and JS-laden, flip to per-IP — that's exactly the workload unlimited bandwidth exists for.

**US SERP tracking across states:** per-IP, with state targeting. You're holding an identity per location, not pushing huge data volumes.

**Multi-account and social work on US platforms:** per-IP with sticky sessions (`sst` plus `ssid` per instance), and consider mobile only if the platform specifically trusts carrier IPs. Mobile is the most expensive option and its geography is approximate, so don't reach for it to solve a targeting problem.

**Agency or reseller:** sub-accounts, share codes, and the bundle tiers — 5,000 IPs plus 500 GB at $720 is the configuration built for running several clients off one budget line.

## Things worth knowing before you pay

- **It's balance-based, not subscription-based.** You top up and spend; there are no recurring monthly charges to cancel. Good if your project is bursty, less convenient if you like flat invoices.
- **Activated IPs aren't permanent.** A residential proxy stays live for hours up to about a day. If a session must survive for weeks, you want a static ISP product, not this.
- **Unused IPs don't expire, but standard GB traffic has 180 days.** Only the enterprise GB tiers remove the deadline. Buy traffic in line with your actual usage pattern, not with optimism.
- **Pool size isn't a guarantee of coverage.** 9Proxy advertises 20M+ residential IPs across 90+ countries, with the strongest coverage in the US, Southeast Asia and Latin America. Not every ZIP or ISP has stock at every moment.
- **Support is human and 24/7** via Telegram, email and tickets — useful when a targeting string isn't returning IPs, which is usually a filter problem rather than an outage.
- **Check the service status yourself.** One reseller-run review site reported availability problems during 2026 infrastructure migrations, and while 9Proxy's blog, docs and third-party listings were live as of the most recent checks, the sensible response to any provider with a history of migration downtime is the same: fund a small balance, test your targets, then scale. Never park a quarter's budget in a prepaid wallet.

## FAQ

**Can I use a free USA proxy list instead?** For a one-time check of whether a page loads differently, maybe. They're shared, slow, unpredictably dead, and occasionally run by people collecting the traffic. Nothing with a login or a budget behind it should touch one.

**Does 9Proxy have US IPs?** Yes — the US is one of its strongest markets, and targeting runs down to state, city, ZIP and ISP through the username structure or the desktop app's filter.

**How do I check the exit is really in the US?** Route a request to an IP lookup service such as `ipinfo.io/json` and read the city, region and ASN, not just the country code.

**Will it work with anti-detect browsers?** The network speaks HTTP(S) and SOCKS5 with username/password or IP authentication, which is what AdsPower, Dolphin Anty, BitBrowser and similar tools expect. For IP-based packages, you point the browser at `localhost:port` after forwarding.

**Is per-IP or per-GB cheaper for me?** Do the arithmetic on one day of real traffic: total data divided by the number of distinct identities you need. Heavy pages and few identities favour per-IP; light requests and constant rotation favour per-GB.

If your project is US-specific and you're tired of guessing whether a provider's "US coverage" means a country filter or actual city-level control, 👉 browse 9Proxy's US residential plans and start with a small balance — the 100 IP package or the 5 GB plan is enough to find out whether your targets behave.
