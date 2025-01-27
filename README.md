# Terraform Provider for Git

This project is a fork of the provider from [Innovation Norway](https://github.com/innovationnorway-archive/terraform-provider-git).

No new development on the provider is planned at this time, but the build has been updated to include the Darwin ARM64 architecture to support the M-series Macs.

## Requirements

-	[Terraform](https://www.terraform.io/downloads.html) >= 1.5
-	[Go](https://golang.org/doc/install) >= 1.19

## Usage

```hcl
provider "git" {}

data "git_repository" "example" {
  path = path.root
}

resource "azurerm_resource_group" "example" {
  ...

  tags = {
    branch = data.git_repository.example.branch
    commit = substr(data.git_repository.example.commit_sha, 0, 7)
    tag    = data.git_repository.example.tag
  }
}
```
