# Community Lorebooks homepage

[![All Contributors](https://img.shields.io/github/all-contributors/lorebooks-wiki/homepage?color=ee8449&style=flat-square)](#contributors)

The homepage for `lorebooks.wiki` domain service itself, hosted on ~~Netlify~~
Cloudflare Pages, built with Mkdocs + Material theme. All of the documentation
sources are at the [`src` directory](./src/) including our [legal documents](./src/legal/)
and [documentation](./src/docs/).

## Local development

You might need to install `pipenv`, although we also generate static lockfiles at
`requirements.txt`

1. Install deps: `pipenv install` or `pip3 intall -r requirements.txt`
2. Run localdev server: `pipenv run mkdocs serve`
3. Edit as usual

## License

* Code: [`MPL-2.0`](./LICENSE-MPL-2.0)
* Documentation: [`CC-BY-SA-4.0`](./LICENSE-CC-BY-SA-4.0)
