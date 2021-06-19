# FAQs

## Why the hell I need both Python3 and Node.js?

On the Python side, we need `mkdocs` (and its dependencies), and [the upstream version of `mkdocs-material`][mkodcs-material] (because we're abandoned our fork, lol).

[mkodcs-material]: https://github.com/squidfunk/mkdocs-material

We also need Node.js for Contributor Convenant and Commitizen.

## Can I get an `.community-lores.gq` (`.lores.community` in the future) even I don't converted my wiki pages into Markdown files?

Yes, but you need to provide us details like:

* A/AAAA/CNAME record to point into (if not provided, we'll host an redirect server instead)
* Where your docs/lore/wiki site is hosted on (and what software)
* And an slug so we can redirect traffic to yours

## Why you use an `.gq` domain instead of buying `lores.community`?

We don't have the money (yet) to purchase that. If you want to handle the costs of domain registration and renewal, thank you for that! Please contact [Andrei Jiroh](htttps://rtapp.tk/contact-andreijiroh) for the Netlify nameservers you should point to.
