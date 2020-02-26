Terraform Provider for Git
==================

[![Build Status](https://travis-ci.com/volcano-coffee-company/terraform-provider-git.svg?branch=master)](https://travis-ci.com/volcano-coffee-company/terraform-provider-git)

<img src="https://cdn.rawgit.com/hashicorp/terraform-website/master/content/source/assets/images/logo-hashicorp.svg" width="600px">

Requirements
------------

-	[Terraform](https://www.terraform.io/downloads.html) 0.12.x
-	[Go](https://golang.org/doc/install) 1.13

Building The Provider
---------------------

Clone repository to: `$GOPATH/src/github.com/volcano-coffee-company/terraform-provider-git`

```sh
$ mkdir -p $GOPATH/src/github.com/volcano-coffee-company; cd $GOPATH/src/github.com/volcano-coffee-company
$ git clone https://github.com/volcano-coffee-company/terraform-provider-git.git
```

Enter the provider directory and build the provider

```sh
$ cd $GOPATH/src/github.com/volcano-coffee-company/terraform-provider-git
$ make build
```

Using the provider
----------------------

```hcl
provider "git" {}

data "git_repository" "example" {
  path = path.root
}

resource "aws_vpc" "example" {
  ...

  tags = {
    branch = data.git_repository.example.branch
    commit = substr(data.git_repository.example.commit_sha, 0, 7)
    tag    = data.git_repository.example.tag
  }
}
```

Developing the Provider
---------------------------

If you wish to work on the provider, you'll first need [Go](http://www.golang.org) installed on your machine (version 1.13+ is *required*). You'll also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `$GOPATH/bin` to your `$PATH`.

To compile the provider, run `make build`. This will build the provider and put the provider binary in the `$GOPATH/bin` directory.

```sh
$ make bin
...
$ $GOPATH/bin/terraform-provider-git
...
```

In order to test the provider, you can simply run `make test`.

```sh
$ make test
```

In order to run the full suite of Acceptance tests, run `make testacc`.

*Note:* Acceptance tests create real resources, and often cost money to run.

```sh
$ make testacc
```
