---
title: Azure Government Connect with PowerShell | Microsoft Docs
description: Information on connecting your subscription in Azure Government with PowerShell
services: azure-government
cloud: gov
documentationcenter: ''
author: zakramer
manager: liki
ms.assetid: 47e5e535-baa0-457e-8c41-f9fd65478b38
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 02/13/2017
ms.author: zakramer
ms.openlocfilehash: de36ddf8e270f12c886877d7c78237106aabc38c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562873"
---
# <a name="connect-to-azure-government-with-powershell"></a><span data-ttu-id="82f73-103">Connect to Azure Government with PowerShell</span><span class="sxs-lookup"><span data-stu-id="82f73-103">Connect to Azure Government with PowerShell</span></span>
<span data-ttu-id="82f73-104">To use Azure PowerShell with Azure Government, you need to connect to Azure Government instead of Azure Public.</span><span class="sxs-lookup"><span data-stu-id="82f73-104">To use Azure PowerShell with Azure Government, you need to connect to Azure Government instead of Azure Public.</span></span> <span data-ttu-id="82f73-105">Azure PowerShell can be used to manage a large subscription through script or to access features that are not currently available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82f73-105">Azure PowerShell can be used to manage a large subscription through script or to access features that are not currently available in the Azure portal.</span></span> <span data-ttu-id="82f73-106">If you have used PowerShell in Azure Public, it is mostly the same.</span><span class="sxs-lookup"><span data-stu-id="82f73-106">If you have used PowerShell in Azure Public, it is mostly the same.</span></span>  <span data-ttu-id="82f73-107">The differences in Azure Government are:</span><span class="sxs-lookup"><span data-stu-id="82f73-107">The differences in Azure Government are:</span></span>

* <span data-ttu-id="82f73-108">Connecting your account</span><span class="sxs-lookup"><span data-stu-id="82f73-108">Connecting your account</span></span>
* <span data-ttu-id="82f73-109">Region names</span><span class="sxs-lookup"><span data-stu-id="82f73-109">Region names</span></span>

> [!NOTE]
> <span data-ttu-id="82f73-110">If you have not used PowerShell yet, check out the [Introduction to Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="82f73-110">If you have not used PowerShell yet, check out the [Introduction to Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
> 
> 

<span data-ttu-id="82f73-111">When you start PowerShell, you have to tell Azure PowerShell to connect to Azure Government by specifying an environment parameter.</span><span class="sxs-lookup"><span data-stu-id="82f73-111">When you start PowerShell, you have to tell Azure PowerShell to connect to Azure Government by specifying an environment parameter.</span></span>  <span data-ttu-id="82f73-112">The parameter ensures that PowerShell is connecting to the correct endpoints.</span><span class="sxs-lookup"><span data-stu-id="82f73-112">The parameter ensures that PowerShell is connecting to the correct endpoints.</span></span>  <span data-ttu-id="82f73-113">The collection of endpoints is determined when you connect log in to your account.</span><span class="sxs-lookup"><span data-stu-id="82f73-113">The collection of endpoints is determined when you connect log in to your account.</span></span>  <span data-ttu-id="82f73-114">Different APIs require different versions of the environment switch:</span><span class="sxs-lookup"><span data-stu-id="82f73-114">Different APIs require different versions of the environment switch:</span></span>

| <span data-ttu-id="82f73-115">Connection type</span><span class="sxs-lookup"><span data-stu-id="82f73-115">Connection type</span></span> | <span data-ttu-id="82f73-116">Command</span><span class="sxs-lookup"><span data-stu-id="82f73-116">Command</span></span> |
| --- | --- |
| <span data-ttu-id="82f73-117">[Azure (Classic deployment model)](https://msdn.microsoft.com/library/dn708504.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="82f73-117">[Azure (Classic deployment model)](https://msdn.microsoft.com/library/dn708504.aspx) commands</span></span> |`Add-AzureAccount -Environment AzureUSGovernment` |
| <span data-ttu-id="82f73-118">[Azure (Resource Manager deployment model)](https://msdn.microsoft.com/library/mt125356.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="82f73-118">[Azure (Resource Manager deployment model)](https://msdn.microsoft.com/library/mt125356.aspx) commands</span></span> |`Login-AzureRmAccount -EnvironmentName AzureUSGovernment` |
| <span data-ttu-id="82f73-119">[Azure Active Directory (Classic deployment model)](https://msdn.microsoft.com/library/azure/jj151815.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="82f73-119">[Azure Active Directory (Classic deployment model)](https://msdn.microsoft.com/library/azure/jj151815.aspx) commands</span></span> |`Connect-MsolService -AzureEnvironment UsGovernment` |
| <span data-ttu-id="82f73-120">[Azure Active Directory (Resource Manager deployment model)](https://msdn.microsoft.com/library/azure/mt757189.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="82f73-120">[Azure Active Directory (Resource Manager deployment model)](https://msdn.microsoft.com/library/azure/mt757189.aspx) commands</span></span> |`Connect-AzureAD -AzureEnvironmentName AzureUSGovernment` |

<span data-ttu-id="82f73-121">You may also use the `Environment` switch when connecting to a storage account using `New-AzureStorageContext` and specify `AzureUSGovernment`.</span><span class="sxs-lookup"><span data-stu-id="82f73-121">You may also use the `Environment` switch when connecting to a storage account using `New-AzureStorageContext` and specify `AzureUSGovernment`.</span></span>

### <a name="determining-region"></a><span data-ttu-id="82f73-122">Determining region</span><span class="sxs-lookup"><span data-stu-id="82f73-122">Determining region</span></span>
<span data-ttu-id="82f73-123">Once you are connected, there is one additional difference – The regions used to target a service.</span><span class="sxs-lookup"><span data-stu-id="82f73-123">Once you are connected, there is one additional difference – The regions used to target a service.</span></span>  <span data-ttu-id="82f73-124">Every Azure cloud has different regions.</span><span class="sxs-lookup"><span data-stu-id="82f73-124">Every Azure cloud has different regions.</span></span>  <span data-ttu-id="82f73-125">You can see them listed on the service availability page.</span><span class="sxs-lookup"><span data-stu-id="82f73-125">You can see them listed on the service availability page.</span></span>  <span data-ttu-id="82f73-126">You normally use the region in the `Location` parameter for a command.</span><span class="sxs-lookup"><span data-stu-id="82f73-126">You normally use the region in the `Location` parameter for a command.</span></span>

<span data-ttu-id="82f73-127">There is one catch.</span><span class="sxs-lookup"><span data-stu-id="82f73-127">There is one catch.</span></span>  <span data-ttu-id="82f73-128">The Azure Government region display names have different formatting than their common names:</span><span class="sxs-lookup"><span data-stu-id="82f73-128">The Azure Government region display names have different formatting than their common names:</span></span>

| <span data-ttu-id="82f73-129">Common Name</span><span class="sxs-lookup"><span data-stu-id="82f73-129">Common Name</span></span> | <span data-ttu-id="82f73-130">Display Name</span><span class="sxs-lookup"><span data-stu-id="82f73-130">Display Name</span></span> | <span data-ttu-id="82f73-131">Location Name</span><span class="sxs-lookup"><span data-stu-id="82f73-131">Location Name</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82f73-132">US Gov Virginia</span><span class="sxs-lookup"><span data-stu-id="82f73-132">US Gov Virginia</span></span> |`USGov Virginia` | `usgovvirginia` |
| <span data-ttu-id="82f73-133">US Gov Iowa</span><span class="sxs-lookup"><span data-stu-id="82f73-133">US Gov Iowa</span></span> |`USGov Iowa` | `usgoviowa` |
| <span data-ttu-id="82f73-134">US DoD East</span><span class="sxs-lookup"><span data-stu-id="82f73-134">US DoD East</span></span> |`USDoD East` | `usdodeast` |
| <span data-ttu-id="82f73-135">US DoD Central</span><span class="sxs-lookup"><span data-stu-id="82f73-135">US DoD Central</span></span> |`USDoD Central` | `usdodcentral` |

> [!NOTE]
> <span data-ttu-id="82f73-136">There is no space between `US` and `Gov` or `US` and `DoD` when using the `Location` parameter.</span><span class="sxs-lookup"><span data-stu-id="82f73-136">There is no space between `US` and `Gov` or `US` and `DoD` when using the `Location` parameter.</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="82f73-137">As is true with PowerShell for Azure Public, you can use either the Display Name or the Location Name for the `Location` parameter.</span><span class="sxs-lookup"><span data-stu-id="82f73-137">As is true with PowerShell for Azure Public, you can use either the Display Name or the Location Name for the `Location` parameter.</span></span>
>
>

<span data-ttu-id="82f73-138">If you ever want to validate the available regions in Azure Government, you can run the following commands and print the current list:</span><span class="sxs-lookup"><span data-stu-id="82f73-138">If you ever want to validate the available regions in Azure Government, you can run the following commands and print the current list:</span></span>

    Get-AzureLocation

<span data-ttu-id="82f73-139">If you are curious about the available environments across Azure, you can run:</span><span class="sxs-lookup"><span data-stu-id="82f73-139">If you are curious about the available environments across Azure, you can run:</span></span>

    Get-AzureEnvironment
