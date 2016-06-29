Azure Deployment
================

Azure deployment template to deploy a 2-tier architecture (private + public subnets).
Resources are deployed using the [ARM](https://azure.microsoft.com/en-in/documentation/articles/resource-group-overview/) API.

## TODO

* Upgrade configuration to use YAML
* Generate `azuredeploy.parameters.json` from a YAML configuration
* Use resource count to specify number of resources
* Allow configurable subnets (address spaces, prefixes and names)
* Allow configurable ports exposed from the Load Balancer

## Requirements

* [Node](https://nodejs.org/en/) (v5.0+)
* [Azure Xplat-CLI](https://github.com/Azure/azure-xplat-cli) (v0.9+)

## Setup

#### Login to Azure account
```
$ azure login
```

#### Configure ARM mode
```
$ azure config set mode arm
```

#### Configure subscription

```
$ azure account set <YourSubscription>
```

The chosen subscription will be billed when provisioning any resources after
this configuration.

## Deploy

#### Create a resource group
```
$ azure group create -n my_resource_group -l west_us
```
This will deploy a resource group (container for all your resources) by the name
`my_resource_group` in the location `west_us`.

Use the `example.parameters.json` as a reference to add your SSH public Key,
a list of private and public VMs into a new file called `azuredeploy.parameters.json`.

**NOTE**: Current template only contains two subnets (`public` and `app`).
They will be configurable in future releases.

#### Deploy to resource group
```
$ azure group deployment create \
  -f azuredeploy.json \
  -e azuredeploy.parameters.json \
  -g my_resource_group \
  -n my_new_deployment
```

#### Delete resource group

```
$ azure group delete my_resource_group
```

This will delete all resources provisioned under `my_resource_group`.

## Contribution

* Found an issue? Please open a [new issue](https://github.com/activatedgeek/azure-deploy/issues/new).

* Want to help me add features? Fork, commit and submit pull request! ;-).
