---
title: 'PowerShell script: Create a custom image from a VHD file in Azure Lab Services | Microsoft Docs'
description: This PowerShell script creates a custom image from a VHD file in Azure Lab Services.
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
ms.openlocfilehash: 19b7c3c6018ec56b056761c336bc56c8b63b47a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857130"
---
# <a name="use-powershell-to-create-a-custom-image-from-a-vhd-file-in-azure-lab-services"></a><span data-ttu-id="dd73e-103">Use PowerShell to create a custom image from a VHD file in Azure Lab Services</span><span class="sxs-lookup"><span data-stu-id="dd73e-103">Use PowerShell to create a custom image from a VHD file in Azure Lab Services</span></span>

<span data-ttu-id="dd73e-104">This sample PowerShell script creates a custom image from a VHD file in Azure Lab Services</span><span class="sxs-lookup"><span data-stu-id="dd73e-104">This sample PowerShell script creates a custom image from a VHD file in Azure Lab Services</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="dd73e-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd73e-105">Prerequisites</span></span>
* <span data-ttu-id="dd73e-106">**A lab**.</span><span class="sxs-lookup"><span data-stu-id="dd73e-106">**A lab**.</span></span> <span data-ttu-id="dd73e-107">The script requires you to have an existing lab.</span><span class="sxs-lookup"><span data-stu-id="dd73e-107">The script requires you to have an existing lab.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dd73e-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="dd73e-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/devtest-lab/create-custom-image-from-vhd/create-custom-image-from-vhd.ps1 "Add external user to a lab")]

## <a name="script-explanation"></a><span data-ttu-id="dd73e-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="dd73e-109">Script explanation</span></span>

<span data-ttu-id="dd73e-110">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="dd73e-110">This script uses the following commands:</span></span> 

| <span data-ttu-id="dd73e-111">Command</span><span class="sxs-lookup"><span data-stu-id="dd73e-111">Command</span></span> | <span data-ttu-id="dd73e-112">Notes</span><span class="sxs-lookup"><span data-stu-id="dd73e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dd73e-113">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="dd73e-113">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="dd73e-114">Gets resources.</span><span class="sxs-lookup"><span data-stu-id="dd73e-114">Gets resources.</span></span> |
| [<span data-ttu-id="dd73e-115">Get-AzureRmStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="dd73e-115">Get-AzureRmStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="dd73e-116">Gets the access keys for an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="dd73e-116">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="dd73e-117">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="dd73e-117">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="dd73e-118">Adds an Azure deployment to a resource group.</span><span class="sxs-lookup"><span data-stu-id="dd73e-118">Adds an Azure deployment to a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dd73e-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd73e-119">Next steps</span></span>

<span data-ttu-id="dd73e-120">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="dd73e-120">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="dd73e-121">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dd73e-121">Additional Azure Lab Services PowerShell script samples can be found in the [Azure Lab Services PowerShell samples](../samples-powershell.md).</span></span>