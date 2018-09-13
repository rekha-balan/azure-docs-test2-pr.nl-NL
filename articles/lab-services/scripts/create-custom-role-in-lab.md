---
title: 'PowerShell script: Create a custom role in a lab in Azure DevTest Labs | Microsoft Docs'
description: This PowerShell script adds an external user to a lab in Azure DevTest Labs.
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
ms.openlocfilehash: 295f742342fba7d77b556724c8005f3ac4816482
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968378"
---
# <a name="use-powershell-to-create-a-custom-role-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="3b59d-103">Use PowerShell to create a custom role in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3b59d-103">Use PowerShell to create a custom role in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="3b59d-104">This sample PowerShell script creates a custom role to use in a lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="3b59d-104">This sample PowerShell script creates a custom role to use in a lab in Azure DevTest Labs.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="3b59d-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b59d-105">Prerequisites</span></span>
* <span data-ttu-id="3b59d-106">**A lab**.</span><span class="sxs-lookup"><span data-stu-id="3b59d-106">**A lab**.</span></span> <span data-ttu-id="3b59d-107">The script requires you to have an existing lab.</span><span class="sxs-lookup"><span data-stu-id="3b59d-107">The script requires you to have an existing lab.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3b59d-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="3b59d-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/devtest-lab/create-custom-role-in-lab/create-custom-role-in-lab.ps1 "Add external user to a lab")]

## <a name="script-explanation"></a><span data-ttu-id="3b59d-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3b59d-109">Script explanation</span></span>

<span data-ttu-id="3b59d-110">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="3b59d-110">This script uses the following commands:</span></span> 

| <span data-ttu-id="3b59d-111">Command</span><span class="sxs-lookup"><span data-stu-id="3b59d-111">Command</span></span> | <span data-ttu-id="3b59d-112">Notes</span><span class="sxs-lookup"><span data-stu-id="3b59d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3b59d-113">Get-AzureRmProviderOperation</span><span class="sxs-lookup"><span data-stu-id="3b59d-113">Get-AzureRmProviderOperation</span></span>](/powershell/module/azurerm.resources/get-azurermprovideroperation) | <span data-ttu-id="3b59d-114">Gets the operations for an Azure resource provider that are securable using Azure RBAC.</span><span class="sxs-lookup"><span data-stu-id="3b59d-114">Gets the operations for an Azure resource provider that are securable using Azure RBAC.</span></span> |
| [<span data-ttu-id="3b59d-115">Get-AzureRmRoleDefinition</span><span class="sxs-lookup"><span data-stu-id="3b59d-115">Get-AzureRmRoleDefinition</span></span>](/powershell/module/azurerm.resources/get-azurermroledefinition) | <span data-ttu-id="3b59d-116">Lists all Azure RBAC roles that are available for assignment.</span><span class="sxs-lookup"><span data-stu-id="3b59d-116">Lists all Azure RBAC roles that are available for assignment.</span></span> |
| [<span data-ttu-id="3b59d-117">New-AzureRmRoleDefinition</span><span class="sxs-lookup"><span data-stu-id="3b59d-117">New-AzureRmRoleDefinition</span></span>](/powershell/module/azurerm.resources/new-azurermroledefinition) | <span data-ttu-id="3b59d-118">Creates a custom role.</span><span class="sxs-lookup"><span data-stu-id="3b59d-118">Creates a custom role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3b59d-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b59d-119">Next steps</span></span>

<span data-ttu-id="3b59d-120">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="3b59d-120">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="3b59d-121">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b59d-121">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span></span>