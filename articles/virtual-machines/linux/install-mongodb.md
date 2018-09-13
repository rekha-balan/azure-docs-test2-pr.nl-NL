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
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="bac7b-103">How to install and configure MongoDB on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="bac7b-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="bac7b-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span><span class="sxs-lookup"><span data-stu-id="bac7b-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="bac7b-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="bac7b-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="bac7b-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bac7b-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="bac7b-107">Examples are shown that detail how to:</span><span class="sxs-lookup"><span data-stu-id="bac7b-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="bac7b-108">Manually install and configure a basic MongoDB instance</span><span class="sxs-lookup"><span data-stu-id="bac7b-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="bac7b-109">Create a basic MongoDB instance using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="bac7b-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="bac7b-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="bac7b-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="bac7b-111">Manually install and configure MongoDB on a VM</span><span class="sxs-lookup"><span data-stu-id="bac7b-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="bac7b-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span><span class="sxs-lookup"><span data-stu-id="bac7b-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="bac7b-113">The following example creates a `CentOS` VM using an SSH key stored at `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="bac7b-113">The following example creates a `CentOS` VM using an SSH key stored at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="bac7b-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bac7b-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="bac7b-115">Create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bac7b-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bac7b-116">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span><span class="sxs-lookup"><span data-stu-id="bac7b-116">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span></span>

```azurecli
 az group create --name myResourceGroup --location westus
```

<span data-ttu-id="bac7b-117">Create a VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bac7b-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bac7b-118">The following example creates a VM named `myVM` with a user named `azureuser` using SSH public key authentication, and a public DNS entry of `mypublicdns`:</span><span class="sxs-lookup"><span data-stu-id="bac7b-118">The following example creates a VM named `myVM` with a user named `azureuser` using SSH public key authentication, and a public DNS entry of `mypublicdns`:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --public-ip-address-dns-name mypublicdns
```

<span data-ttu-id="bac7b-119">Log on to the VM using the public DNS address of your VM.</span><span class="sxs-lookup"><span data-stu-id="bac7b-119">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="bac7b-120">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="bac7b-120">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="bac7b-121">SSH to your VM using your own username and public DNS address:</span><span class="sxs-lookup"><span data-stu-id="bac7b-121">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="bac7b-122">To add the installation sources for MongoDB, create a `yum` repository file as follows:</span><span class="sxs-lookup"><span data-stu-id="bac7b-122">To add the installation sources for MongoDB, create a `yum` repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.2.repo
```

<span data-ttu-id="bac7b-123">Open the MongoDB repo file for editing.</span><span class="sxs-lookup"><span data-stu-id="bac7b-123">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="bac7b-124">Add the following lines:</span><span class="sxs-lookup"><span data-stu-id="bac7b-124">Add the following lines:</span></span>

```sh
[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc
```

<span data-ttu-id="bac7b-125">Install MongoDB using `yum` as follows:</span><span class="sxs-lookup"><span data-stu-id="bac7b-125">Install MongoDB using `yum` as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="bac7b-126">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bac7b-126">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="bac7b-127">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span><span class="sxs-lookup"><span data-stu-id="bac7b-127">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="bac7b-128">Start the MongoDB service as follows:</span><span class="sxs-lookup"><span data-stu-id="bac7b-128">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="bac7b-129">Verify the MongoDB installation by connecting using the local `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="bac7b-129">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="bac7b-130">Now test the MongoDB instance by adding some data and then searching:</span><span class="sxs-lookup"><span data-stu-id="bac7b-130">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="bac7b-131">If desired, configure MongoDB to start automatically during a system reboot:</span><span class="sxs-lookup"><span data-stu-id="bac7b-131">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="bac7b-132">Create basic MongoDB instance on CentOS using a template</span><span class="sxs-lookup"><span data-stu-id="bac7b-132">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="bac7b-133">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="bac7b-133">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="bac7b-134">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bac7b-134">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="bac7b-135">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="bac7b-135">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="bac7b-136">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bac7b-136">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="bac7b-137">First, create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bac7b-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bac7b-138">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span><span class="sxs-lookup"><span data-stu-id="bac7b-138">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="bac7b-139">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="bac7b-139">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="bac7b-140">Define your own resource names and sizes where needed such as for `newStorageAccountName`, `virtualNetworkName`, and `vmSize`:</span><span class="sxs-lookup"><span data-stu-id="bac7b-140">Define your own resource names and sizes where needed such as for `newStorageAccountName`, `virtualNetworkName`, and `vmSize`:</span></span>

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

<span data-ttu-id="bac7b-141">Log on to the VM using the public DNS address of your VM.</span><span class="sxs-lookup"><span data-stu-id="bac7b-141">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="bac7b-142">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="bac7b-142">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="bac7b-143">SSH to your VM using your own username and public DNS address:</span><span class="sxs-lookup"><span data-stu-id="bac7b-143">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="bac7b-144">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span><span class="sxs-lookup"><span data-stu-id="bac7b-144">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="bac7b-145">Now test the instance by adding some data and searching as follows:</span><span class="sxs-lookup"><span data-stu-id="bac7b-145">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="bac7b-146">Create a complex MongoDB Sharded Cluster on CentOS using a template</span><span class="sxs-lookup"><span data-stu-id="bac7b-146">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="bac7b-147">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="bac7b-147">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="bac7b-148">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span><span class="sxs-lookup"><span data-stu-id="bac7b-148">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="bac7b-149">The template creates two shards, with three nodes in each replica set.</span><span class="sxs-lookup"><span data-stu-id="bac7b-149">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="bac7b-150">One config server replica set with three nodes is also created, plus two `mongos` router servers to provide consistency to applications from across the shards.</span><span class="sxs-lookup"><span data-stu-id="bac7b-150">One config server replica set with three nodes is also created, plus two `mongos` router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="bac7b-151">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="bac7b-151">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="bac7b-152">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span><span class="sxs-lookup"><span data-stu-id="bac7b-152">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="bac7b-153">Open an Azure support request to increase your core count.</span><span class="sxs-lookup"><span data-stu-id="bac7b-153">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="bac7b-154">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bac7b-154">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="bac7b-155">First, create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bac7b-155">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bac7b-156">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span><span class="sxs-lookup"><span data-stu-id="bac7b-156">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="bac7b-157">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="bac7b-157">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="bac7b-158">Define your own resource names and sizes where needed such as for `mongoAdminUsername`, `sizeOfDataDiskInGB`, and `configNodeVmSize`:</span><span class="sxs-lookup"><span data-stu-id="bac7b-158">Define your own resource names and sizes where needed such as for `mongoAdminUsername`, `sizeOfDataDiskInGB`, and `configNodeVmSize`:</span></span>

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

<span data-ttu-id="bac7b-159">This deployment can take over an hour to deploy and configure all the VM instances.</span><span class="sxs-lookup"><span data-stu-id="bac7b-159">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="bac7b-160">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="bac7b-160">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="bac7b-161">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="bac7b-161">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="bac7b-162">The following example views the status for the `myMongoDBCluster` deployment in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="bac7b-162">The following example views the status for the `myMongoDBCluster` deployment in the `myResourceGroup` resource group:</span></span>

```azurecli
az group deployment show --resource-group myResourceGroup --name myMongoDBCluster \
    --query [properties.provisioningState] --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="bac7b-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="bac7b-163">Next steps</span></span>
<span data-ttu-id="bac7b-164">In these examples, you connect to the MongoDB instance locally from the VM.</span><span class="sxs-lookup"><span data-stu-id="bac7b-164">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="bac7b-165">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bac7b-165">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bac7b-166">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bac7b-166">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="bac7b-167">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span><span class="sxs-lookup"><span data-stu-id="bac7b-167">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="bac7b-168">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bac7b-168">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

