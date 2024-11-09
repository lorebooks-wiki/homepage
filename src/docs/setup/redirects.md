# Configuring redirects via proxypartylab

If you opt to use proxypartylab to redirect your docs/wiki subdomain somewhere else, especially
when you have your own domain and you need to reserve the 

## The easy route

[Use this GitHub issue form] and follow instructions on how to fill it up. Once
we approved the request, we'll take care the rest.

Alternatively, send a email in [plain-text] to [lorebooks.wiki-discuss] mailing
list on sourcehut, with subject `[proxypartylab]: Request to add for
your-desired-subdomaim.lorebooks.wiki` and using the template below.
Remember to replace any placeholders into real ones like your
`.lorebooks.wiki` subdomain and the target URL for redirects.

```txt
### Domain to be added

your-desired-subdomain.lorebooks.wiki

### Target URL

### Please describe why you need this service

Your reason goes here, just replace this text with a real one.

<!-- delete the text below this line, including this if not neeeded -->
**Additional (sub)domain redirect routes**:
- sub.domain.tld: https://target-url.tld/owo
- domain-two.tld: https://chaos.dev

**Paths with target URL overrides**:
- /path1: https://another-url.tld/todo
- /path2: https://why.dev/chaos
- domain-two.tld/gtwscar: https://hermitcraft.com/scar
<!-- delete the text above this line, including this if not neeeded -->

### Anything else?

* [ ] I need to proxy into the target URL instead of a simple redirect.
* [ ] Redirect all paths on the source URL
* [ ] I need to redirect some paths to other target URLs.
* [ ] I am redirecting/proxying more than one (sub)domain.

```

[Use this GitHub issue form]: https://github.com/recaptime-dev/proxyparty-caddy/issues/new?assignees=ajhalili2006&labels=&projects=&template=add-domain.yml&title=[new-domain]%3A+Request+to+add+for+your-desired-subdomain.lorebooks.wiki&domain=your-desired-subdomain.lorebooks.wiki
[plain-text]: https://useplaintext.email
[lorebooks.wiki-discuss]: mailto:~recaptime-dev/lorebooks.wiki-discuss@lists.sr.ht?subject=[proxypartylab]%3A+Request+to+add+for+your-desired-subdomain.lorebooks.wiki

## The merge request flow

### Example config

```caddyfile title="gh:recaptime-dev/proxypartylab-caddy@main/config/caddy/gcp/projects/lorebooks-wiki.Caddyfile (simplified)" hl_lines="6 10-12"
# This is the Caddy configuration for lorebooks.wiki (and its related
# domains)
*.lorebooks.wiki, *.beta.lorebooks.wiki {
  # snip other configuration

  @yourWikiSlugInCamelCase host your-desired-subdomain.lorebooks.wiki
  
  # ..snip other request handlers
  
  handle @yourWIkiSlugInCamelCase {
    redir https://target-url.tld{path}
  }

  # ..snip other handlers
}
```
