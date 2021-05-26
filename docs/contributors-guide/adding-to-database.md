# Adding an new lore to the database

Bringing your community's lore, wiki or whatever documentation your
community call it into Community Lores helps keep the documentations in one place (you can keep your MediaWiki/Wiki.js/Google Docs/Notion-based documentation site up and use Community Lores as an backup in case of maintanenace).

## What you need

* **Either your community wiki exists within the last 3 months or your community needs a wiki.** If your wiki is newer than 3 months, please wait for up to 3 months before you apply. If you moving your docs/lore into us, you need to export everything into Markdown.
* **Only active community wikis will be accepted** Dormat community wikis are instead go to <https://archived.lores.rtapp.tk>` website. Inactive/dormat community wikis or docs are only goes to the archives repo if these don't receive any edits/contributions (atleadt 20) within the last 6 months.
* **You agree to our terms of service and code of conduct.** Please read it ahead of time. Here's the links for these:
    * ToS: https://lores.rtapp.tk/legal/ToS
    * Code of Conduct: <https://rtapp.tk/community-codeofconduct>
* **You may also need to get your community verified.** See <https://github.com/RecapTime/verify/wiki> for details on how to get verified. If you request

## Exporting your content

Create an new repo [using this template](https://github.com/community-lores/lore-starter-pack/generate). It has Mkdocs and Material theme included with Gitpod configuration, Contributor Convenant CLI for listing bot code and non-code contributors and a few management scripts for you to get started.

Use automation tools to convert vendor-locked-in format into Markdown or write Markdown files manually. For some use cases, the Material for Mkdocs has provided great documentation for these cases:

* [Buttons](https://squidfunk.github.io/mkdocs-material/reference/buttons/)
* [Tabs](https://squidfunk.github.io/mkdocs-material/reference/content-tabs/)
* [Footnotes](https://squidfunk.github.io/mkdocs-material/reference/footnotes/)
* ..and.more! Visit the [theme documentation](https://squidfunk.github.io/mkdocs-material/)

### Using Material Insider for Mkdocs

!!! warning "DO NOT COMMIT YOUR GITHUB PAT INTO ANY FILE, INCLUDING `netlify.toml`!"
    If commited, GitHub will automatically revoke the offending PAT for security reasons.
    In case that happen, you may need to [follow GitHub's guidance](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) and revoke any leaked keys.

    Since this involves rewriting the Git history, you MUST notify your fellow collaborators and any contributors that have any PRs to rebase after you force-push to prevent any hassle. While PRs and forks can still have these leaked secrets, you SHOULD contact GitHub Support to premenently remove these cached views and references.

??? info "In order to use Material for Mkdocs Insider, you should be [Martin Donath](https://github.com/squidfunk)'s patron on GitHub Sponsors."
    You should be on the $10/month tier to use the Insiders edition. And if you forked it, GitHub will delete private forks once Martin removed your collaborator access to the Insiders repo once your sponsorship is not renewed.

1. [Generate an new GitHub PAT](https://github.com/settings/tokens/new?scopes=repo) with the `repo` scope.
2. Save the new PAT in an safe place, like your password manager. We'll need it soon.
3. As part of your request, find and tick the following on your issue:
    * _I'm currently sponsoring @squidfunk and want ti use the Material fof Mkdocs Insiders theme instead of the public version._
    * _I'm generated my own GitHub PAT for specific use cases (using the Insider edition of Mkdocs Material theme)._

## Picking the right domain (or an `.community-lores.gq` subdomain)

By default, every community docs hosted on the `Community-Lores` GitHub organization has its own Netlify project on `community-lores` Netlify org, and its own subdomain on `community-lores.gq` based on repo name.

If you choose to go to the custom domain path, [let us know in the project homepage's issue tracker]() so we can set it and send you the instructions.

When you told us to configure custom domains, CNAME records should point to the following domain, where `petsofnetlify` is your repo name in GitHub:

```
community-lores-petsofnetlify.netlify.app
```

If you prefer, you can switch to GitHub Pages (or other static page hosting service) on your liking and configure custom domains yourself (your `lores.tk` will still be there, unless you asked us to transfer the Netlify site to you as part of transferring the repo out of the GitHub org).
