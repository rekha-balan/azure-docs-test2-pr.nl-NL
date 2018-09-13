---
title: Select Linux VM images with the Azure  CLI | Microsoft Docs
description: Learn how to determine the publisher, offer, and SKU for images when creating a Linux virtual machine with the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/15/2017
ms.author: rasquill
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe121b05fa54d90a9ce63fc4591ec4a9bd30d605
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550924"
---
# <a name="how-to-find-linux-vm-images-with-the-azure-cli"></a><span data-ttu-id="97970-103">How to find Linux VM images with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="97970-103">How to find Linux VM images with the Azure CLI</span></span>
<span data-ttu-id="97970-104">This topic describes how to find publishers, offers, skus, and versions for each location into which you might deploy.</span><span class="sxs-lookup"><span data-stu-id="97970-104">This topic describes how to find publishers, offers, skus, and versions for each location into which you might deploy.</span></span> 


## <a name="use-azure-cli-20"></a><span data-ttu-id="97970-105">Use Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="97970-105">Use Azure CLI 2.0</span></span>

<span data-ttu-id="97970-106">Once you have [installed the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), use the `az vm image list` command to see a cached list of popular VM images.</span><span class="sxs-lookup"><span data-stu-id="97970-106">Once you have [installed the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), use the `az vm image list` command to see a cached list of popular VM images.</span></span> <span data-ttu-id="97970-107">For example, the following example of the command `az vm image list -o table` displays:</span><span class="sxs-lookup"><span data-stu-id="97970-107">For example, the following example of the command `az vm image list -o table` displays:</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               14.04.4-LTS         Canonical:UbuntuServer:14.04.4-LTS:latest                       UbuntuLTS            latest
CentOS         OpenLogic               7.2                 OpenLogic:CentOS:7.2:latest                                     CentOS               latest
openSUSE       SUSE                    13.2                SUSE:openSUSE:13.2:latest                                       openSUSE             latest
RHEL           RedHat                  7.2                 RedHat:RHEL:7.2:latest                                          RHEL                 latest
SLES           SUSE                    12-SP1              SUSE:SLES:12-SP1:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

### <a name="finding-all-current-images"></a><span data-ttu-id="97970-108">Finding all current images</span><span class="sxs-lookup"><span data-stu-id="97970-108">Finding all current images</span></span>

<span data-ttu-id="97970-109">To obtain the current list of all images, use the `az vm image list` command with the `--all` option.</span><span class="sxs-lookup"><span data-stu-id="97970-109">To obtain the current list of all images, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="97970-110">Unlike the Azure CLI 1.0 commands, the `az vm image list --all` command returns all images in **westus** by default (unless you specify a particular `--location` argument), so the `--all` command takes some time to complete.</span><span class="sxs-lookup"><span data-stu-id="97970-110">Unlike the Azure CLI 1.0 commands, the `az vm image list --all` command returns all images in **westus** by default (unless you specify a particular `--location` argument), so the `--all` command takes some time to complete.</span></span> <span data-ttu-id="97970-111">If you intend to investigate interactively, use `az vm image list --all > allImages.json`, which returns a list of all images currently available on Azure and stores it as a file for local use.</span><span class="sxs-lookup"><span data-stu-id="97970-111">If you intend to investigate interactively, use `az vm image list --all > allImages.json`, which returns a list of all images currently available on Azure and stores it as a file for local use.</span></span> 

<span data-ttu-id="97970-112">You can specify one of several options to restrict your search to a specific location, offer, publisher, or sku if you already have one or more in mind.</span><span class="sxs-lookup"><span data-stu-id="97970-112">You can specify one of several options to restrict your search to a specific location, offer, publisher, or sku if you already have one or more in mind.</span></span> <span data-ttu-id="97970-113">If you do not specify a location, the values for **westus** are returned.</span><span class="sxs-lookup"><span data-stu-id="97970-113">If you do not specify a location, the values for **westus** are returned.</span></span>

### <a name="find-specific-images"></a><span data-ttu-id="97970-114">Find specific images</span><span class="sxs-lookup"><span data-stu-id="97970-114">Find specific images</span></span>

<span data-ttu-id="97970-115">Use `az vm image list` with a filter to find specific information.</span><span class="sxs-lookup"><span data-stu-id="97970-115">Use `az vm image list` with a filter to find specific information.</span></span> <span data-ttu-id="97970-116">For example, the following displays the **offer**s that are available for **Debian** (remember that without the `--all` switch, it only searches the local cache of common images):</span><span class="sxs-lookup"><span data-stu-id="97970-116">For example, the following displays the **offer**s that are available for **Debian** (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian -o table --all
```

<span data-ttu-id="97970-117">The output is something like:</span><span class="sxs-lookup"><span data-stu-id="97970-117">The output is something like:</span></span> 
```
Offer   Publisher   Sku   Urn                              Version
------  ---------   ---   -------------------------------  -------------
Debian  credativ    8     credativ:Debian:8:8.0.201701180  8.0.201701180

<list shortened for the example>
```

<span data-ttu-id="97970-118">You can perform similar filters on the **--publisher** and **--sku** option.</span><span class="sxs-lookup"><span data-stu-id="97970-118">You can perform similar filters on the **--publisher** and **--sku** option.</span></span> <span data-ttu-id="97970-119">You can even perform partial matches on a filter, such as searching for **--offer Deb** to find all Debian images or **--publisher Micr** to find all Microsoft-published images.</span><span class="sxs-lookup"><span data-stu-id="97970-119">You can even perform partial matches on a filter, such as searching for **--offer Deb** to find all Debian images or **--publisher Micr** to find all Microsoft-published images.</span></span>

<span data-ttu-id="97970-120">If you know where you are deploying, you can use the general image search results along with the `az vm image list-skus`, `az vm image list-offers`, and `az vm image list-publishers` commands to find exactly what you want and where it can be deployed.</span><span class="sxs-lookup"><span data-stu-id="97970-120">If you know where you are deploying, you can use the general image search results along with the `az vm image list-skus`, `az vm image list-offers`, and `az vm image list-publishers` commands to find exactly what you want and where it can be deployed.</span></span> <span data-ttu-id="97970-121">For example, if from the preceding example you know that `credativ` has a Debian offer, you can then use the `--location` and other options to find exactly what you want.</span><span class="sxs-lookup"><span data-stu-id="97970-121">For example, if from the preceding example you know that `credativ` has a Debian offer, you can then use the `--location` and other options to find exactly what you want.</span></span> <span data-ttu-id="97970-122">The following example looks for a Debian 8 image in **westeurope**:</span><span class="sxs-lookup"><span data-stu-id="97970-122">The following example looks for a Debian 8 image in **westeurope**:</span></span>

```azurecli 
az vm image show -l westeurope -f debian -p credativ --skus 8 --version 8.0.201701180
```

<span data-ttu-id="97970-123">and the output is:</span><span class="sxs-lookup"><span data-stu-id="97970-123">and the output is:</span></span>

```json
{
  "dataDiskImages": [],
  "id": "/Subscriptions/<guid>/Providers/Microsoft.Compute/Locations/westeurope/Publishers/credativ/ArtifactTypes/VMImage/Offers/debian/Skus/8/Versions/8.0.201701180",
  "location": "westeurope",
  "name": "8.0.201701180",
  "osDiskImage": {
    "operatingSystem": "Linux"
  },
  "plan": null,
  "tags": null
}
```

## <a name="use-azure-cli-10"></a><span data-ttu-id="97970-124">Use Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="97970-124">Use Azure CLI 1.0</span></span> 

> [!NOTE]
> <span data-ttu-id="97970-125">This article describes how to navigate and select virtual machine images, using an installation of either the Azure CLI 1.0 or Azure PowerShell that supports the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="97970-125">This article describes how to navigate and select virtual machine images, using an installation of either the Azure CLI 1.0 or Azure PowerShell that supports the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="97970-126">As a prerequisite, change to the Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="97970-126">As a prerequisite, change to the Resource Manager mode.</span></span> <span data-ttu-id="97970-127">With the Azure CLI, enter that mode by typing `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="97970-127">With the Azure CLI, enter that mode by typing `azure config mode arm`.</span></span> 
> 

<span data-ttu-id="97970-128">The quickest way to locate an image is to call the `azure vm image list` command and pass the location, the publisher name (it's not case-sensitive!), and an offer -- if you know the offer.</span><span class="sxs-lookup"><span data-stu-id="97970-128">The quickest way to locate an image is to call the `azure vm image list` command and pass the location, the publisher name (it's not case-sensitive!), and an offer -- if you know the offer.</span></span> <span data-ttu-id="97970-129">For example, the following list is only a short example -- many lists are quite long -- if you know that "Canonical" is a publisher for the "UbuntuServer" offer.</span><span class="sxs-lookup"><span data-stu-id="97970-129">For example, the following list is only a short example -- many lists are quite long -- if you know that "Canonical" is a publisher for the "UbuntuServer" offer.</span></span>

```azurecli
azure vm image list westus canonical ubuntuserver
info:    Executing command vm image list
warn:    The parameter --sku if specified will be ignored
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"westus")
data:    Publisher  Offer         Sku                OS     Version          Location  Urn
data:    ---------  ------------  -----------------  -----  ---------------  --------  --------------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201604203  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201604203
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201605161  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201605161
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201606100  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606100
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201606270  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201607210  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201607210
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201608150  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201608150
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607220  westus    canonical:ubuntuserver:16.10-DAILY:16.10.201607220
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607230  westus    canonical:ubuntuserver:16.10-DAILY:16.10.201607230
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607240  westus    canonical:ubuntuserver:16.10-DAILY:16.10.201607240
```

<span data-ttu-id="97970-130">The **Urn** column will be the form you pass to `azure vm quick-create`.</span><span class="sxs-lookup"><span data-stu-id="97970-130">The **Urn** column will be the form you pass to `azure vm quick-create`.</span></span>

<span data-ttu-id="97970-131">Often, however, you don't yet know what is available.</span><span class="sxs-lookup"><span data-stu-id="97970-131">Often, however, you don't yet know what is available.</span></span> <span data-ttu-id="97970-132">In this case, you can navigate images by using the `azure vm image list-publishers` command and specifying a data center location at the prompt.</span><span class="sxs-lookup"><span data-stu-id="97970-132">In this case, you can navigate images by using the `azure vm image list-publishers` command and specifying a data center location at the prompt.</span></span> <span data-ttu-id="97970-133">For example, the following lists all image publishers in the West US location (pass the location argument by lowercasing and removing spaces from the standard locations)</span><span class="sxs-lookup"><span data-stu-id="97970-133">For example, the following lists all image publishers in the West US location (pass the location argument by lowercasing and removing spaces from the standard locations)</span></span>

```azurecli
azure vm image list-publishers
info:    Executing command vm image list-publishers
Location: westus
+ Getting virtual machine and/or extension image publishers (Location: "westus")
data:    Publisher                                       Location
data:    ----------------------------------------------  --------
data:    a10networks                                     westus  
data:    aiscaler-cache-control-ddos-and-url-rewriting-  westus  
data:    alertlogic                                      westus  
data:    AlertLogic.Extension                            westus  
```

<span data-ttu-id="97970-134">These lists can be quite long, so the example list preceding is just a snippet.</span><span class="sxs-lookup"><span data-stu-id="97970-134">These lists can be quite long, so the example list preceding is just a snippet.</span></span> <span data-ttu-id="97970-135">Let's say that I noticed that Canonical is, indeed, an image publisher in the West US location.</span><span class="sxs-lookup"><span data-stu-id="97970-135">Let's say that I noticed that Canonical is, indeed, an image publisher in the West US location.</span></span> <span data-ttu-id="97970-136">You can now find their offers by calling `azure vm image list-offers` and pass the location and the publisher at the prompts, like the following example:</span><span class="sxs-lookup"><span data-stu-id="97970-136">You can now find their offers by calling `azure vm image list-offers` and pass the location and the publisher at the prompts, like the following example:</span></span>

```azurecli
azure vm image list-offers
info:    Executing command vm image list-offers
Location: westus
Publisher: canonical
+ Getting virtual machine image offers (Publisher: "canonical" Location:"westus")
data:    Publisher  Offer                      Location
data:    ---------  -------------------------  --------
data:    canonical  Ubuntu15.04Snappy          westus
data:    canonical  Ubuntu15.04SnappyDocker    westus
data:    canonical  UbunturollingSnappy        westus
data:    canonical  UbuntuServer               westus
data:    canonical  Ubuntu_Snappy_Core         westus
data:    canonical  Ubuntu_Snappy_Core_Docker  westus
info:    vm image list-offers command OK
```

<span data-ttu-id="97970-137">Now we know that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span><span class="sxs-lookup"><span data-stu-id="97970-137">Now we know that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="97970-138">But what SKUs?</span><span class="sxs-lookup"><span data-stu-id="97970-138">But what SKUs?</span></span> <span data-ttu-id="97970-139">To get those values, you call `azure vm image list-skus` and respond to the prompt with the location, publisher, and offer that you have discovered.</span><span class="sxs-lookup"><span data-stu-id="97970-139">To get those values, you call `azure vm image list-skus` and respond to the prompt with the location, publisher, and offer that you have discovered.</span></span>

```azurecli
azure vm image list-skus
info:    Executing command vm image list-skus
Location: westus
Publisher: canonical
Offer: ubuntuserver
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"westus")
data:    Publisher  Offer         sku                Location
data:    ---------  ------------  -----------------  --------
data:    canonical  ubuntuserver  12.04.2-LTS        westus
data:    canonical  ubuntuserver  12.04.3-LTS        westus
data:    canonical  ubuntuserver  12.04.4-LTS        westus
data:    canonical  ubuntuserver  12.04.5-DAILY-LTS  westus
data:    canonical  ubuntuserver  12.04.5-LTS        westus
data:    canonical  ubuntuserver  12.10              westus
data:    canonical  ubuntuserver  14.04-beta         westus
data:    canonical  ubuntuserver  14.04.0-LTS        westus
data:    canonical  ubuntuserver  14.04.1-LTS        westus
data:    canonical  ubuntuserver  14.04.2-LTS        westus
data:    canonical  ubuntuserver  14.04.3-LTS        westus
data:    canonical  ubuntuserver  14.04.4-DAILY-LTS  westus
data:    canonical  ubuntuserver  14.04.4-LTS        westus
data:    canonical  ubuntuserver  14.04.5-DAILY-LTS  westus
data:    canonical  ubuntuserver  14.04.5-LTS        westus
data:    canonical  ubuntuserver  14.10              westus
data:    canonical  ubuntuserver  14.10-beta         westus
data:    canonical  ubuntuserver  14.10-DAILY        westus
data:    canonical  ubuntuserver  15.04              westus
data:    canonical  ubuntuserver  15.04-beta         westus
data:    canonical  ubuntuserver  15.04-DAILY        westus
data:    canonical  ubuntuserver  15.10              westus
data:    canonical  ubuntuserver  15.10-alpha        westus
data:    canonical  ubuntuserver  15.10-beta         westus
data:    canonical  ubuntuserver  15.10-DAILY        westus
data:    canonical  ubuntuserver  16.04-alpha        westus
data:    canonical  ubuntuserver  16.04-beta         westus
data:    canonical  ubuntuserver  16.04.0-DAILY-LTS  westus
data:    canonical  ubuntuserver  16.04.0-LTS        westus
data:    canonical  ubuntuserver  16.10-DAILY        westus
info:    vm image list-skus command OK
```

<span data-ttu-id="97970-140">With this information, you can now find exactly the image you want by calling the original call at the top.</span><span class="sxs-lookup"><span data-stu-id="97970-140">With this information, you can now find exactly the image you want by calling the original call at the top.</span></span>

```azurecli
azure vm image list westus canonical ubuntuserver 16.04.0-LTS
info:    Executing command vm image list
+ Getting virtual machine images (Publisher:"canonical" Offer:"ubuntuserver" Sku: "16.04.0-LTS" Location:"westus")
data:    Publisher  Offer         Sku          OS     Version          Location  Urn
data:    ---------  ------------  -----------  -----  ---------------  --------  --------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201604203  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201604203
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201605161  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201605161
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606100  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606100
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606270  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201607210  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201607210
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201608150  westus    canonical:ubuntuserver:16.04.0-LTS:16.04.201608150
info:    vm image list command OK
```

## <a name="next-steps"></a><span data-ttu-id="97970-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="97970-141">Next steps</span></span>
<span data-ttu-id="97970-142">Now you can choose precisely the image you want to use.</span><span class="sxs-lookup"><span data-stu-id="97970-142">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="97970-143">To create a virtual machine quickly by using the URN information, which you just found, or to use a template with that URN information, see [Create a Linux VM using the Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97970-143">To create a virtual machine quickly by using the URN information, which you just found, or to use a template with that URN information, see [Create a Linux VM using the Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
