---
title: 'PowerShell script: Add an external user to a lab in Azure DevTest Labs | Microsoft Docs'
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
ms.openlocfilehash: 0acff1eb4cee441187205b11a7e07cc718072cbf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965505"
---
# <a name="use-powershell-to-add-an-external-user-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bd059-103">Use PowerShell to add an external user to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bd059-103">Use PowerShell to add an external user to a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="bd059-104">This sample PowerShell script adds an external user to a lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="bd059-104">This sample PowerShell script adds an external user to a lab in Azure DevTest Labs.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="bd059-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bd059-105">Prerequisites</span></span>
* <span data-ttu-id="bd059-106">**A lab**.</span><span class="sxs-lookup"><span data-stu-id="bd059-106">**A lab**.</span></span> <span data-ttu-id="bd059-107">The script requires you to have an existing lab.</span><span class="sxs-lookup"><span data-stu-id="bd059-107">The script requires you to have an existing lab.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bd059-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="bd059-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/devtest-lab/add-external-user-to-lab/add-external-user-to-custom-lab.ps1 "Add external user to a lab")]

## <a name="script-explanation"></a><span data-ttu-id="bd059-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="bd059-109">Script explanation</span></span>

<span data-ttu-id="bd059-110">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="bd059-110">This script uses the following commands:</span></span> 

| <span data-ttu-id="bd059-111">Command</span><span class="sxs-lookup"><span data-stu-id="bd059-111">Command</span></span> | <span data-ttu-id="bd059-112">Notes</span><span class="sxs-lookup"><span data-stu-id="bd059-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bd059-113">Get-AzureRmADUser</span><span class="sxs-lookup"><span data-stu-id="bd059-113">Get-AzureRmADUser</span></span>](/powershell/module/azurerm.resources/get-azurermaduser) | <span data-ttu-id="bd059-114">Retries the user object from Azure active directory.</span><span class="sxs-lookup"><span data-stu-id="bd059-114">Retries the user object from Azure active directory.</span></span> |
| [<span data-ttu-id="bd059-115">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="bd059-115">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="bd059-116">Assigns the specified role to the specified principal, at the specified scope.</span><span class="sxs-lookup"><span data-stu-id="bd059-116">Assigns the specified role to the specified principal, at the specified scope.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bd059-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd059-117">Next steps</span></span>

<span data-ttu-id="bd059-118">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="bd059-118">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="bd059-119">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd059-119">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span></span>
