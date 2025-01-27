# DNS Records

DNS records are managed via octoDNS and synchorized with the Cloudflare API
at the registry repository's `dns` directory.

## Step-by-step

### New registrations

1. Create a new YAML at `dns/partials/<domain>/<slug>.yml` where:
    * `<domain>` is either `lorebooks.wiki` or `stellapent.wiki`
    * `<slug>` is your personal or organization namespace on GitHub
2. Write your

## Receipes

### Deno Deploy

```yaml
subdomain:
- type: A
  ttl: 300
  value:
- type: AAAA
  ttl: 300
  value:
_acme-challenge.subdomain:
  type: CNAME
  ttl: 300
  value: tbd.com.
```
