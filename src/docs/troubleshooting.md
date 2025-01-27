# Troubleshooting your `lorebooks.wiki` subdomain

Here are some troubleshooting documentation to frequently asked questions
regarding errors you may experience about your subdomain.

## General

### CNAME values require a trailing dot

This is DNS by design for the uninitiated, as prompted by this octoDNS error on
the CI test logs for `pipenv run dns-dryrun`. To fix it, just add the trailing dot
into the value of your DNS record.

### My DNS record updates got merged, but why it is still not yet propagated?

There's a possibility that the `merge-records` script is having a hiccup (e.g. either
on octoDNS or Cloudflare API side) or GitHub Actions is experiencing issues at the
moment. It will run again on next commit to the `dns/partials` directory unless
manually triggered by an maintainer or someone with access to the secrets via
Doppler CLI.

## GitHub Pages

### I got a error that says I need to verify my subdomain in order to use it as custom domain.

**Error message**: You must verify your domain your-domain-here.lorebooks.wiki before being able to use it. Check out https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages for more information.

To prevent abuse, we verified `beta.lorebooks.wiki` and `lorebooks.wiki` to the
@lorebooks-wiki GitHub organization, which requires you to do this.

If you want to use GitHub Pages, you need to verify your `lorebooks.wiki`
subdomain against your GitHub account or organization first. ([see example config](./setup/dns-records.md/#__tabbed_2_3))
