# commercetools Terraform Provider

This is the Terraform provider for commercetools. It allows you to configure
your [commercetools](https://commercetools.com/) project with
infrastructure-as-code principles. The project is in development and it might
not support the complete commercetools API yet, but it can be considered
'production' ready for the resource it does support.

# Installation

## Terraform registry

Terraform 0.13 added support for automatically downloading providers from
the terraform registry. Add the following to your terraform project

```hcl
terraform {
  required_providers {
    commercetools = {
      source = "AdikaStyle/commercetools"
    }
  }
}
```

## Binaries

Packages of the releases are available at
https://github.com/AdikaStyle/terraform-provider-commercetools/releases See the
[terraform documentation](https://www.terraform.io/docs/configuration/providers.html#third-party-plugins)
for more information about installing third-party providers.

# Getting started

[Read our documentation](https://readthedocs.org/projects/commercetools-terraform-provider)
and check out the [examples](https://commercetools-terraform-provider.readthedocs.io/en/latest/examples/).

# Contributing

## Building the provider

Clone repository to: `$GOPATH/src/github.com/AdikaStyle/terraform-provider-commercetools`

```sh
$ mkdir -p $GOPATH/src/github.com/AdikaStyle; cd $GOPATH/src/github.com/AdikaStyle
$ git clone git@github.com:AdikaStyle/terraform-provider-commercetools
```

Enter the provider directory and build the provider

```sh
$ cd $GOPATH/src/github.com/AdikaStyle/terraform-provider-commercetools
$ make build
```

To then locally test:

```sh
$ cp terraform-provider-commercetools ~/.terraform.d/plugins/darwin_amd64/terraform-provider-commercetools
```

### Update commercetools-go-sdk

The commercetools-go-sdk always uses the latest (master) version. To update to
the latest version:

```sh
make update-sdk
```

## Debugging / Troubleshooting

There are two environment settings for troubleshooting:

- `TF_LOG=1` enables debug output for Terraform.
- `CTP_DEBUG=1` enables debug output for the Commercetools GO SDK this provider uses.

Note this generates a lot of output!

## Releasing

When pushing a new tag prefixed with `v` a GitHub action will automatically
use Goreleaser to build and release the build.

```sh
git tag <release> -m "Release <release>" # please use semantic version, so always vX.Y.Z
git push --follow-tags
```

## Testing

### Running the unit tests

```sh
$ make test
```

### Running an Acceptance Test

In order to run the full suite of Acceptance tests, run `make testacc`.

**NOTE:** Acceptance tests create real resources.

Prior to running the tests provider configuration details such as access keys
must be made available as environment variables.

Since we need to be able to create commercetools resources, we need the
commercetools API credentials. So in order for the acceptance tests to run
correctly please provide all of the following:

```sh
export CTP_CLIENT_ID=...
export CTP_CLIENT_SECRET=...
export CTP_PROJECT_KEY=...
export CTP_SCOPES=...
```

For convenience, place a `testenv.sh` in your `local` folder (which is
included in .gitignore) where you can store these environment variables.

Tests can then be started by running

```sh
$ source local/testenv.sh
$ make testacc
```

