---
title: Azure PowerShell script sample - Get a managed resource group and resize VMs | Microsoft Docs
description: Azure PowerShell script sample - Get a managed resource group and resize VMs
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: poweshell
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2017
ms.author: tomfitz
ms.openlocfilehash: f549f26cb3f9fdb2d805d2efb2c0e1706abe3edb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966640"
---
# <a name="get-resources-in-a-managed-resource-group-and-resize-vms-with-powershell"></a><span data-ttu-id="ff731-103">Get resources in a managed resource group and resize VMs with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff731-103">Get resources in a managed resource group and resize VMs with PowerShell</span></span>

<span data-ttu-id="ff731-104">This script retrieves resources from a managed resource group, and resizes the VMs in that resource group.</span><span class="sxs-lookup"><span data-stu-id="ff731-104">This script retrieves resources from a managed resource group, and resizes the VMs in that resource group.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ff731-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="ff731-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/managed-applications/get-application/get-application.ps1 "Get application")]


## <a name="script-explanation"></a><span data-ttu-id="ff731-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ff731-106">Script explanation</span></span>

<span data-ttu-id="ff731-107">This script uses the following commands to deploy the managed application.</span><span class="sxs-lookup"><span data-stu-id="ff731-107">This script uses the following commands to deploy the managed application.</span></span> <span data-ttu-id="ff731-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ff731-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="ff731-109">Command</span><span class="sxs-lookup"><span data-stu-id="ff731-109">Command</span></span> | <span data-ttu-id="ff731-110">Notes</span><span class="sxs-lookup"><span data-stu-id="ff731-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff731-111">Get-AzureRmManagedApplication</span><span class="sxs-lookup"><span data-stu-id="ff731-111">Get-AzureRmManagedApplication</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermmanagedapplication) | <span data-ttu-id="ff731-112">List managed applications.</span><span class="sxs-lookup"><span data-stu-id="ff731-112">List managed applications.</span></span> <span data-ttu-id="ff731-113">Provide resource group name to focus the results.</span><span class="sxs-lookup"><span data-stu-id="ff731-113">Provide resource group name to focus the results.</span></span> |
| [<span data-ttu-id="ff731-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="ff731-114">Get-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="ff731-115">List resources.</span><span class="sxs-lookup"><span data-stu-id="ff731-115">List resources.</span></span> <span data-ttu-id="ff731-116">Provide a resource group and resource type to focus the result.</span><span class="sxs-lookup"><span data-stu-id="ff731-116">Provide a resource group and resource type to focus the result.</span></span> |
| [<span data-ttu-id="ff731-117">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ff731-117">Update-AzureRmVM</span></span>](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) | <span data-ttu-id="ff731-118">Update a virtual machine's size.</span><span class="sxs-lookup"><span data-stu-id="ff731-118">Update a virtual machine's size.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ff731-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff731-119">Next steps</span></span>

* <span data-ttu-id="ff731-120">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff731-120">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span></span>
* <span data-ttu-id="ff731-121">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="ff731-121">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span></span>
