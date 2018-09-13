---
title: Install MongoDB on a Linux VM with the Azure CLI 2.0 | Microsoft Docs
description: Learn how to install and configure MongoDB on a Linux virtual machine iusing the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: iainfou
ms.openlocfilehash: d621f50b2145782f915ae4dfd3f914b0baa949c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551683"
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a>How to install and configure MongoDB on a Linux VM
[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database. This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0. You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Examples are shown that detail how to:

* [Manually install and configure a basic MongoDB instance](#manually-install-and-configure-mongodb-on-a-vm)
* [Create a basic MongoDB instance using a Resource Manager template](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Manually install and configure MongoDB on a VM
MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian. The following example creates a `CentOS` VM using an SSH key stored at `~/.ssh/id_rsa.pub`. To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).

Create a resource group with [az group create](/cli/azure/group#create). The following example creates a resource group named `myResourceGroup` in the `West US` location:

```azurecli
 az group create --name myResourceGroup --location westus
```

Create a VM with [az vm create](/cli/azure/vm#create). The following example creates a VM named `myVM` with a user named `azureuser` using SSH public key authentication, and a public DNS entry of `mypublicdns`:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --public-ip-address-dns-name mypublicdns
```

Log on to the VM using the public DNS address of your VM. You can view the public DNS address with [az vm show](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH to your VM using your own username and public DNS address:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

To add the installation sources for MongoDB, create a `yum` repository file as follows:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.2.repo
```

Open the MongoDB repo file for editing. Add the following lines:

```sh
[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc
```

Install MongoDB using `yum` as follows:

```bash
sudo yum install -y mongodb-org
```

By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB. Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows. 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Start the MongoDB service as follows:

```bash
sudo service mongod start
```

Verify the MongoDB installation by connecting using the local `mongo` client:

```bash
mongo
```

Now test the MongoDB instance by adding some data and then searching:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

If desired, configure MongoDB to start automatically during a system reboot:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Create basic MongoDB instance on CentOS using a template
You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub. This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.

* [Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login). First, create a resource group with [az group create](/cli/azure/group#create). The following example creates a resource group named `myResourceGroup` in the `West US` location:

```azurecli
az group create --name myResourceGroup --location westus
```

Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create). Define your own resource names and sizes where needed such as for `newStorageAccountName`, `virtualNetworkName`, and `vmSize`:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

Log on to the VM using the public DNS address of your VM. You can view the public DNS address with [az vm show](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH to your VM using your own username and public DNS address:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Verify the MongoDB installation by connecting using the local `mongo` client as follows:

```bash
mongo
```

Now test the instance by adding some data and searching as follows:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Create a complex MongoDB Sharded Cluster on CentOS using a template
You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub. This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability. The template creates two shards, with three nodes in each replica set. One config server replica set with three nodes is also created, plus two `mongos` router servers to provide consistency to applications from across the shards.

* [MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription. Open an Azure support request to increase your core count.

To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login). First, create a resource group with [az group create](/cli/azure/group#create). The following example creates a resource group named `myResourceGroup` in the `West US` location:

```azurecli
az group create --name myResourceGroup --location westus
```

Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create). Define your own resource names and sizes where needed such as for `mongoAdminUsername`, `sizeOfDataDiskInGB`, and `configNodeVmSize`:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster --no-wait
```

This deployment can take over an hour to deploy and configure all the VM instances. The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform. You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show). The following example views the status for the `myMongoDBCluster` deployment in the `myResourceGroup` resource group:

```azurecli
az group deployment show --resource-group myResourceGroup --name myMongoDBCluster \
    --query [properties.provisioningState] --output tsv
```

## <a name="next-steps"></a>Next steps
In these examples, you connect to the MongoDB instance locally from the VM. If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).

The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs. For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

