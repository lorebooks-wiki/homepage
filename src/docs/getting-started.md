# Getting started: Setup your `.lorebooks.wiki` subdomain

Getting your `.lorebooks.wiki` subdomain is as easy as submitting a ticket in the
[registry repository] or [setting up a redirect].

[registry repository]: https://github.com/lorebooks-wiki/registry
[setting up a redirect]: ./setup/redirects.md

## Preflight

* [ ] [Review the hosting ToS and Acceptable Use Policy](../legal/tos.md)
* [ ] Make sure to have your email address (or another contact method) for administrative communications.
* [ ] [Check if your subdomain is in use](#checking-if-your-subdomain-is-in-use)

### Hosting Tos and AUP

It is important to follow the hosting terms and the Acceptable Use Policy to ensure that this
domain service will be available freely for years to come. Non-compilance will
make us ban your project from this service and utlimately you from Recap Time
Squad technical and community spaces if you host abusive and illegal content and
your (or your community's) behavior is abusive and breaking the law.

### Contact details

As part of your agreement with the Hosting ToS and AUP, we need your contact details,
preferably over email (or a private mailing list with just project maintainers
who have access to entire message history).

If you are uncomfortable with publicly sharing your email, let us know and we'll
provide a way for that.

### Checking if your subdomain is in use

Run a quick `dig <CNAME|A|AAAA> <your-preferred-subdomain>.lorebooks.wiki`
on your terminal (or [open whatsmydns.net](https://whatsmydns.net),
enter your desired subdomain and select `A`, `AAAA` or `CNAME` as DNS record
type to look up to and hit `Search`), replacing the placeholder `<your-preferred-subdomain>`
with your desired subdomain. If it is unused,
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
and [Caddyfile configuration] to see if it is used by someone else or reserved
for internal use. Please contact us via the issue tracker to see if it is
possible to rename or if it involves trademark use. You can also opt to
navigate directly to check if any real content is hosted there.

=== "Example subdomain with parking page"

    ![An example subdomain with parking page hosted on proxypartylab](https://meta.cdn.lorebooks.wiki/docs/Screenshot_20240819_233412.png)

=== "Example sub-subdomain (expect SSL errors)"

    ![](https://meta.cdn.lorebooks.wiki/docs/Screenshot_20240819_232929.png)

## Picking your subdomain

In order to claim a subdomain, it must be in slugiffied form,
which means the following are only allowed per the DNS spec:

* lowercase numbers and letters
* dashes only
* limited to one level sub-subdomain if using a period for subprojects.

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

## Setting it up

Depending on your chosen setup, we separate them into different documentation pages, as listed below:

* [Adding or updating DNS records](./setup/dns-records.md)
* [Parking a subdomain](./setup/parking.md)
* [Redirect somewhere else](./setup/redirects.md)

## Done

Congratulations, your docs site is now on `lorebooks.wiki` domain! 🎉 If your hosting provider requires additional steps
in verifying domain ownership, please let us know [in the issue tracker](./issue-tracker.md).


[reserved subdomains list]: ./reserved-subdomains.md
[octoDNS DNS records-as-YAML configuration]: https://github.com/recaptime-dev/infraops/blob/main/dns/lorebooks.wiki.yaml
[Caddyfile configuration]: https://github.com/recaptime-dev/proxyparty-caddy/blob/main/config/caddy/gcp/projects/lorebooks-wiki.Caddyfile