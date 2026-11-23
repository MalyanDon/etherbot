# EtherBot

EtherBot is the web crawler for Ether, a search service that AI agents
use to find and read public web pages.

## What it does
- Fetches public web pages and stores their text in a search index.
- When a page matches a search, Ether returns short excerpts with a
  link back to the original page.
- It does not log in, fill in forms, or fetch pages behind a paywall.

## How to recognise it
User agent: `EtherBot/0.1 (+https://github.com/MalyanDon/etherbot; abhishekmalyan1@gmail.com)`

## How it behaves
- It reads and obeys robots.txt before every fetch.
- It sends at most one request per second to any one site.
- It never disguises itself as a browser and never uses rotating
  proxies.

## How to block it
Add this to your robots.txt:

    User-agent: EtherBot
    Disallow: /

To block only part of your site, list those paths instead of `/`.

## Other data we use
Ether also builds its index from Common Crawl, a public web archive
collected by CCBot, and from Wikipedia dumps. To keep your site out of
Common Crawl, block `CCBot` in robots.txt as well.

## Removal requests and contact
To have pages removed from our index, or to report a problem with the
crawler, email CONTACT_EMAIL. We act on removal requests
within 7 days.
