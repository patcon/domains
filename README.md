# g0v.network domains

For automating management of the `g0v.network` domain via config files.

Changing or adding DNS records in `main` branach of this repository with update
the actual domain records.

Inspired by [`g0v/domain`][g0v/domain]

   [g0v/domain]: https://github.com/g0v/domain

**Note:** Work in progress. Not yet functional.

## Technologies Used

- [**octoDNS.**][octodns]

   [octodns]: https://github.com/octodns/octodns

## Usage

The intended way to use this repository is via pull request directly on GitHub.

(You should only need to clone this code locally in order to improve the
automation part of this repository. See Development section.)

### Create a new subdomain

Create a new YAML file, and fill it out. For example, to create
`my.example.g0v.network`, you'd create a config file with the full subdomain
name, with a key inside it for `my.example`. Like so (click through the link to
see example):

[`g0v.network./my.example.g0v.network.yaml`][new-subdomain]

   [new-subdomain]: https://github.com/g0v-network/domains/new/main?filename=g0v.network./my.example.g0v.network.yaml&value=my.example%3A%0A%20%20-%20type%3A%20A%0A%20%20%20%20value%3A%0A%20%20%20%20%20%20-%20123.45.67.89

### Delete an existing subdomain

Delete a file or a specific record type within a file. Our automation will sync this deletion when it runs.

### Modify an existing subdomain

Modify an [existing file][existing]. Our automation will sync this change when it runs.

   [existing]: /g0v.network./g0v.network.yaml

## Development

To contribute changes to our automation, you'll likely want to be able to run it locally. Here's what you'll need:

- Python 3
- Cloudflare account
- Cloudflare site: `g0v.network` (can "fake it", no need to actually have access to it)
- Cloudflare API token (see instructions in `sample.env`)

```
git clone https://github.com/g0v-network/domains
cd domains

brew install pipenv
pipenv install

# Copy and modify as needed with API token
cp sample.env .env

# Validate your config locally
pipenv run octodns-validate --config-file config.yaml

# Do a dry run (no changes will be made)
pipenv run octodns-sync --config-file config.yaml

# Do a REAL run (!!!)
#
# WARNING: this is destructive, and will delete any records on a domain that
# are not present in your configuration files.
pipenv run octodns-sync --config-file config.yaml --doit
```

## :muscle: Contributing

Please open an issue or pull request in order to apply for a new subdomain.

## :copyright: License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/)