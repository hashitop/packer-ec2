# Packer - EC2

This project provides basic template for building an AWS AMI Image with nginx package installed

## Download Packer

Packer installer can be downloaded from this [page](https://www.packer.io/downloads.html)

## Install Packer

Here is [install instructions](https://www.packer.io/intro/getting-started/install.html#precompiled-binaries) for pre-compiled binary

## Build AMI Image

Running build command:

`packer build template.json`

## What's in template.json?

The [template.json](template.json) is packer file with descriptive resources.
It supports various components as per [Template Structure](https://www.packer.io/docs/templates/index.html#template-structure) document.
In this sample, it declares `variables` to demonstrate configurable pieces of information and the `builders` to perform build task(s) to build a machine with specific `type`, in this case `amazon-ebs`.

**Provisioners**
Provisioners will be used to perform additional tasks on the machine created by the builders such as install and configure software.
With this mini-sample, it uses `shell` provisioner with external script, `scripts/provision.sh`, to install `nginx` package.

```
  "provisioners": [
    {
      "script": "scripts/provision.sh",
      "type": "shell"
    }
  ],
```

## Running Test

The file `.kitchen.yml` provides brief demonstration of `ec2` driver from `kitchen-ec2` module.

### Prerequisites

- AWS key-pair
- AWS AMI Image

### Converge

Converge will perform environment preparation task where it runs up the machine.

`kitchen converge`

### Verify

Verify will perform verification task using `test/integration/default/default_test.rb` using the following command:

`kitchen verify`

### Destroy

Clean up test environment by running `destroy` command:

`kitchen destroy`

### Full test

Alternatively, running a single `test` command for full test cycle:

`kitchen test`
