---
title: 'PowerShell script: Set allowed VM sizes in Azure Lab Services | Microsoft Docs'
description: This PowerShell script sets allowed VM sizes in Azure Lab Services.
services: lab-services
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2018
ms.author: spelluru
ms.openlocfilehash: 559e74675a5d113584dca21979c20462c9cdf19c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871076"
---
# <a name="use-powershell-to-set-allowed-vm-sizes-in-azure-lab-services"></a><span data-ttu-id="b2dcd-103">Use PowerShell to set allowed VM sizes in Azure Lab Services</span><span class="sxs-lookup"><span data-stu-id="b2dcd-103">Use PowerShell to set allowed VM sizes in Azure Lab Services</span></span>

<span data-ttu-id="b2dcd-104">This sample PowerShell script sets allowed virtual machine (VM) sizes in Azure Lab Services.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-104">This sample PowerShell script sets allowed virtual machine (VM) sizes in Azure Lab Services.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="b2dcd-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b2dcd-105">Prerequisites</span></span>
* <span data-ttu-id="b2dcd-106">**A lab**.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-106">**A lab**.</span></span> <span data-ttu-id="b2dcd-107">The script requires you to have an existing lab.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-107">The script requires you to have an existing lab.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b2dcd-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="b2dcd-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/devtest-lab/set-allowed-vm-sizes-in-lab/set-allowed-vm-sizes-in-lab.ps1 "Add external user to a lab")]

## <a name="script-explanation"></a><span data-ttu-id="b2dcd-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b2dcd-109">Script explanation</span></span>

<span data-ttu-id="b2dcd-110">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="b2dcd-110">This script uses the following commands:</span></span> 

| <span data-ttu-id="b2dcd-111">Command</span><span class="sxs-lookup"><span data-stu-id="b2dcd-111">Command</span></span> | <span data-ttu-id="b2dcd-112">Notes</span><span class="sxs-lookup"><span data-stu-id="b2dcd-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b2dcd-113">Find-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b2dcd-113">Find-AzureRmResource</span></span>](/powershell/module/azurerm.resources/find-azurermresource) | <span data-ttu-id="b2dcd-114">Searches for resources based on specified parameters.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-114">Searches for resources based on specified parameters.</span></span> |
| [<span data-ttu-id="b2dcd-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b2dcd-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="b2dcd-116">Gets resources.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-116">Gets resources.</span></span> |
| [<span data-ttu-id="b2dcd-117">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b2dcd-117">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="b2dcd-118">Modifies a resource.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-118">Modifies a resource.</span></span> |
| [<span data-ttu-id="b2dcd-119">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b2dcd-119">New-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="b2dcd-120">Create a resource.</span><span class="sxs-lookup"><span data-stu-id="b2dcd-120">Create a resource.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2dcd-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2dcd-121">Next steps</span></span>

<span data-ttu-id="b2dcd-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="b2dcd-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="b2dcd-123">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b2dcd-123">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span></span>
