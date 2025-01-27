---
title: Subdomain Registry
description: Learn more about our subdomain registry and how it is managed.
---

# Subdomain registry

Unlike `is-a.dev` and Open Domains where subdomain ownership data is coupled with
DNS records in one JSON file per subdomain, we chose to seperate them from the
underlying DNS records to seperate concerns without having to maintain additional
code parsing them and do the DNS management work (we use octoDNS for YAML-based
DNS records as code).

## Where they are managed?

Subdomain registry data are stored and managed as good old YAML files in the
[`data` directory](https://github.com/lorebooks-wiki/registry/tree/main/data)

## API Docs

API documentation for the registry is available at <https://api.lorebooks.wiki/docs>
([source code](https://github.com/lorebooks-wiki/registry/tree/main/api)).
