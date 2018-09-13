---
title: 'PowerShell script: Add a marketplace image to a lab in Azure DevTest Labs | Microsoft Docs'
description: This PowerShell script adds a marketplace image to a lab in Azure DevTest Labs.
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
ms.openlocfilehash: a3a007bf19a28e6f361837856f83a191a761ef9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869501"
---
# <a name="use-powershell-to-add-a-marketplace-image-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="2690f-103">Use PowerShell to add a marketplace image to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2690f-103">Use PowerShell to add a marketplace image to a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="2690f-104">This sample PowerShell script adds a marketplace image to a lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="2690f-104">This sample PowerShell script adds a marketplace image to a lab in Azure DevTest Labs.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="2690f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2690f-105">Prerequisites</span></span>
* <span data-ttu-id="2690f-106">**A lab**.</span><span class="sxs-lookup"><span data-stu-id="2690f-106">**A lab**.</span></span> <span data-ttu-id="2690f-107">The script requires you to have an existing lab.</span><span class="sxs-lookup"><span data-stu-id="2690f-107">The script requires you to have an existing lab.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2690f-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="2690f-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/devtest-lab/add-marketplace-images-to-lab/add-marketplace-images-to-lab.ps1 "Add marketplace images to a lab")]

## <a name="script-explanation"></a><span data-ttu-id="2690f-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="2690f-109">Script explanation</span></span>

<span data-ttu-id="2690f-110">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="2690f-110">This script uses the following commands:</span></span> 

| <span data-ttu-id="2690f-111">Command</span><span class="sxs-lookup"><span data-stu-id="2690f-111">Command</span></span> | <span data-ttu-id="2690f-112">Notes</span><span class="sxs-lookup"><span data-stu-id="2690f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2690f-113">Find-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2690f-113">Find-AzureRmResource</span></span>](/powershell/module/azurerm.resources/find-azurermresource) | <span data-ttu-id="2690f-114">Searches for resources based on specified parameters.</span><span class="sxs-lookup"><span data-stu-id="2690f-114">Searches for resources based on specified parameters.</span></span> |
| [<span data-ttu-id="2690f-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2690f-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="2690f-116">Gets resources.</span><span class="sxs-lookup"><span data-stu-id="2690f-116">Gets resources.</span></span> |
| [<span data-ttu-id="2690f-117">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2690f-117">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="2690f-118">Modifies a resource.</span><span class="sxs-lookup"><span data-stu-id="2690f-118">Modifies a resource.</span></span> |
| [<span data-ttu-id="2690f-119">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2690f-119">New-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="2690f-120">Create a resource.</span><span class="sxs-lookup"><span data-stu-id="2690f-120">Create a resource.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2690f-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="2690f-121">Next steps</span></span>

<span data-ttu-id="2690f-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="2690f-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="2690f-123">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2690f-123">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span></span>
