---
title: Guest OS family 1 retirement notice | Microsoft Docs
description: Provides information about when the Azure Guest OS Family 1 retirement happened and how to determine if you are affected
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: ''
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782488"
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="e5862-103">Guest OS Family 1 retirement notice</span><span class="sxs-lookup"><span data-stu-id="e5862-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="e5862-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span><span class="sxs-lookup"><span data-stu-id="e5862-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="e5862-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span><span class="sxs-lookup"><span data-stu-id="e5862-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="e5862-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span><span class="sxs-lookup"><span data-stu-id="e5862-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="e5862-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span><span class="sxs-lookup"><span data-stu-id="e5862-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="e5862-108">All services still on Family 1 will be impacted.</span><span class="sxs-lookup"><span data-stu-id="e5862-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="e5862-109">We may stop those services at any time.</span><span class="sxs-lookup"><span data-stu-id="e5862-109">We may stop those services at any time.</span></span> <span data-ttu-id="e5862-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span><span class="sxs-lookup"><span data-stu-id="e5862-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="e5862-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="e5862-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="e5862-112">Are you affected?</span><span class="sxs-lookup"><span data-stu-id="e5862-112">Are you affected?</span></span>
<span data-ttu-id="e5862-113">Your Cloud Services are affected if any one of the following applies:</span><span class="sxs-lookup"><span data-stu-id="e5862-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="e5862-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="e5862-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="e5862-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="e5862-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="e5862-116">Currently, the system uses the default value of "1" in this case.</span><span class="sxs-lookup"><span data-stu-id="e5862-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="e5862-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="e5862-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="e5862-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span><span class="sxs-lookup"><span data-stu-id="e5862-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="e5862-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5862-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="e5862-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span><span class="sxs-lookup"><span data-stu-id="e5862-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="e5862-121">Recommendations if you are affected</span><span class="sxs-lookup"><span data-stu-id="e5862-121">Recommendations if you are affected</span></span>
<span data-ttu-id="e5862-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span><span class="sxs-lookup"><span data-stu-id="e5862-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="e5862-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span><span class="sxs-lookup"><span data-stu-id="e5862-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="e5862-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="e5862-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="e5862-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span><span class="sxs-lookup"><span data-stu-id="e5862-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="e5862-126">**Guest OS family 3.x** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e5862-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="e5862-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span><span class="sxs-lookup"><span data-stu-id="e5862-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="e5862-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span><span class="sxs-lookup"><span data-stu-id="e5862-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="e5862-129">**Guest OS family 2.x** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="e5862-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="e5862-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span><span class="sxs-lookup"><span data-stu-id="e5862-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="e5862-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span><span class="sxs-lookup"><span data-stu-id="e5862-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="e5862-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span><span class="sxs-lookup"><span data-stu-id="e5862-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="e5862-133">Cloud services on Guest OS family 1 are no longer supported.</span><span class="sxs-lookup"><span data-stu-id="e5862-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="e5862-134">Migrate off family 1 as soon as possible to avoid service disruption.</span><span class="sxs-lookup"><span data-stu-id="e5862-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e5862-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5862-135">Next steps</span></span>
<span data-ttu-id="e5862-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="e5862-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
