---
title: Getting started
description: Learn more how to claim your own lorebooks.wiki subdomain.
---

# Getting started with your `lorebooks.wiki` domain

Getting your `.lorebooks.wiki` subdomain for your project
or wiki community is as easy as add your own DNS records in the [registry][yaml]
(they are YAML-based DNS zonfiles which are processed by octoDNS before calling
Cloudflare's DNS API to manage them) and then sending a merge request/patch over GitHub,
GitLab or sourcehut. If you don't want to edit any YAML files, you can easily request one
in [our issue tracker].

## Preflight checklist

* [ ] Review [our subdomain service terms and Acceptable Use Policy][aup] as well as [Code of Conduct][coc]
* [ ] Make sure to have your email address (or other contact methods) for administrative communications.
* [ ] Check if your subdomain is in use by someone else.

## Checking your subdomain if in use

Try navigating your browser or do a DNS lookup [via WhatsMyDNS.net] to
`subdomain.lorebooks.wiki` (where `subdomain` is your desired subdomain).
You should expect either a `NXDOMAIN` error from your browser or DNS provider or
redirected to a parking page, which mean it is available.

## Creating DNS records

[yaml]: https://github.com/lorebooks-wiki/registry
[our issue tracker]: ./issue-tracker.md
[aup]: ../legal/tos.md
[coc]: https://policies.recaptime.dev/code-of-conduct
[via WhatsMyDNS.net]: https://whatsmydns.net