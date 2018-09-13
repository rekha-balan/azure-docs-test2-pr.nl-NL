---
title: Install MongoDB on a Linux VM with the Azure CLI | Microsoft Docs
description: Learn how to install and configure MongoDB on a Linux virtual machine iusing the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2017
ms.author: cynthn
ms.openlocfilehash: dd42b9509c0ec819973686563c1a61539f6d9072
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809288"
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="ad8ec-103">How to install and configure MongoDB on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="ad8ec-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="ad8ec-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="ad8ec-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="ad8ec-106">Examples are shown that detail how to:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="ad8ec-107">Manually install and configure a basic MongoDB instance</span><span class="sxs-lookup"><span data-stu-id="ad8ec-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="ad8ec-108">Create a basic MongoDB instance using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="ad8ec-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="ad8ec-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="ad8ec-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="ad8ec-110">Manually install and configure MongoDB on a VM</span><span class="sxs-lookup"><span data-stu-id="ad8ec-110">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="ad8ec-111">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-111">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="ad8ec-112">The following example creates a *CentOS* VM.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-112">The following example creates a *CentOS* VM.</span></span> <span data-ttu-id="ad8ec-113">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-113">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="ad8ec-114">Create a resource group with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-114">Create a resource group with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="ad8ec-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ad8ec-116">Create a VM with [az vm create](/cli/azure/vm#az_vm_create).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-116">Create a VM with [az vm create](/cli/azure/vm#az_vm_create).</span></span> <span data-ttu-id="ad8ec-117">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span><span class="sxs-lookup"><span data-stu-id="ad8ec-117">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ad8ec-118">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-118">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="ad8ec-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.6.repo
```

<span data-ttu-id="ad8ec-120">Open the MongoDB repo file for editing, such as with `vi` or `nano`.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-120">Open the MongoDB repo file for editing, such as with `vi` or `nano`.</span></span> <span data-ttu-id="ad8ec-121">Add the following lines:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
```

<span data-ttu-id="ad8ec-122">Install MongoDB using **yum** as follows:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="ad8ec-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="ad8ec-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="ad8ec-125">Start the MongoDB service as follows:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="ad8ec-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="ad8ec-127">Now test the MongoDB instance by adding some data and then searching:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="ad8ec-128">If desired, configure MongoDB to start automatically during a system reboot:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="ad8ec-129">Create basic MongoDB instance on CentOS using a template</span><span class="sxs-lookup"><span data-stu-id="ad8ec-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="ad8ec-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="ad8ec-131">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-131">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="ad8ec-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="ad8ec-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="ad8ec-133">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-133">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span> <span data-ttu-id="ad8ec-134">First, create a resource group with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-134">First, create a resource group with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="ad8ec-135">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-135">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ad8ec-136">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-136">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create).</span></span> <span data-ttu-id="ad8ec-137">When prompted, enter your own unique values for *newStorageAccountName*, *dnsNameForPublicIP*, and admin username and password:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-137">When prompted, enter your own unique values for *newStorageAccountName*, *dnsNameForPublicIP*, and admin username and password:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="ad8ec-138">Log on to the VM using the public DNS address of your VM.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-138">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="ad8ec-139">You can view the public DNS address with [az vm show](/cli/azure/vm#az_vm_show):</span><span class="sxs-lookup"><span data-stu-id="ad8ec-139">You can view the public DNS address with [az vm show](/cli/azure/vm#az_vm_show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myLinuxVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="ad8ec-140">SSH to your VM using your own username and public DNS address:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-140">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="ad8ec-141">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-141">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="ad8ec-142">Now test the instance by adding some data and searching as follows:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-142">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="ad8ec-143">Create a complex MongoDB Sharded Cluster on CentOS using a template</span><span class="sxs-lookup"><span data-stu-id="ad8ec-143">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="ad8ec-144">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-144">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="ad8ec-145">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-145">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="ad8ec-146">The template creates two shards, with three nodes in each replica set.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-146">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="ad8ec-147">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-147">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="ad8ec-148">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="ad8ec-148">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="ad8ec-149">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-149">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="ad8ec-150">Open an Azure support request to increase your core count.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-150">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="ad8ec-151">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-151">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span> <span data-ttu-id="ad8ec-152">First, create a resource group with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-152">First, create a resource group with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="ad8ec-153">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-153">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ad8ec-154">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-154">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create).</span></span> <span data-ttu-id="ad8ec-155">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-155">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="ad8ec-156">This deployment can take over an hour to deploy and configure all the VM instances.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-156">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="ad8ec-157">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-157">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="ad8ec-158">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#az_group_deployment_show).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-158">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#az_group_deployment_show).</span></span> <span data-ttu-id="ad8ec-159">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span><span class="sxs-lookup"><span data-stu-id="ad8ec-159">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="ad8ec-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad8ec-160">Next steps</span></span>
<span data-ttu-id="ad8ec-161">In these examples, you connect to the MongoDB instance locally from the VM.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-161">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="ad8ec-162">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-162">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="ad8ec-163">These examples deploy the core MongoDB environment for development purposes.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-163">These examples deploy the core MongoDB environment for development purposes.</span></span> <span data-ttu-id="ad8ec-164">Apply the required security configuration options for your environment.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-164">Apply the required security configuration options for your environment.</span></span> <span data-ttu-id="ad8ec-165">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-165">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="ad8ec-166">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-166">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="ad8ec-167">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span><span class="sxs-lookup"><span data-stu-id="ad8ec-167">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="ad8ec-168">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="ad8ec-168">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

