# EtherBot and EtherBot-Fetch

Ether is an open web search platform for AI agents. It answers from its own search index. Two programs visit websites
on its behalf. This page says who they are, what they do and do not do, and how to stop them.

**Contact (opt-out and removal):** realgamer327@gmail.com
**Project:** https://github.com/MalyanDon/etherbot

## The two bots

| Bot | User-Agent header (exactly) | robots.txt token | What it does | Does it store pages? |
|---|---|---|---|---|
| **EtherBot** | `EtherBot/0.1 (+https://github.com/MalyanDon/etherbot; realgamer327@gmail.com)` | `EtherBot` | Crawls sites on Ether's approved list to build Ether's own search index | Yes: pages are staged, then indexed after review |
| **EtherBot-Fetch** | `EtherBot-Fetch/0.1 (+https://github.com/MalyanDon/etherbot; realgamer327@gmail.com)` | `EtherBot-Fetch` | Fetches one page when a user of Ether asks for it, from approved sites only | Kept for at most 24 hours; never added to the index |

The version number (`0.1`) changes when the bots change. The name and the contact do not.

## Block them with robots.txt

Copy one of these blocks into your robots.txt. No contact is needed; the change takes effect within one hour.

**Block both bots from your whole site:**
```
User-agent: EtherBot
Disallow: /
```
A `User-agent: EtherBot` group covers EtherBot-Fetch too, because "EtherBot" is part of its name.

**Block only EtherBot-Fetch (the on-request fetcher):**
```
User-agent: EtherBot-Fetch
Disallow: /
```

**Block only the crawler, and still allow on-request fetches:**
```
User-agent: EtherBot
Disallow: /

User-agent: EtherBot-Fetch
Allow: /
```

**Block part of your site:**
```
User-agent: EtherBot
Disallow: /private/
```

**Slow the crawler down:**
```
User-agent: EtherBot
Crawl-delay: 10
```
Crawl-delay is honoured when it is longer than our own limit of 1 request per second.

## What the bots do
- **Read robots.txt** before every request and on every redirect, and keep a copy for at most one hour.
- **Go slowly:** at most 1 request per second per site, one connection at a time.
- **Identify themselves:** they always send the User-Agent above. Callers cannot change it.
- **Respect refusals:**
  - **401, 403, 418 or 451** (on a page or on robots.txt) stops every request to your site, and the site stays refused for good;
  - **429 or 503** pauses requests to your site for 24 hours;
  - **any other 4xx** on robots.txt also pauses requests for 24 hours.
- **Obey page directives:** `noindex` and `nofollow` are obeyed, whether in a meta tag or in an `X-Robots-Tag` header.
- **Crawl only approved sites.** A site is approved only if its robots.txt allows EtherBot, its published terms do not forbid automated access, and it is not on our blocklist. The terms are recorded and re-checked; a change pauses crawling until a person reviews it.

## What the bots do not do
- No proxy rotation, no other user agents, no browser impersonation.
- No browser and no script running: pages that need scripts to show their content are not read.
- No working around a block, a refusal or a rate limit, and no retries through another route.
- No logins, forms or paywalls.
- No targeted collection of personal data about named people.

## Ask for removal
Write to **realgamer327@gmail.com** with your site, or the page URLs you want removed.

**What removal deletes:**
- the site (or the pages) from every store: staged crawl pages and raw copies, the crawl queue, the search index, and the on-request fetch cache;
- and then the site goes on our blocklist, so neither bot requests it again.

## Not offered yet
- **Signed requests (Web Bot Auth):** not available yet. Today you can recognise the bots only by their User-Agent.
- **A published list of our IP addresses:** not available yet. Ether runs from one machine without a fixed address.

If you see traffic that claims to be EtherBot but does not follow the rules above, please tell us at
realgamer327@gmail.com.
