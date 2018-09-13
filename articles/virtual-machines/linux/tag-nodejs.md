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
ms.openlocfilehash: becf792a1cbf7453937370af7aece60b25b19f9e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556151"
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="8578a-103">How to tag a Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="8578a-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="8578a-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="8578a-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="8578a-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span><span class="sxs-lookup"><span data-stu-id="8578a-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="8578a-106">Azure currently supports up to 15 tags per resource and resource group.</span><span class="sxs-lookup"><span data-stu-id="8578a-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="8578a-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span><span class="sxs-lookup"><span data-stu-id="8578a-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="8578a-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span><span class="sxs-lookup"><span data-stu-id="8578a-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="8578a-109">Tagging with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8578a-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="8578a-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="8578a-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="8578a-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span><span class="sxs-lookup"><span data-stu-id="8578a-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="8578a-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span><span class="sxs-lookup"><span data-stu-id="8578a-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="8578a-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span><span class="sxs-lookup"><span data-stu-id="8578a-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="8578a-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span><span class="sxs-lookup"><span data-stu-id="8578a-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="8578a-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="8578a-115">Next steps</span></span>
* <span data-ttu-id="8578a-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="8578a-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="8578a-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="8578a-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
