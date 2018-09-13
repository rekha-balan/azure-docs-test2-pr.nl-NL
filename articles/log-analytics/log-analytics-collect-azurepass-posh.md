---
title: Collect Azure PaaS resource metrics with Log Analytics | Microsoft Docs
description: Learn how to enable Azure PaaS resource metrics collection using PowerShell for retention and analysis in Log Analytics.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 11/13/2017
ms.author: magoedte
ms.component: na
ms.openlocfilehash: b44a6627ab12c8a4ad21e7beded7c5fd2c2e1d39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855829"
---
# <a name="configure-collection-of-azure-paas-resource-metrics-with-log-analytics"></a><span data-ttu-id="f3d5b-103">Configure collection of Azure PaaS resource metrics with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f3d5b-103">Configure collection of Azure PaaS resource metrics with Log Analytics</span></span>

<span data-ttu-id="f3d5b-104">Azure Platform as a Service (PaaS) resources, like Azure SQL and Web Sites (Web Apps), can emit performance metrics data natively to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-104">Azure Platform as a Service (PaaS) resources, like Azure SQL and Web Sites (Web Apps), can emit performance metrics data natively to Log Analytics.</span></span> <span data-ttu-id="f3d5b-105">This script allows users to enable metrics logging for PaaS resources already deployed in a specific resource group or across an entire subscription.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-105">This script allows users to enable metrics logging for PaaS resources already deployed in a specific resource group or across an entire subscription.</span></span> 

<span data-ttu-id="f3d5b-106">Today, there is no way to enable metrics logging for PaaS resources through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-106">Today, there is no way to enable metrics logging for PaaS resources through the Azure portal.</span></span> <span data-ttu-id="f3d5b-107">Therefore, you need to use a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-107">Therefore, you need to use a PowerShell script.</span></span> <span data-ttu-id="f3d5b-108">This native metrics logging capability along with Log Analytics monitoring, enable you to monitor Azure resources at scale.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-108">This native metrics logging capability along with Log Analytics monitoring, enable you to monitor Azure resources at scale.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f3d5b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f3d5b-109">Prerequisites</span></span>
<span data-ttu-id="f3d5b-110">Verify you have the following Azure Resource Manager modules installed on your computer before proceeding:</span><span class="sxs-lookup"><span data-stu-id="f3d5b-110">Verify you have the following Azure Resource Manager modules installed on your computer before proceeding:</span></span>

- <span data-ttu-id="f3d5b-111">AzureRM.Insights</span><span class="sxs-lookup"><span data-stu-id="f3d5b-111">AzureRM.Insights</span></span>
- <span data-ttu-id="f3d5b-112">AzureRM.OperationalInsights</span><span class="sxs-lookup"><span data-stu-id="f3d5b-112">AzureRM.OperationalInsights</span></span>
- <span data-ttu-id="f3d5b-113">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="f3d5b-113">AzureRM.Resources</span></span>
- <span data-ttu-id="f3d5b-114">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="f3d5b-114">AzureRM.profile</span></span>

>[!NOTE]
><span data-ttu-id="f3d5b-115">We recommend that all your Azure Resource Manager modules are the same version to ensure compatibility when you run Azure Resource Manager commands from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-115">We recommend that all your Azure Resource Manager modules are the same version to ensure compatibility when you run Azure Resource Manager commands from PowerShell.</span></span>
>
<span data-ttu-id="f3d5b-116">To install the latest version of the Azure Resource Manager modules on your computer, see [Install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.4.1#update-azps).</span><span class="sxs-lookup"><span data-stu-id="f3d5b-116">To install the latest version of the Azure Resource Manager modules on your computer, see [Install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.4.1#update-azps).</span></span>  

## <a name="enable-azure-diagnostics"></a><span data-ttu-id="f3d5b-117">Enable Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f3d5b-117">Enable Azure Diagnostics</span></span>  
<span data-ttu-id="f3d5b-118">Configuring Azure Diagnostics for PaaS resources is accomplished by executing the script, **Enable-AzureRMDiagnostics.ps1**, which is available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/Enable-AzureRMDiagnostics/2.52/DisplayScript).</span><span class="sxs-lookup"><span data-stu-id="f3d5b-118">Configuring Azure Diagnostics for PaaS resources is accomplished by executing the script, **Enable-AzureRMDiagnostics.ps1**, which is available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/Enable-AzureRMDiagnostics/2.52/DisplayScript).</span></span>  <span data-ttu-id="f3d5b-119">The script supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="f3d5b-119">The script supports the following scenarios:</span></span>
  
* <span data-ttu-id="f3d5b-120">Specifying a resource related to one or more resource groups in a subscription</span><span class="sxs-lookup"><span data-stu-id="f3d5b-120">Specifying a resource related to one or more resource groups in a subscription</span></span>  
* <span data-ttu-id="f3d5b-121">Specifying a resource related to a specific resource group in a subscription</span><span class="sxs-lookup"><span data-stu-id="f3d5b-121">Specifying a resource related to a specific resource group in a subscription</span></span>  
* <span data-ttu-id="f3d5b-122">Reconfigure a resource to forward to a different workspace</span><span class="sxs-lookup"><span data-stu-id="f3d5b-122">Reconfigure a resource to forward to a different workspace</span></span>

<span data-ttu-id="f3d5b-123">Only resources that support collecting metrics with Azure diagnostics and send directly to Log Analytics are supported.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-123">Only resources that support collecting metrics with Azure diagnostics and send directly to Log Analytics are supported.</span></span>  <span data-ttu-id="f3d5b-124">For a detailed list, review [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="f3d5b-124">For a detailed list, review [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md)</span></span> 

<span data-ttu-id="f3d5b-125">Perform the following steps to download and execute the script.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-125">Perform the following steps to download and execute the script.</span></span>

1.  <span data-ttu-id="f3d5b-126">From the Windows start screen, type **PowerShell** and right-click PowerShell from the search results.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-126">From the Windows start screen, type **PowerShell** and right-click PowerShell from the search results.</span></span>  <span data-ttu-id="f3d5b-127">Select from the menu **Run As Administrator**.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-127">Select from the menu **Run As Administrator**.</span></span>   
2. <span data-ttu-id="f3d5b-128">Save the **Enable-AzureRMDiagnostics.ps1** script file locally by running the following command and providing a path to store the script.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-128">Save the **Enable-AzureRMDiagnostics.ps1** script file locally by running the following command and providing a path to store the script.</span></span>    

    ```
    PS C:\> save-script -Name Enable-AzureRMDiagnostics -Path "C:\users\<username>\desktop\temp"
    ```

3. <span data-ttu-id="f3d5b-129">Run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-129">Run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>   
4. <span data-ttu-id="f3d5b-130">Run the following script `.\Enable-AzureRmDiagnostics.ps1` without any parameters to enable data collection from a specific resource in your subscription or with the parameter `-ResourceGroup <myResourceGroup>` to specify a resource in a specific resource group.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-130">Run the following script `.\Enable-AzureRmDiagnostics.ps1` without any parameters to enable data collection from a specific resource in your subscription or with the parameter `-ResourceGroup <myResourceGroup>` to specify a resource in a specific resource group.</span></span>   
5. <span data-ttu-id="f3d5b-131">Select the appropriate subscription from the list if you have more than one, by entering the correct value.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-131">Select the appropriate subscription from the list if you have more than one, by entering the correct value.</span></span><br><br> ![Select subscription returned by script](./media/log-analytics-collect-azurepass-posh/script-select-subscription.png)<br> <span data-ttu-id="f3d5b-133">Otherwise, it automatically selects the single subscription available.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-133">Otherwise, it automatically selects the single subscription available.</span></span>
6. <span data-ttu-id="f3d5b-134">Next, the script returns a list of Log Analytics workspaces registered in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-134">Next, the script returns a list of Log Analytics workspaces registered in the subscription.</span></span>  <span data-ttu-id="f3d5b-135">Select the appropriate one from the list.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-135">Select the appropriate one from the list.</span></span><br><br> ![Select workspace returned by script](./media/log-analytics-collect-azurepass-posh/script-select-workspace.png)<br> 
7. <span data-ttu-id="f3d5b-137">Select the Azure resource that you would like to enable collection from.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-137">Select the Azure resource that you would like to enable collection from.</span></span> <span data-ttu-id="f3d5b-138">For example, if you type 5, you enable data collection for SQL Azure Databases.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-138">For example, if you type 5, you enable data collection for SQL Azure Databases.</span></span><br><br> <span data-ttu-id="f3d5b-139">![Select resource type returned by script](./media/log-analytics-collect-azurepass-posh/script-select-resource.png)</span><span class="sxs-lookup"><span data-stu-id="f3d5b-139">![Select resource type returned by script](./media/log-analytics-collect-azurepass-posh/script-select-resource.png)</span></span><br>
   <span data-ttu-id="f3d5b-140">You can only select resources that support collecting metrics with Azure Diagnostics and sending directly to a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-140">You can only select resources that support collecting metrics with Azure Diagnostics and sending directly to a Log Analytics.</span></span>  <span data-ttu-id="f3d5b-141">The script will show a value of **True** under the **Metrics** column for the list of resources it discovers in your subscription or specified resource group.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-141">The script will show a value of **True** under the **Metrics** column for the list of resources it discovers in your subscription or specified resource group.</span></span>    
8. <span data-ttu-id="f3d5b-142">You are prompted to confirm your selection.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-142">You are prompted to confirm your selection.</span></span>  <span data-ttu-id="f3d5b-143">Enter **Y** to enable metrics logging for all selected resources for the scope defined, which in our example are all SQL databases in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-143">Enter **Y** to enable metrics logging for all selected resources for the scope defined, which in our example are all SQL databases in the subscription.</span></span>  

<span data-ttu-id="f3d5b-144">The script will run against each and every resource matching selected criteria and enable metrics collection for them.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-144">The script will run against each and every resource matching selected criteria and enable metrics collection for them.</span></span> <span data-ttu-id="f3d5b-145">After it’s finished, you will see a message indicating configuration is complete.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-145">After it’s finished, you will see a message indicating configuration is complete.</span></span>  

<span data-ttu-id="f3d5b-146">Shortly after completion, you will start to see data from the Azure PaaS resource in your Log Analytics repository.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-146">Shortly after completion, you will start to see data from the Azure PaaS resource in your Log Analytics repository.</span></span>  <span data-ttu-id="f3d5b-147">A record with type `AzureMetrics` is created and analyzing these records are supported by the [Azure SQL Analytics](log-analytics-azure-sql.md) and [Azure Web Apps Analytics](log-analytics-azure-web-apps-analytics.md) management solutions.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-147">A record with type `AzureMetrics` is created and analyzing these records are supported by the [Azure SQL Analytics](log-analytics-azure-sql.md) and [Azure Web Apps Analytics](log-analytics-azure-web-apps-analytics.md) management solutions.</span></span>   

## <a name="update-a-resource-to-send-data-to-another-workspace"></a><span data-ttu-id="f3d5b-148">Update a resource to send data to another workspace</span><span class="sxs-lookup"><span data-stu-id="f3d5b-148">Update a resource to send data to another workspace</span></span>
<span data-ttu-id="f3d5b-149">If you have a resource that is already sending data to a Log Analytics workspace and you later decide to reconfigure it to reference another workspace, you can run the script with the `-Update` parameter.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-149">If you have a resource that is already sending data to a Log Analytics workspace and you later decide to reconfigure it to reference another workspace, you can run the script with the `-Update` parameter.</span></span>  

<span data-ttu-id="f3d5b-150">**Example:** 
`PS C:\users\<username>\Desktop\temp> .\Enable-AzureRMDiagnostics.ps1 -Update`</span><span class="sxs-lookup"><span data-stu-id="f3d5b-150">**Example:** 
`PS C:\users\<username>\Desktop\temp> .\Enable-AzureRMDiagnostics.ps1 -Update`</span></span>

<span data-ttu-id="f3d5b-151">You will be prompted to answer the same information as when you ran the script to perform the initial configuration.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-151">You will be prompted to answer the same information as when you ran the script to perform the initial configuration.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f3d5b-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3d5b-152">Next steps</span></span>

* <span data-ttu-id="f3d5b-153">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-153">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 

* <span data-ttu-id="f3d5b-154">Use [Custom Fields](log-analytics-custom-fields.md)( to parse the event records into individual fields.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-154">Use [Custom Fields](log-analytics-custom-fields.md)( to parse the event records into individual fields.</span></span>

* <span data-ttu-id="f3d5b-155">Review [Create a custom dashboard for use in Log Analytics](log-analytics-dashboards.md) to understand how to visualize your log searches in meaningful ways for the organization.</span><span class="sxs-lookup"><span data-stu-id="f3d5b-155">Review [Create a custom dashboard for use in Log Analytics](log-analytics-dashboards.md) to understand how to visualize your log searches in meaningful ways for the organization.</span></span>
