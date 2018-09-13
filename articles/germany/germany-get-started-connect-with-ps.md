---
title: Connect to Azure Germany by using PowerShell | Microsoft Docs
description: Information on managing your subscription in Azure Germany by using PowerShell
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2017
ms.author: ralfwi
ms.openlocfilehash: 4232227f8598e8b67987412c0f4afdb738a6040c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857818"
---
# <a name="connect-to-azure-germany-by-using-powershell"></a><span data-ttu-id="7b181-103">Connect to Azure Germany by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b181-103">Connect to Azure Germany by using PowerShell</span></span>
<span data-ttu-id="7b181-104">To use Azure PowerShell with Azure Germany, you need to connect to Azure Germany instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="7b181-104">To use Azure PowerShell with Azure Germany, you need to connect to Azure Germany instead of global Azure.</span></span> <span data-ttu-id="7b181-105">You can use Azure PowerShell to manage a large subscription through a script or to access features that are not currently available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b181-105">You can use Azure PowerShell to manage a large subscription through a script or to access features that are not currently available in the Azure portal.</span></span> <span data-ttu-id="7b181-106">If you have used PowerShell in global Azure, it's mostly the same.</span><span class="sxs-lookup"><span data-stu-id="7b181-106">If you have used PowerShell in global Azure, it's mostly the same.</span></span> <span data-ttu-id="7b181-107">The differences in Azure Germany are:</span><span class="sxs-lookup"><span data-stu-id="7b181-107">The differences in Azure Germany are:</span></span>

* <span data-ttu-id="7b181-108">Connecting your account</span><span class="sxs-lookup"><span data-stu-id="7b181-108">Connecting your account</span></span>
* <span data-ttu-id="7b181-109">Region names</span><span class="sxs-lookup"><span data-stu-id="7b181-109">Region names</span></span>

> [!NOTE]
> <span data-ttu-id="7b181-110">If you have not used PowerShell yet, check out [Introduction to Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b181-110">If you have not used PowerShell yet, check out [Introduction to Azure PowerShell](/powershell/azure/overview).</span></span>


<span data-ttu-id="7b181-111">When you start PowerShell, you have to tell Azure PowerShell to connect to Azure Germany by specifying an environment parameter.</span><span class="sxs-lookup"><span data-stu-id="7b181-111">When you start PowerShell, you have to tell Azure PowerShell to connect to Azure Germany by specifying an environment parameter.</span></span> <span data-ttu-id="7b181-112">The parameter ensures that PowerShell is connecting to the correct endpoints.</span><span class="sxs-lookup"><span data-stu-id="7b181-112">The parameter ensures that PowerShell is connecting to the correct endpoints.</span></span> <span data-ttu-id="7b181-113">The collection of endpoints is determined when you connect to your account.</span><span class="sxs-lookup"><span data-stu-id="7b181-113">The collection of endpoints is determined when you connect to your account.</span></span> <span data-ttu-id="7b181-114">Different APIs require different versions of the environment switch:</span><span class="sxs-lookup"><span data-stu-id="7b181-114">Different APIs require different versions of the environment switch:</span></span>

| <span data-ttu-id="7b181-115">Connection type</span><span class="sxs-lookup"><span data-stu-id="7b181-115">Connection type</span></span> | <span data-ttu-id="7b181-116">Command</span><span class="sxs-lookup"><span data-stu-id="7b181-116">Command</span></span> |
| --- | --- |
| <span data-ttu-id="7b181-117">[Azure (classic deployment model)](https://msdn.microsoft.com/library/dn708504.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="7b181-117">[Azure (classic deployment model)](https://msdn.microsoft.com/library/dn708504.aspx) commands</span></span> |`Add-AzureAccount -Environment AzureGermanCloud` |
| <span data-ttu-id="7b181-118">[Azure (Resource Manager deployment model)](https://msdn.microsoft.com/library/mt125356.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="7b181-118">[Azure (Resource Manager deployment model)](https://msdn.microsoft.com/library/mt125356.aspx) commands</span></span> |`Connect-AzureRmAccount -EnvironmentName AzureGermanCloud` |
| <span data-ttu-id="7b181-119">[Azure Active Directory (classic deployment model)](https://msdn.microsoft.com/library/azure/jj151815.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="7b181-119">[Azure Active Directory (classic deployment model)](https://msdn.microsoft.com/library/azure/jj151815.aspx) commands</span></span> |`Connect-MsolService -AzureEnvironment AzureGermanyCloud` |
| <span data-ttu-id="7b181-120">[Azure Active Directory (Resource Manager deployment model)](https://msdn.microsoft.com/library/azure/mt757189.aspx) commands</span><span class="sxs-lookup"><span data-stu-id="7b181-120">[Azure Active Directory (Resource Manager deployment model)](https://msdn.microsoft.com/library/azure/mt757189.aspx) commands</span></span> |`Connect-AzureAD -AzureEnvironmentName AzureGermanyCloud` |

<span data-ttu-id="7b181-121">You can also use the `Environment` switch when connecting to a storage account by using `New-AzureStorageContext`, and then specify `AzureGermanCloud`.</span><span class="sxs-lookup"><span data-stu-id="7b181-121">You can also use the `Environment` switch when connecting to a storage account by using `New-AzureStorageContext`, and then specify `AzureGermanCloud`.</span></span>

## <a name="determining-region"></a><span data-ttu-id="7b181-122">Determining region</span><span class="sxs-lookup"><span data-stu-id="7b181-122">Determining region</span></span>
<span data-ttu-id="7b181-123">After you're connected, there is one more difference: the regions that are used to target a service.</span><span class="sxs-lookup"><span data-stu-id="7b181-123">After you're connected, there is one more difference: the regions that are used to target a service.</span></span> <span data-ttu-id="7b181-124">Every Azure cloud service has different regions.</span><span class="sxs-lookup"><span data-stu-id="7b181-124">Every Azure cloud service has different regions.</span></span> <span data-ttu-id="7b181-125">You can see them listed on the service availability page.</span><span class="sxs-lookup"><span data-stu-id="7b181-125">You can see them listed on the service availability page.</span></span> <span data-ttu-id="7b181-126">You normally use the region in the `Location` parameter for a command.</span><span class="sxs-lookup"><span data-stu-id="7b181-126">You normally use the region in the `Location` parameter for a command.</span></span>


| <span data-ttu-id="7b181-127">Common name</span><span class="sxs-lookup"><span data-stu-id="7b181-127">Common name</span></span> | <span data-ttu-id="7b181-128">Display name</span><span class="sxs-lookup"><span data-stu-id="7b181-128">Display name</span></span> | <span data-ttu-id="7b181-129">Location name</span><span class="sxs-lookup"><span data-stu-id="7b181-129">Location name</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b181-130">Germany Central</span><span class="sxs-lookup"><span data-stu-id="7b181-130">Germany Central</span></span> |`Germany Central` | `germanycentral` |
| <span data-ttu-id="7b181-131">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="7b181-131">Germany Northeast</span></span> |`Germany Northeast` | `germanynortheast` |


> [!NOTE]
> <span data-ttu-id="7b181-132">As is true with PowerShell for global Azure, you can use either the display name or the location name for the `Location` parameter.</span><span class="sxs-lookup"><span data-stu-id="7b181-132">As is true with PowerShell for global Azure, you can use either the display name or the location name for the `Location` parameter.</span></span>
>
>

<span data-ttu-id="7b181-133">If you ever want to validate the available regions in Azure Germany, you can run the following commands and print the current list.</span><span class="sxs-lookup"><span data-stu-id="7b181-133">If you ever want to validate the available regions in Azure Germany, you can run the following commands and print the current list.</span></span> <span data-ttu-id="7b181-134">For classic deployments, use the first command.</span><span class="sxs-lookup"><span data-stu-id="7b181-134">For classic deployments, use the first command.</span></span> <span data-ttu-id="7b181-135">For Resource Manager deployments, use the second command.</span><span class="sxs-lookup"><span data-stu-id="7b181-135">For Resource Manager deployments, use the second command.</span></span>

    Get-AzureLocation
    Get-AzureRmLocation

<span data-ttu-id="7b181-136">If you're curious about the available environments across Azure, you can run:</span><span class="sxs-lookup"><span data-stu-id="7b181-136">If you're curious about the available environments across Azure, you can run:</span></span>

    Get-AzureEnvironment
    Get-AzureRmEnvironment

## <a name="next-steps"></a><span data-ttu-id="7b181-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b181-137">Next steps</span></span>
<span data-ttu-id="7b181-138">For more information about connecting to Azure Germany, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="7b181-138">For more information about connecting to Azure Germany, see the following resources:</span></span>

* [<span data-ttu-id="7b181-139">Connect to Azure Germany by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b181-139">Connect to Azure Germany by using Azure CLI</span></span>](./germany-get-started-connect-with-cli.md)
* [<span data-ttu-id="7b181-140">Connect to Azure Germany by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b181-140">Connect to Azure Germany by using Visual Studio</span></span>](./germany-get-started-connect-with-vs.md)
* [<span data-ttu-id="7b181-141">Connect to Azure Germany by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7b181-141">Connect to Azure Germany by using the Azure portal</span></span>](./germany-get-started-connect-with-portal.md)




