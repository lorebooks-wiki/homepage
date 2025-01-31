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

### Checking your subdomain if in use

Try navigating your browser or do a DNS lookup [via WhatsMyDNS.net] to
`subdomain.lorebooks.wiki` (where `subdomain` is your desired subdomain).
You should expect either a `NXDOMAIN` error from your browser or DNS provider or
redirected to a parking page, which mean it is available.

## Submitting a subdomain request issue

!!! info "This is optional but recommended"
    While you can skip ahead to the exciting parts, this step will help us review your
    usage before you proceed with the next steps as well as to track requests publicly.

[Use this issue form](https://github.com/lorebooks-wiki/registry/issues/new?template=subdomain-request.yml) to create a subdomain request issue on GitHub.

For GitLab and sourcehut users, we'll be working on alternatives to ensure coverage,
among other things.

## Creating DNS records and registrant data

> See [DNS records reference](./reference/dns-records.md) and [subdomain registry](./reference/subdomain-registry.md) for examples and more.

In the [registry repository][yaml] create a YAML file at `dns/partials/<domain>/` with the
filename format `<namespace>.yml` (`<domain>` is either `lorebooks.wiki` or `stellapent.wiki`
and `namespace` can be either your username or GitHub organization slug).

```yaml
subdomain:
  type: CNAME
  ttl: 300
  value: your-username.github.io
_github-pages-verification-your-org.subdomain:
  type: TXT
  ttl: 300
  value: asdfgh123456
```

Once you added the required records, go ahead and create another file at `data/<domain>` directory,
this time with information about the project and the subdomain maintainers:

```yaml
# yaml-language-server: $schema=../registry-schema.json

# This is the registry data template for you to use if you need some ideas.
# Replace the values below with your own for that project/site.

in_use: true
reserved: false

# project metadata
project_name: "Your Project Here"
project_description: "TBA"
project_license:
- MPL-2.0
- CC-BY-SA-4.0
project_repo_url: https://github.com/ajhalili2006/your-project-here

# Subdomain maintainers as PoCs (point of contacts)
# for the apex domain itself, we just use the data from domain registration
# here, minus the mailing address for privacy reasons.
subdomain_maintainers:
  - name: Andrei Jiroh Halili
    github: ajhalili2006
    email: ajhalili2006@crew.recaptime.dev
    bluesky: andreijiroh.dev
    fediverse: https://tilde.zone/@ajhalili2006
    matrix: ajhalili2006@andreijiroh.dev
    slack:
      - team: hackclub
        team_id: T0266FRGM
        username: ajhalili2006
        user_id: TBD  `1BG`


# contact details for the team/project
contact_details:
  github: recaptime-dev
  email: squad@crew.recaptime.dev
  slack:
    - team: hackclub
      team_id: TBD
      channel_name: recaptime-dev
      channel_id: TBD
  zulip:
    - host: recaptime-dev.zulipchat.com
      stream: lorebooks.wiki
```

## Send the patch

Once ready, submit your changes as a pull request on GitHub and wait for the YAML linter and
`octodns-sync --dry-run` to pass. Remember to mention your subdomain request issue in the description
to help us map records in our API when iplemented.

If the CI fails, look at the logs for hints and check your YAML files for any issues. Otherwise, just
wait for the review to go along and get merged.

A maintainer, usually a team member at @recaptime-dev will look at your YAML files for issues and may
suggest edits along the way. Make sure to read their feedback to understand why.

## Profit!

**If your patch got merged**: Your documentation site should be up after propagating its DNS records for up to 24 hours. You can
monitor the deployments [here](https://github.com/lorebooks-wiki/registry/actions/workflows/dns.yml),
and if something fails we'll look onto it as much as we can.

**If it is not**: Review the AUP and CoC again, update subdomain registry data and DNS records and resubmit again.

[yaml]: https://github.com/lorebooks-wiki/registry
[our issue tracker]: ./issue-tracker.md
[aup]: ../legal/tos.md
[coc]: https://policies.recaptime.dev/code-of-conduct
[via WhatsMyDNS.net]: https://whatsmydns.net
