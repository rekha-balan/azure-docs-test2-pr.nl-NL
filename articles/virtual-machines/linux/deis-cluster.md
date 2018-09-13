---
title: Deploy a 3-node Deis cluster | Microsoft Docs
description: This article describes how to create a 3-node Deis cluster on Azure using an Azure Resource Manager template
services: virtual-machines-linux
documentationcenter: ''
author: HaishiBai
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba9fb1306f7c9b2dfdcc874b76a084599faa483e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555195"
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="41b3a-103">Deploy and configure a 3-node Deis cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="41b3a-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="41b3a-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span><span class="sxs-lookup"><span data-stu-id="41b3a-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="41b3a-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="41b3a-106">The following diagram shows the architecture of the deployed system.</span><span class="sxs-lookup"><span data-stu-id="41b3a-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="41b3a-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="41b3a-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="41b3a-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="41b3a-109">The clients access deployed applications through the load balancer as well.</span><span class="sxs-lookup"><span data-stu-id="41b3a-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="41b3a-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![Architecture diagram of deployed Desis cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deis-cluster/architecture-overview.png)

<span data-ttu-id="41b3a-112">In order to run through the following steps, you'll need:</span><span class="sxs-lookup"><span data-stu-id="41b3a-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="41b3a-113">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="41b3a-113">An active Azure subscription.</span></span> <span data-ttu-id="41b3a-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="41b3a-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="41b3a-115">A work or school id to use Azure resource groups.</span><span class="sxs-lookup"><span data-stu-id="41b3a-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="41b3a-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="41b3a-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="41b3a-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="41b3a-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="41b3a-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="41b3a-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="41b3a-119">OpenSSL is used to generate the necessary certificates.</span><span class="sxs-lookup"><span data-stu-id="41b3a-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="41b3a-120">A Git client such as [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="41b3a-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="41b3a-121">To test the sample application, you'll also need a DNS server.</span><span class="sxs-lookup"><span data-stu-id="41b3a-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="41b3a-122">You can use any DNS servers or services that support wildcard A records.</span><span class="sxs-lookup"><span data-stu-id="41b3a-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="41b3a-123">A computer to run Deis client tools.</span><span class="sxs-lookup"><span data-stu-id="41b3a-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="41b3a-124">You can use either a local machine or a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="41b3a-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="41b3a-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="41b3a-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="41b3a-126">Provision the cluster</span><span class="sxs-lookup"><span data-stu-id="41b3a-126">Provision the cluster</span></span>
<span data-ttu-id="41b3a-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="41b3a-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="41b3a-128">First, you'll copy down the template.</span><span class="sxs-lookup"><span data-stu-id="41b3a-128">First, you'll copy down the template.</span></span> <span data-ttu-id="41b3a-129">Then, you'll create a new SSH key pair for authentication.</span><span class="sxs-lookup"><span data-stu-id="41b3a-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="41b3a-130">And then, you'll configure a new identifier for you cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="41b3a-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="41b3a-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="41b3a-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="41b3a-133">Go to the template folder:</span><span class="sxs-lookup"><span data-stu-id="41b3a-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="41b3a-134">Create a new SSH key pair using ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="41b3a-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="41b3a-135">Generate a certificate using the above private key:</span><span class="sxs-lookup"><span data-stu-id="41b3a-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="41b3a-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span><span class="sxs-lookup"><span data-stu-id="41b3a-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="41b3a-137">Each CoreOS cluster needs to have a unique token from this free service.</span><span class="sxs-lookup"><span data-stu-id="41b3a-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="41b3a-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span><span class="sxs-lookup"><span data-stu-id="41b3a-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="41b3a-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span><span class="sxs-lookup"><span data-stu-id="41b3a-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="41b3a-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span><span class="sxs-lookup"><span data-stu-id="41b3a-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="41b3a-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span><span class="sxs-lookup"><span data-stu-id="41b3a-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="41b3a-142">Modify the **newStorageAccountName** parameter.</span><span class="sxs-lookup"><span data-stu-id="41b3a-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="41b3a-143">This is the storage account for VM OS disks.</span><span class="sxs-lookup"><span data-stu-id="41b3a-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="41b3a-144">This account name has to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="41b3a-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="41b3a-145">Modify the **publicDomainName** parameter.</span><span class="sxs-lookup"><span data-stu-id="41b3a-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="41b3a-146">This will become part of the DNS name associated with the load balancer public IP.</span><span class="sxs-lookup"><span data-stu-id="41b3a-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="41b3a-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="41b3a-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="41b3a-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="41b3a-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="41b3a-149">Save the parameter file.</span><span class="sxs-lookup"><span data-stu-id="41b3a-149">Save the parameter file.</span></span> <span data-ttu-id="41b3a-150">And then you can provision the cluster using Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41b3a-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="41b3a-151">or Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="41b3a-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="41b3a-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="41b3a-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="41b3a-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span><span class="sxs-lookup"><span data-stu-id="41b3a-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="41b3a-154">The group also contains a load balancer, which has an associated public IP.</span><span class="sxs-lookup"><span data-stu-id="41b3a-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![The provisioned resource group on Azure classic portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="41b3a-156">Install the client</span><span class="sxs-lookup"><span data-stu-id="41b3a-156">Install the client</span></span>
<span data-ttu-id="41b3a-157">You need **deisctl** to control your Deis cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="41b3a-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span><span class="sxs-lookup"><span data-stu-id="41b3a-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="41b3a-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span><span class="sxs-lookup"><span data-stu-id="41b3a-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="41b3a-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="41b3a-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="41b3a-161">Install deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="41b3a-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="41b3a-162">Add your private key to ssh agent:</span><span class="sxs-lookup"><span data-stu-id="41b3a-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="41b3a-163">Configure deisctl:</span><span class="sxs-lookup"><span data-stu-id="41b3a-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="41b3a-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span><span class="sxs-lookup"><span data-stu-id="41b3a-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="41b3a-165">This provides redundancy for using the deisctl tool.</span><span class="sxs-lookup"><span data-stu-id="41b3a-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="41b3a-166">You can examine these rules on Azure classic portal:</span><span class="sxs-lookup"><span data-stu-id="41b3a-166">You can examine these rules on Azure classic portal:</span></span>

![NAT rules on the load balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="41b3a-168">Currently the template only supports 3-node clusters.</span><span class="sxs-lookup"><span data-stu-id="41b3a-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="41b3a-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span><span class="sxs-lookup"><span data-stu-id="41b3a-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="41b3a-170">Install and start the Deis platform</span><span class="sxs-lookup"><span data-stu-id="41b3a-170">Install and start the Deis platform</span></span>
<span data-ttu-id="41b3a-171">Now you can use deisctl to install and start the Deis platform:</span><span class="sxs-lookup"><span data-stu-id="41b3a-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="41b3a-172">Starting the platform takes a while (as much as 10 minutes).</span><span class="sxs-lookup"><span data-stu-id="41b3a-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="41b3a-173">Especially, starting the builder service can take a long time.</span><span class="sxs-lookup"><span data-stu-id="41b3a-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="41b3a-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span><span class="sxs-lookup"><span data-stu-id="41b3a-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="41b3a-175">You can use `deisctl list` to verify if all services are running:</span><span class="sxs-lookup"><span data-stu-id="41b3a-175">You can use `deisctl list` to verify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="41b3a-176">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="41b3a-176">Congratulations!</span></span> <span data-ttu-id="41b3a-177">Now you've got a running Deis clsuter on Azure!</span><span class="sxs-lookup"><span data-stu-id="41b3a-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="41b3a-178">Next, let's deploy a sample Go application to see the cluster in action.</span><span class="sxs-lookup"><span data-stu-id="41b3a-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="41b3a-179">Deploy and scale a Hello World application</span><span class="sxs-lookup"><span data-stu-id="41b3a-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="41b3a-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span><span class="sxs-lookup"><span data-stu-id="41b3a-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="41b3a-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="41b3a-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="41b3a-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="41b3a-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="41b3a-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="41b3a-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy A record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="41b3a-185">Install deis:</span><span class="sxs-lookup"><span data-stu-id="41b3a-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="41b3a-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span><span class="sxs-lookup"><span data-stu-id="41b3a-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="41b3a-187">To create a new SSH key pair, use:</span><span class="sxs-lookup"><span data-stu-id="41b3a-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="41b3a-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span><span class="sxs-lookup"><span data-stu-id="41b3a-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="41b3a-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span><span class="sxs-lookup"><span data-stu-id="41b3a-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="41b3a-191">Register a new user:</span><span class="sxs-lookup"><span data-stu-id="41b3a-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="41b3a-192">Add the SSH key:</span><span class="sxs-lookup"><span data-stu-id="41b3a-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="41b3a-193">Create an application.</span><span class="sxs-lookup"><span data-stu-id="41b3a-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="41b3a-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="41b3a-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="41b3a-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span><span class="sxs-lookup"><span data-stu-id="41b3a-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="41b3a-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span><span class="sxs-lookup"><span data-stu-id="41b3a-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="41b3a-197">If everything works out, you should see something like the following at the end of command outputs:</span><span class="sxs-lookup"><span data-stu-id="41b3a-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="41b3a-198">Verify if the application is working:</span><span class="sxs-lookup"><span data-stu-id="41b3a-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="41b3a-199">You should see:</span><span class="sxs-lookup"><span data-stu-id="41b3a-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="41b3a-200">Scale the application to 3 instances:</span><span class="sxs-lookup"><span data-stu-id="41b3a-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="41b3a-201">Optionally, you can use deis info to examine details of your application.</span><span class="sxs-lookup"><span data-stu-id="41b3a-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="41b3a-202">The following outputs are from my application deployment:</span><span class="sxs-lookup"><span data-stu-id="41b3a-202">The following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="41b3a-203">Next Steps</span><span class="sxs-lookup"><span data-stu-id="41b3a-203">Next Steps</span></span>
<span data-ttu-id="41b3a-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="41b3a-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="41b3a-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span><span class="sxs-lookup"><span data-stu-id="41b3a-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="41b3a-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span><span class="sxs-lookup"><span data-stu-id="41b3a-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="41b3a-207">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="41b3a-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="41b3a-208">[Azure Resource Manager Overview][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="41b3a-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="41b3a-209">[How to use the Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="41b3a-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="41b3a-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="41b3a-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md





