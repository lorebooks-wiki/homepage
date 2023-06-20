<!-- markdownlint-disable MD013 -->
# Adding an new project to Community Lores

Do you want to start an new documentation website under Community Lores (aka `lorebooks.wiki`)
banner? If so, you're welcome here to start a fresh project (or transfer them into its new home)!

## Prerquisites

* **Your documentation website should be SFW.** Due to various reasons, we can't
accept NSFW documentation/wiki sites into our docs directory nor even hosted here.
* **Your content should be licensed under an free license for text and image-based content.** We're talking about
[Creative Commons licenses][cc], although most open-source licenses can be also used to website content too
(using them at visuals are on the unchartered territory).
* **You should be abide by our [Code of Conduct](../../code-of-conduct.md) and [Website Hosting ToS](../../legal/tos.md).** Failure to do so might cause
your project to be ejected from the docs directory and even trigger an ban from our community if happened repeatedly.
* **For non-Recap Time Squad projects, your project or community might requires undergo verification and background checks.** [Visit the Verification Endpoint API documentation](https://rtapp-verify.lorebooks.eu.org) for
details on the process and how we do background checks.

[cc]: https://creativecommons.org/licenses

## Step-by-step process

This section contains both what steps requesters and squad members (and sometimes community wranglers) do during this process.

### Requester: Submit an request for an new project

On the lorebooks.wiki's issue tracker in either [mau.dev][mau.dev-issues][^1] or [sr.ht][srht-todo], copy and paste this following
Markdown form template and fill up the necessary details.

```md
## Basic project information

* Project name:
* Desired repository slug:
* Is this SSG website or requires an server? Explain why or why not:

## Please describe the project in 120 characters or more.

<!-- Project description goes here. -->

## Where do you host the website?

<!--

Note that we only allow custom domains for projects that will be hosted under Community Lores banner/namespace.
If you want to park an subdomain for your wiki for redirection reasons, please DO NOT USE THIS template and
instead see https://go.lorebooks.eu.org/templates/subdomain-redirection.

-->

* Hosting service: Service Name, Type (Static|PaaS|VPS/delicated server behind the scenes)
* Subdomain (for backup purposes if going with custom domain): SUBDOMAIN.lorebooks.eu.org
* Custom domain: domain.tld (or N/A if going with the subdomain instead)
```

Before hiting that `Create new issue` or `Submit` button, make sure the tittle of that ticket should follows the
following format below to help squad members and community wranglers to triage your request faster.

```plain
[new project request] Request for new project <repo-slug or project here>
```

[mau.dev-issues]: https://mau.dev/lorebooks.wiki/issue-tracker/issues/new
[srht-todo]: https://todo.sr.ht/~recaptime-dev/lorebooks.wiki
[^1]: Since we're migrating our repos to mau.dev because of free plan changes in SaaS version, gitlab.com project creation is currently limited until further notice.

### Squad Member/Community Wranglers: Review and triage the request

Once the request has been received, you should have an look first before assigning to yourself and
adding the `new project requests:assigned` tag.
As an issue assignee, you're responsible for communicating between the Infra team (who have prvilleged access to
project management[^2] and DNS stuff, among other things) and the person who requested that new project creation and reviewing
it for possible issues.

[^2]: Although creating subgroups for your project/org under our root namespace requires additional scrutiny from
squad leaders and our legal team, ANY community members with `Maintainer` access can provision an project under
`lorebooks.wiki/docs-incubator` namespace.
