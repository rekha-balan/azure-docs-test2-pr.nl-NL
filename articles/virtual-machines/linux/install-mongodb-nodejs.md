---
title: Install MongoDB on a Linux VM using the Azure CLI 1.0 | Microsoft Docs
description: Learn how to install and configure MongoDB on a Linux virtual machine in Azure using the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/20/2016
ms.author: iainfou
ms.openlocfilehash: 253eabc5ce872497d0d3207b735db57423ac45b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550013"
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="6ad21-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6ad21-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="6ad21-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span><span class="sxs-lookup"><span data-stu-id="6ad21-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="6ad21-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="6ad21-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="6ad21-106">Examples are shown that detail how to:</span><span class="sxs-lookup"><span data-stu-id="6ad21-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="6ad21-107">Manually install and configure a basic MongoDB instance</span><span class="sxs-lookup"><span data-stu-id="6ad21-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="6ad21-108">Create a basic MongoDB instance using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="6ad21-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="6ad21-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="6ad21-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6ad21-110">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="6ad21-110">CLI versions to complete the task</span></span>
<span data-ttu-id="6ad21-111">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="6ad21-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6ad21-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="6ad21-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6ad21-113">[Azure CLI 2.0](create-cli-complete-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="6ad21-113">[Azure CLI 2.0](create-cli-complete-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="6ad21-114">Manually install and configure MongoDB on a VM</span><span class="sxs-lookup"><span data-stu-id="6ad21-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="6ad21-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span><span class="sxs-lookup"><span data-stu-id="6ad21-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="6ad21-116">The following example creates a `CentOS` VM using an SSH key stored at `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="6ad21-116">The following example creates a `CentOS` VM using an SSH key stored at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="6ad21-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span><span class="sxs-lookup"><span data-stu-id="6ad21-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create --ssh-publickey-file ~/.ssh/id_rsa.pub --image-urn CentOS
```

<span data-ttu-id="6ad21-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span><span class="sxs-lookup"><span data-stu-id="6ad21-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="6ad21-119">To add the installation sources for MongoDB, create a `yum` repository file as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-119">To add the installation sources for MongoDB, create a `yum` repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.2.repo
```

<span data-ttu-id="6ad21-120">Open the MongoDB repo file for editing.</span><span class="sxs-lookup"><span data-stu-id="6ad21-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="6ad21-121">Add the following lines:</span><span class="sxs-lookup"><span data-stu-id="6ad21-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc
```

<span data-ttu-id="6ad21-122">Install MongoDB using `yum` as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-122">Install MongoDB using `yum` as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="6ad21-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6ad21-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="6ad21-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span><span class="sxs-lookup"><span data-stu-id="6ad21-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="6ad21-125">Start the MongoDB service as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="6ad21-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="6ad21-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="6ad21-127">Now test the MongoDB instance by adding some data and then searching:</span><span class="sxs-lookup"><span data-stu-id="6ad21-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="6ad21-128">If desired, configure MongoDB to start automatically during a system reboot:</span><span class="sxs-lookup"><span data-stu-id="6ad21-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="6ad21-129">Create basic MongoDB instance on CentOS using a template</span><span class="sxs-lookup"><span data-stu-id="6ad21-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="6ad21-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="6ad21-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="6ad21-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6ad21-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="6ad21-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6ad21-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="6ad21-133">The following example creates a resource group with the name `myResourceGroup` in the `WestUS` region.</span><span class="sxs-lookup"><span data-stu-id="6ad21-133">The following example creates a resource group with the name `myResourceGroup` in the `WestUS` region.</span></span> <span data-ttu-id="6ad21-134">Enter your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-134">Enter your own values as follows:</span></span>

```azurecli
azure group create --name myResourceGroup --location WestUS \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="6ad21-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6ad21-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="6ad21-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span><span class="sxs-lookup"><span data-stu-id="6ad21-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="6ad21-137">Wait until the `ProvisioningState` shows 'Succeeded' before trying to SSH to the VM.</span><span class="sxs-lookup"><span data-stu-id="6ad21-137">Wait until the `ProvisioningState` shows 'Succeeded' before trying to SSH to the VM.</span></span>
> 
> 

<span data-ttu-id="6ad21-138">Once the deployment is complete, SSH to the VM.</span><span class="sxs-lookup"><span data-stu-id="6ad21-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="6ad21-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span><span class="sxs-lookup"><span data-stu-id="6ad21-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="6ad21-140">Near the end of the output, the `Public IP address` is displayed.</span><span class="sxs-lookup"><span data-stu-id="6ad21-140">Near the end of the output, the `Public IP address` is displayed.</span></span> <span data-ttu-id="6ad21-141">SSH to your VM with the IP address of your VM:</span><span class="sxs-lookup"><span data-stu-id="6ad21-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="6ad21-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="6ad21-143">Now test the instance by adding some data and searching as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="6ad21-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span><span class="sxs-lookup"><span data-stu-id="6ad21-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="6ad21-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="6ad21-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="6ad21-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span><span class="sxs-lookup"><span data-stu-id="6ad21-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="6ad21-147">The template creates two shards, with three nodes in each replica set.</span><span class="sxs-lookup"><span data-stu-id="6ad21-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="6ad21-148">One config server replica set with three nodes is also created, plus two `mongos` router servers to provide consistency to applications from across the shards.</span><span class="sxs-lookup"><span data-stu-id="6ad21-148">One config server replica set with three nodes is also created, plus two `mongos` router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="6ad21-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6ad21-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="6ad21-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span><span class="sxs-lookup"><span data-stu-id="6ad21-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="6ad21-151">Open an Azure support request to increase your core count.</span><span class="sxs-lookup"><span data-stu-id="6ad21-151">Open an Azure support request to increase your core count.</span></span>
> 
> 

<span data-ttu-id="6ad21-152">The following example creates a resource group with the name `myResourceGroup` in the `WestUS` region.</span><span class="sxs-lookup"><span data-stu-id="6ad21-152">The following example creates a resource group with the name `myResourceGroup` in the `WestUS` region.</span></span> <span data-ttu-id="6ad21-153">Enter your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="6ad21-153">Enter your own values as follows:</span></span>

```azurecli
azure group create --name myResourceGroup --location WestUS \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="6ad21-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span><span class="sxs-lookup"><span data-stu-id="6ad21-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="6ad21-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span><span class="sxs-lookup"><span data-stu-id="6ad21-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="6ad21-156">Wait until the `ProvisioningState` shows 'Succeeded' before connecting to the VMs.</span><span class="sxs-lookup"><span data-stu-id="6ad21-156">Wait until the `ProvisioningState` shows 'Succeeded' before connecting to the VMs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6ad21-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ad21-157">Next steps</span></span>
<span data-ttu-id="6ad21-158">In these examples, you connect to the MongoDB instance locally from the VM.</span><span class="sxs-lookup"><span data-stu-id="6ad21-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="6ad21-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ad21-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6ad21-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ad21-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="6ad21-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span><span class="sxs-lookup"><span data-stu-id="6ad21-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="6ad21-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ad21-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

