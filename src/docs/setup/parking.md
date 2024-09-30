# Parked subdomains

If you don't have a docs or wiki site yet but want to claim your subdomain,
you can park it through proxypartylab's Caddy configuration.

## Default parking page

```caddyfile
@yourWikiSlugInCamelCase host your-desired-subdomain.lorebooks.wiki

handle @yourWIkiSlugInCamelCase {
    handle * ./pages/parking.lorebooks.wiki
    encode gzip
    try_files {path} /index.html
    file_server
}
```

## Can I customize the page?

Currently not yet, but that's something we're investigating on behind the scenes.
