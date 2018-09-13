---
title: How to tag an Azure Linux virtual machine | Microsoft Docs
description: Learn about tagging an Azure Linux virtual machine created in Azure using the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 94db9bf6b5e16f43a7f8276c316052a08d382e79
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549929"
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="12a6d-103">How to tag a Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="12a6d-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="12a6d-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="12a6d-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="12a6d-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span><span class="sxs-lookup"><span data-stu-id="12a6d-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="12a6d-106">Azure currently supports up to 15 tags per resource and resource group.</span><span class="sxs-lookup"><span data-stu-id="12a6d-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="12a6d-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span><span class="sxs-lookup"><span data-stu-id="12a6d-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="12a6d-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span><span class="sxs-lookup"><span data-stu-id="12a6d-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="12a6d-109">Tagging with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="12a6d-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="12a6d-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="12a6d-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="12a6d-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12a6d-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="12a6d-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span><span class="sxs-lookup"><span data-stu-id="12a6d-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="12a6d-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span><span class="sxs-lookup"><span data-stu-id="12a6d-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="12a6d-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span><span class="sxs-lookup"><span data-stu-id="12a6d-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="12a6d-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span><span class="sxs-lookup"><span data-stu-id="12a6d-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="12a6d-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="12a6d-116">Next steps</span></span>
* <span data-ttu-id="12a6d-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="12a6d-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="12a6d-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="12a6d-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
