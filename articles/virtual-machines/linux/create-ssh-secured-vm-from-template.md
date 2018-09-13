---
title: Create a Linux VM using an Azure template | Microsoft Docs
description: Create a Linux VM on Azure using an Azure Resource Manager template.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 10/24/2016
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae057350a15ef484bee9812babb24e3eca15d434
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556330"
---
# <a name="how-to-create-a-linux-vm-using-an-azure-resource-manager-template"></a><span data-ttu-id="f4538-103">How to create a Linux VM using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="f4538-103">How to create a Linux VM using an Azure Resource Manager template</span></span>
<span data-ttu-id="f4538-104">This article shows you how to quickly deploy a Linux Virtual Machine on Azure using an Azure Template.</span><span class="sxs-lookup"><span data-stu-id="f4538-104">This article shows you how to quickly deploy a Linux Virtual Machine on Azure using an Azure Template.</span></span>  <span data-ttu-id="f4538-105">The article requires:</span><span class="sxs-lookup"><span data-stu-id="f4538-105">The article requires:</span></span>

* <span data-ttu-id="f4538-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="f4538-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="f4538-107">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span><span class="sxs-lookup"><span data-stu-id="f4538-107">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="f4538-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="f4538-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="f4538-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4538-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="f4538-110">Quick Command Summary</span><span class="sxs-lookup"><span data-stu-id="f4538-110">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f4538-111">Detailed Walkthrough</span><span class="sxs-lookup"><span data-stu-id="f4538-111">Detailed Walkthrough</span></span>
<span data-ttu-id="f4538-112">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span><span class="sxs-lookup"><span data-stu-id="f4538-112">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="f4538-113">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span><span class="sxs-lookup"><span data-stu-id="f4538-113">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="f4538-114">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span><span class="sxs-lookup"><span data-stu-id="f4538-114">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="f4538-115">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span><span class="sxs-lookup"><span data-stu-id="f4538-115">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="f4538-116">Create the Linux VM</span><span class="sxs-lookup"><span data-stu-id="f4538-116">Create the Linux VM</span></span>
<span data-ttu-id="f4538-117">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f4538-117">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="f4538-118">Remember that in your example you need to use names that are unique to your environment.</span><span class="sxs-lookup"><span data-stu-id="f4538-118">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="f4538-119">This example uses `myResourceGroup` as the resource group name, and `myVM` as the VM name.</span><span class="sxs-lookup"><span data-stu-id="f4538-119">This example uses `myResourceGroup` as the resource group name, and `myVM` as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="f4538-120">The output should look like the following output block:</span><span class="sxs-lookup"><span data-stu-id="f4538-120">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="f4538-121">That example deployed a VM using the `--template-uri` parameter.</span><span class="sxs-lookup"><span data-stu-id="f4538-121">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="f4538-122">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span><span class="sxs-lookup"><span data-stu-id="f4538-122">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="f4538-123">The Azure CLI prompts you for the parameters required by the template.</span><span class="sxs-lookup"><span data-stu-id="f4538-123">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4538-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4538-124">Next steps</span></span>
<span data-ttu-id="f4538-125">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span><span class="sxs-lookup"><span data-stu-id="f4538-125">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

