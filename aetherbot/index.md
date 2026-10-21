---
title: AetherBot
---

# AetherBot

AetherBot is the web crawler of AetherOS, marketing audit software. It reads web pages so a marketing team can audit its own website and compare it with the competitors it names.

## How to recognise it

Every request AetherBot makes carries this user agent:

```
Mozilla/5.0 (compatible; AetherBot/1.0; +https://mistermaz.github.io/aether/aetherbot/)
```

To address it in robots.txt, use `User-agent: AetherBot`. Capitals do not matter.

AetherBot never sends a request under another crawler's name.

## What it reads, and why

- **A brand's own website:** usually a dozen pages or fewer in an audit, to check the site's content, offers, product pages and policies.
- **Competitor websites the team names:** up to three in an audit, about six pages each, to compare like for like.
- **The home page of a site that AI assistants cite** when they answer questions about the brand's market, to tell what kind of site it is.
- **Your robots.txt, sitemap and llms.txt**, which say what the site wants read.

A team runs an audit when it chooses to. AetherBot does not crawl the web at large and does not build a search index.

What it reads is analysed for the team that ran the audit, partly by AI models, and kept on that team's computer. AetherOS does not use the pages it reads to train AI models.

It does not log in, fill in forms, add to basket or buy anything. When it takes a picture of a page, it loads the page as a browser would and declines the cookie banner.

## It obeys robots.txt

Before reading a page, AetherBot reads that site's robots.txt and follows it, the standard way (RFC 9309):

- Rules in a group naming AetherBot apply to it; otherwise the `User-agent: *` group applies.
- A page your robots.txt asks bots not to read is not read. The audit says the page was left unread and why.
- **Crawl-delay is honoured.** AetherBot never reads your next page sooner than your Crawl-delay allows. When that would mean waiting more than 15 seconds, it leaves the page unread instead.
- If your robots.txt does not answer (a server error, "too many requests", or no reply within ten seconds), AetherBot reads no page of your site until it does.
- If your site answers "too many requests" to a page, AetherBot tries that page again at most once, after waiting.
- Your rules are kept for up to 24 hours, so an audit asks for your robots.txt once.

## How to block it

Add this to your robots.txt:

```
User-agent: AetherBot
Disallow: /
```

To keep it out of part of your site only, name that part, for example `Disallow: /account/`.

## Where requests come from

AetherOS runs on each team's own computer, so AetherBot's requests come from that team's own internet connection, not from one central server. There is no fixed list of addresses to allow or block: use the user agent and robots.txt above.

## Contact

If AetherBot is causing you a problem, or you want to ask about it, write to **aetherosbeta@gmail.com**. Please include your site's address and, if you can, the time of the visits.
