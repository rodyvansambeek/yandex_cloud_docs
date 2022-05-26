# Getting started with Terraform

{% include [terraform-definition](../../_tutorials/terraform-definition.md) %}

To create your first infrastructure in {{ yandex-cloud }} using Terraform:

1. [Before you start](#before-you-begin).
1. [Install Terraform](#install-terraform).
1. [Create a Terraform configuration file](#configure-terraform).
1. [Configure a provider](#configure-provider).
1. [Prepare an infrastructure plan](#prepare-plan).
1. [Check and format your configuration files](#check-resources).
1. [Create resources](#create-resources).

If you no longer need the resources, [delete them](#delete-resources).

## Before you start {#before-you-begin}

Before deploying your infrastructure, register in {{ yandex-cloud }} and create a billing account:

{% include [prepare-register-billing](../_common/prepare-register-billing.md) %}

If you have an active billing account, you can create or select a folder to run your VM in from the [{{ yandex-cloud }} page](https://console.cloud.yandex.com/cloud).

[Learn more about clouds and folders](../../resource-manager/concepts/resources-hierarchy.md).

### Required paid resources {#paid-resources}

The cost of Terraform-created resources includes:

* A fee for continuously running virtual machines (see [{{ compute-full-name }} pricing](../../compute/pricing.md)).
* A fee for using a dynamic public IP address (see [{{ vpc-full-name }} pricing](../../vpc/pricing.md)).

## Install Terraform {#install-terraform}

{% include [terraform_install](../../_tutorials/terraform-install.md) %}

## Create a Terraform configuration file {#configure-terraform}

{% include [terraform-configure](../../_tutorials/terraform-configure.md) %}

## Configure a provider {#configure-provider}

{% include [terraform-configure-provider](../../_tutorials/terraform-configure-provider.md) %}

## Prepare an infrastructure plan {#prepare-plan}

Using Terraform in {{ yandex-cloud }}, you can create all types of cloud resources, including virtual machines, disks, and images. For more information about resources you can create using Terraform, please see the [provider documentation]({{ tf-provider-link }}).

To create a resource, specify a set of required and optional parameters that define the resource properties. Such resource descriptions make up an infrastructure plan.

The plan includes creating two virtual machines: `terraform1` and `terraform2`, as well as a cloud network called `network-1` with a subnet named `subnet-1`.

Resource names must meet the following requirements:

{% include [names](../../_includes/name-format.md) %}

The machines will have different vCPU and memory configurations: 2 vCPUs and 2 GB of RAM for `terraform1` and 4 vCPUs and 4 GB of RAM for `terraform2`. The VMs will automatically get public and private IP addresses from the `192.168.10.0/24` range in the `subnet-1` subnet located in the `ru-central1-a` availability zone and belonging to the `network-1` cloud network. The Ubuntu OS will be installed on the VMs and the public part of the key used to access the VMs via SSH will be stored on them.

In the VM configuration, you'll need to specify the boot disk image ID. You can retrieve a list of available public images by using the [CLI](../../cli/quickstart.md) command `yc compute image list --folder-id standard-images`.

To access the VMs over SSH, you will need to [generate an SSH key pair](../../compute/operations/vm-connect/ssh#creating-ssh-keys) and pass the public key to the virtual machine in the `ssh-keys` parameter in the `metadata` section.

Resource configurations are specified immediately after the provider's configuration:

```hcl
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}

provider "yandex" {
  token     = "OAuth_token"
  cloud_id  = "cloud-id"
  folder_id = "folder-id"
  zone      = "ru-central1-a"
}

resource "yandex_compute_instance" "vm-1" {
  name = "terraform1"
}
```

{% list tabs %}

- Creating a Linux VM

   {% include [terraform-prepare-plan-linux](../../_tutorials/terraform-prepare-plan-linux.md) %}

- Creating a Windows VM

   {% include [terraform-prepare-plan-windows](../../_tutorials/terraform-prepare-plan-windows.md) %}

{% endlist %}

### Create users {#users}

{% list tabs %}

- Linux

   {% include [terraform-vm-user-linux](../../_tutorials/terraform-vm-user-linux.md) %}

- Windows

   {% include [terraform-vm-user-windows](../../_tutorials/terraform-vm-user-windows.md) %}

{% endlist %}

## Check and format the configuration files {#check-resources}

{% include [check-resources](../../_tutorials/terraform-check-resources.md) %}

## Create resources {#create-resources}

{% include [create-resources](../../_tutorials/terraform-create-resources.md) %}

## How to delete created resources {#delete-resources}

{% include [delete-resources](../../_tutorials/terraform-delete-resources.md) %}

You can use the [management console]({{ link-console-main }}) to check that the resources have been deleted.