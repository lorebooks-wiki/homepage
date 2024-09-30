# Setting up DNS records

[Open `recaptime-dev/infraops` in `github.dev`](https://github.dev/recaptime-dev/infraops)
(or via Remote Repositories VS Code extension) and open `dns/lorebooks.wiki.yaml` file.
Depending on the DNS records needed to add, copy the template below and replace the placeholder
values with those provided from your hosting provider.

Note that you also need to replace the placeholder on `octodns.cloudflare.comment` into
your GitHub username or your organization's GitHub slug for audit purposes and to let
anyone know who manages what.

Make sure that your subdomain entry is alphabetically arranged and any additional records
as sub-subdomains are grouped below the main record.

=== "A + AAAA records"

    Some hosting providers provide both static IPv4 and IPv6 addresses, so you'll
    need to configure it as a list, like this one below:

    ```yaml title="Basic A + AAAA record setup"
    <your-preferred-subdomain>:
    - octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
      ttl: 300
      type: A
      value: "XXX.YYY.ZZZ.ABC" # Change this placeholder with your own value.
    - octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
      ttl: 300
      type: A
      value: "ABCD:EFGH:IJK::" # Change this placeholder with your own value.
    ```

    If you just need A or AAAA record, simply delete the other one.

=== "CNAME"

    Most hosting providers use CNAME records to set up custom domain for your documentation or
    wiki. In this case, you just simply do this:

    ```yaml title="Basic CNAME record"
    <your-preferred-subdomain>:
      octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
      ttl: 300
      type: CNAME
      value: "cname.vercel-dns.com." # Change this placeholder with your own value.
    ```

    If you were instructed to add a CNAME record for `_acme-challenge` pointing to their
    own DNS record on DNS TXT challenges for TLS certificate issuance, DO NOT enable
    the proxy.

    ```yaml title="CNAME record for ACME challenges over DNS"
    # do not set octodns.cloudflare.proxied to true or the TLS cert issuance
    # will fail
    _acme-challenge.<your-preferred-subdomain>:
      octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
      ttl: 300
      type: CNAME
      value: "<random-hash>._acme.deno.dev."
    ```

    Don't forget to add the dot after the domain name, since octodns will flag it as a error if you didn't.

=== "With Cloudflare proxy"

    For providers that support Cloudflare's proxy, you can add the following into your subdomain's
    DNS record entries for `A`, `AAAA` and `CNAME` records:

    ```yaml hl_lines="5-6" title="CNAME setup under Cloudflare proxy"
    <your-preferred-subdomain>:
      octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
          proxied: true
          auto-ttl: true
      ttl: 300
      type: CNAME
      value: "cname.vercel-dns.com" # Change this placeholder with your own value.
    ```

    ```yaml hl_lines="5-6 13-14" title="A + AAAA record setup under Cloudflare proxy"
    <your-preferred-subdomain>:
    - octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
          proxied: true
          auto-ttl: true
      ttl: 300
      type: A
      value: "XXX.YYY.ZZZ.ABC" # Change this placeholder with your own value.
    - octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
          proxied: true
          auto-ttl: true
      ttl: 300
      type: A
      value: "ABCD:EFGH:IJK::" # Change this placeholder with your own value.
    ```

=== "TXT"

    TXT records are managed like the previous DNS record types mentioned here. If it is needed to
    be managed under a separate DNS record, like domain verification for GitLab Pages,

    ```yaml title="Example TXT record for GitLab Pages domain verification"
    _gital-pages-verification.<your-preferred-subdomain>:
      octodns:
        cloudflare:
          comment: "Managed by <your username or org GitHub slug here>"
      ttl: 300
      type: "TXT"
      value: "<code here>
    ```

## Example DNS records by service

=== "Deno Deploy"

    Here's a example configuration for `deno.hello.lorebooks.wiki`, alongside a `_acme-challenge`
    CNAME record for Deno Deploy to issue Let's Encrypt certificates (without granting them access
    to our DNS records over Cloudflare API).

    ```yaml title="deno.hello.lorebooks.wiki DNS records"
    # Project: hello
    # Description: hello lorebooks.wiki!
    # Maintainers: ajhalili2006
    deno.hello:
    - octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: A
      value: "34.120.54.55"
    - octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: AAAA
      value: "2600:1901:0:6d85::" # Change this placeholder with your own value.
    _acme-challenge.deno.hello:
      octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: CNAME
      value: "9a8dbd25e5f083266d95ed6d._acme.deno.dev."
    ```

=== "Storj DCS"

    Using custom domains for your Storj bucket is a involved process, especially
    if you don't upgrade into a paid account and need to use Cloudflare proxy to
    even get a free TLS certificate, but it can be easily configured.

    Unlike Deno Deploy, the metadata server's link sharing gateway handles Let's
    Encrypt certificate issuance over HTTP, via `/.well-known/acme-challenge`.

    ```yaml title="Storj DCS custom domain setup"
    # Generated with the following command:
    #  uplink share --dns cdn.lorebooks.wiki sj://lorebooks-wiki-cdn --not-after=none --tls
    cdn:
      octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: CNAME
      value: "link.storjshare.io."
    txt-cdn:
      octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: TXT
      values:
      - "storj-root:lorebooks-wiki-cdn"
      - "storj-access:jwvik3gmllcibuqruoq56dmyk44a"
      - "storj-tls:true"
    # Generated with the following command:
    #  uplink share --dns meta.cdn.lorebooks.wiki sj://lorebooks-wiki-cdn/meta --not-after=none --tls
    meta.cdn:
      octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: CNAME
      value: "link.storjshare.io."
    txt-meta.cdn:
      octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: TXT
      values:
      - "storj-root:lorebooks-wiki-cdn/meta"
      - "storj-access:jwhphlawjl44d35irmfy32h2bzhq"
      - "storj-tls:true"
    ```

=== "GitHub Pages with domain verification"

    If you use GitHub Pages, get challenge DNS records from your account's (or organization's)
    **Pages** settings:

    ```yaml
    ajhalili2006:
      octodns:
        cloudflare:
          comment: "Managed by ajhalili2006"
      ttl: 300
      type: CNAME
      value: andreijiroh-dev.github.io
    # Place your _github-pages-challenge-<namespace>.<subdomain> below
    # your preferred subdomain.
    _github-pages-challenge-andreijiroh-dev.ajhalili2006:
      octodns:
        cloudflare:
          comment: "Managed by ajhalili2006"
      ttl: 300
      type: TXT
      value: 10fd2b0ab293ffeb53cebef932b4db
    ```
