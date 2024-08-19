# Getting started: Setup your `.lorebooks.wiki` subdomain

Getting your `.lorebooks.wiki` subdomain is as easy as submitting a ticket in our issue tracker
or sending a patch to our DNS configuration in YAML or our Caddyfiles in proxypartylab repository.

## Preflight

* [ ] [Review the hosting ToS and Acceptable Use Policy](../legal/tos.md)
* [ ] Make sure to have your email address (or another contact method) for administrative communications.
* [ ] [Check if your subdomain is in use](#checking-if-your-subdomain-is-in-use)

### Hosting Tos and AUP

It is important to follow the hosting terms and the Acceptable Use Policy to ensure that this
domain service will be available freely for years to come. Non-compilance will make us ban
your project from this service and utlimately you from Recap Time Squad technical and
community spaces if you host abusive and illegal content and your (or your community's)
behavior is abusive and breaking the law.

### Contact details

As part of your agreement with the Hosting ToS and AUP, we need your contact details,
preferably over email (or a private mailing list with just project maintainers who have
access to entire message history)

### Checking if your subdomain is in use

Run a quick `dig <CNAME|A|AAAA> <your-preferred-subdomain>.lorebooks.wiki` on your terminal
(or [open whatsmydns.net](https://whatsmydns.net), enter your desired subdomain and select
`A`, `AAAA` or `CNAME` as DNS record type to look up to and hit `Search`), replacing the
placeholder `<your-preferred-subdomain>` with your desired subdomain. If it is unused,
you should expect wildcard DNS records pointing to `proxyparty.recaptime.dev`.

```
$ dig CNAME thisdoesnotexist.lorebooks.wiki

; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> CNAME thisdoesnotexist.lorebooks.wiki
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 46383
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;thisdoesnotexist.lorebooks.wiki. IN    CNAME

;; ANSWER SECTION:
thisdoesnotexist.lorebooks.wiki. 300 IN CNAME   proxyparty.recaptime.dev.

;; Query time: 16 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Aug 19 13:56:33 UTC 2024
;; MSG SIZE  rcvd: 98

$ dig A thisdoesnotexist.lorebooks.wiki

; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> A thisdoesnotexist.lorebooks.wiki
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 58424
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;thisdoesnotexist.lorebooks.wiki. IN    A

;; ANSWER SECTION:
thisdoesnotexist.lorebooks.wiki. 162 IN A       34.121.49.227

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Aug 19 13:58:31 UTC 2024
;; MSG SIZE  rcvd: 76

dig AAAA thisdoesnotexist.lorebooks.wiki

; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> AAAA thisdoesnotexist.lorebooks.wiki
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 50806
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;thisdoesnotexist.lorebooks.wiki. IN    AAAA

;; ANSWER SECTION:
thisdoesnotexist.lorebooks.wiki. 137 IN CNAME   proxyparty.recaptime.dev.
proxyparty.recaptime.dev. 300   IN      AAAA    2600:1900:4001:b0b::

;; Query time: 12 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Aug 19 13:59:16 UTC 2024
;; MSG SIZE  rcvd: 126

```

When in doubt, check the [reserved subdomains list], our [octoDNS DNS records-as-YAML configuration]
and [Caddyfile configuration] to see if it is used by someone else or reserved for internal use.
Please contact us via the issue tracker to see if it is possible to rename or if it involves
trademark use. You can also opt to navigate directly to check if any real content is hosted there.

=== "Example subdomain with parking page"

    ![An example subdomain with parking page hosted on proxypartylab](../img/Screenshot_20240819_233412.png)

=== "Example sub-subdomain (expect SSL errors)"

    ![](../img/Screenshot_20240819_232929.png)

## Adding your subdomain into your app or service provider

Once confirmed that it is unused, you need to get the required DNS records from your
service provider where you host your documentation or wiki. Here are some of them if
you need quick access to their documentation:

* [GitHub Sites](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)
* [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/custom_domains_ssl_tls_certification/)
* [Railway](https://docs.railway.app/guides/public-networking#custom-domains)

If your documentation or wiki site is hosted on a server (either in the cloud or on-perm),
make sure it is static, otherwise you'll be clogging the patch review queue and causing
us headaches.

## Adding DNS records to your subdomain

### Via the issue tracker


### By editing the YAML file

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

#### Example DNS records by service

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
    _acme-challenge.hello:
      octodns:
        cloudflare:
          comment: "Managed by recaptime-dev"
      ttl: 300
      type: CNAME
      value: "9a8dbd25e5f083266d95ed6d._acme.deno.dev."
    ```

=== "Storj DCS"

    Using custom domains for your Sotrj bucket is a involved process, especially if you don't upgrade into
    a paid account and need to use Cloudflare proxy to even get a free TLS certificate.

[reserved subdomains list]: ./reserved-subdomains.md
[octoDNS DNS records-as-YAML configuration]: https://github.com/recaptime-dev/infraops/blob/main/dns/lorebooks.wiki.yaml
[Caddyfile configuration]: https://github.com/recaptime-dev/proxyparty-caddy/blob/main/config/caddy/gcp/projects/lorebooks-wiki.Caddyfile