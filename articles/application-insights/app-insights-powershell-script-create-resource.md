---
title: PowerShell script to create an Application Insights resource | Microsoft Docs
description: Automate creation of Application Insights resources.
services: application-insights
documentationcenter: windows
author: mrbullwinkle
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 11/19/2016
ms.author: mbullwin
ms.openlocfilehash: 0f2bf1e318729ae8ccb0f4f521b2a795cf932a86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803938"
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="702e3-103">PowerShell script to create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="702e3-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="702e3-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="702e3-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="702e3-105">This resource is where the telemetry data from your app is analyzed and displayed.</span><span class="sxs-lookup"><span data-stu-id="702e3-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="702e3-106">You can automate the creation of a new resource by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="702e3-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="702e3-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span><span class="sxs-lookup"><span data-stu-id="702e3-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="702e3-108">You don't want to get the telemetry results from different versions mixed up.</span><span class="sxs-lookup"><span data-stu-id="702e3-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="702e3-109">So you get your build process to create a new resource for each build.</span><span class="sxs-lookup"><span data-stu-id="702e3-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="702e3-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="702e3-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="702e3-111">Script to create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="702e3-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="702e3-112">See the relevant cmdlet specs:</span><span class="sxs-lookup"><span data-stu-id="702e3-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="702e3-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="702e3-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="702e3-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="702e3-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="702e3-115">*PowerShell Script*</span><span class="sxs-lookup"><span data-stu-id="702e3-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Connect-AzureRmAccount / Connect-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="702e3-116">What to do with the iKey</span><span class="sxs-lookup"><span data-stu-id="702e3-116">What to do with the iKey</span></span>
<span data-ttu-id="702e3-117">Each resource is identified by its instrumentation key (iKey).</span><span class="sxs-lookup"><span data-stu-id="702e3-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="702e3-118">The iKey is an output of the resource creation script.</span><span class="sxs-lookup"><span data-stu-id="702e3-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="702e3-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span><span class="sxs-lookup"><span data-stu-id="702e3-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="702e3-120">There are two ways to make the iKey available to the SDK:</span><span class="sxs-lookup"><span data-stu-id="702e3-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="702e3-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="702e3-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="702e3-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="702e3-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="702e3-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="702e3-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="702e3-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="702e3-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="702e3-125">See also</span><span class="sxs-lookup"><span data-stu-id="702e3-125">See also</span></span>
* [<span data-ttu-id="702e3-126">Create Application Insights and web test resources from templates</span><span class="sxs-lookup"><span data-stu-id="702e3-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="702e3-127">Set up monitoring of Azure diagnostics with PowerShell</span><span class="sxs-lookup"><span data-stu-id="702e3-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="702e3-128">Set alerts by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="702e3-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

