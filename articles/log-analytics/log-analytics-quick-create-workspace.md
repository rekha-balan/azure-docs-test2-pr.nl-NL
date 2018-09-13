---
title: Create a Log Analytics workspace in the Azure Portal | Microsoft Docs
description: Learn how to create a Log Analytics workspace to enable management solutions and data collection from your cloud and on-premises environments in the Azure portal.
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
ms.topic: conceptal
ms.date: 08/23/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: bdf1d1a62bd8e2e1d0a0a8ad30f2d4c4833be0e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969110"
---
# <a name="create-a-log-analytics-workspace-in-the-azure-portal"></a><span data-ttu-id="3768f-103">Create a Log Analytics workspace in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3768f-103">Create a Log Analytics workspace in the Azure portal</span></span>
<span data-ttu-id="3768f-104">In the Azure portal you can set up a Log Analytics workspace, which is a unique Log Analytics environment with its own data repository, data sources, and solutions.</span><span class="sxs-lookup"><span data-stu-id="3768f-104">In the Azure portal you can set up a Log Analytics workspace, which is a unique Log Analytics environment with its own data repository, data sources, and solutions.</span></span>  <span data-ttu-id="3768f-105">The steps described in this article are required if you intend on collecting data from the following sources:</span><span class="sxs-lookup"><span data-stu-id="3768f-105">The steps described in this article are required if you intend on collecting data from the following sources:</span></span>

* <span data-ttu-id="3768f-106">Azure resources in your subscription</span><span class="sxs-lookup"><span data-stu-id="3768f-106">Azure resources in your subscription</span></span>
* <span data-ttu-id="3768f-107">On-premises computers monitored by System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3768f-107">On-premises computers monitored by System Center Operations Manager</span></span>
* <span data-ttu-id="3768f-108">Device collections from System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="3768f-108">Device collections from System Center Configuration Manager</span></span> 
* <span data-ttu-id="3768f-109">Diagnostic or log data from Azure storage</span><span class="sxs-lookup"><span data-stu-id="3768f-109">Diagnostic or log data from Azure storage</span></span>

<span data-ttu-id="3768f-110">For other sources, such as Azure VMs and Windows or Linux VMs in your environment, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="3768f-110">For other sources, such as Azure VMs and Windows or Linux VMs in your environment, see the following topics:</span></span>

*  [<span data-ttu-id="3768f-111">Collect data from Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="3768f-111">Collect data from Azure virtual machines</span></span>](log-analytics-quick-collect-azurevm.md) 
*  [<span data-ttu-id="3768f-112">Collect data from hybrid Linux computer</span><span class="sxs-lookup"><span data-stu-id="3768f-112">Collect data from hybrid Linux computer</span></span>](log-analytics-quick-collect-linux-computer.md)
*  [<span data-ttu-id="3768f-113">Collect data from hybrid Windows computer</span><span class="sxs-lookup"><span data-stu-id="3768f-113">Collect data from hybrid Windows computer</span></span>](log-analytics-quick-collect-windows-computer.md)

<span data-ttu-id="3768f-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3768f-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="sign-in-to-azure-portal"></a><span data-ttu-id="3768f-115">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="3768f-115">Sign in to Azure portal</span></span>
<span data-ttu-id="3768f-116">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3768f-116">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span> 

## <a name="create-a-workspace"></a><span data-ttu-id="3768f-117">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="3768f-117">Create a workspace</span></span>
1. <span data-ttu-id="3768f-118">In the Azure portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="3768f-118">In the Azure portal, click **All services**.</span></span> <span data-ttu-id="3768f-119">In the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3768f-119">In the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="3768f-120">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="3768f-120">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="3768f-121">Select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3768f-121">Select **Log Analytics**.</span></span>

    ![Azure portal](media/log-analytics-quick-collect-azurevm/azure-portal-01.png)
  
2. <span data-ttu-id="3768f-123">Click **Create**, and then select choices for the following items:</span><span class="sxs-lookup"><span data-stu-id="3768f-123">Click **Create**, and then select choices for the following items:</span></span>

  * <span data-ttu-id="3768f-124">Provide a name for the new **OMS Workspace**, such as *DefaultLAWorkspace*.</span><span class="sxs-lookup"><span data-stu-id="3768f-124">Provide a name for the new **OMS Workspace**, such as *DefaultLAWorkspace*.</span></span> 
  * <span data-ttu-id="3768f-125">Select a **Subscription** to link to by selecting from the drop-down list if the default selected is not appropriate.</span><span class="sxs-lookup"><span data-stu-id="3768f-125">Select a **Subscription** to link to by selecting from the drop-down list if the default selected is not appropriate.</span></span>
  * <span data-ttu-id="3768f-126">For **Resource Group**, choose to use an existing resource group already setup or create a new one.</span><span class="sxs-lookup"><span data-stu-id="3768f-126">For **Resource Group**, choose to use an existing resource group already setup or create a new one.</span></span>  
  * <span data-ttu-id="3768f-127">Select an available **Location**.</span><span class="sxs-lookup"><span data-stu-id="3768f-127">Select an available **Location**.</span></span>  <span data-ttu-id="3768f-128">For more information, see which [regions Log Analytics is available in](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="3768f-128">For more information, see which [regions Log Analytics is available in](https://azure.microsoft.com/regions/services/).</span></span>
  * <span data-ttu-id="3768f-129">If you are creating a workspace in a new subscription created after April 2, 2018, it will automatically use the *Per GB* pricing plan and the option to select a pricing tier will not be available.</span><span class="sxs-lookup"><span data-stu-id="3768f-129">If you are creating a workspace in a new subscription created after April 2, 2018, it will automatically use the *Per GB* pricing plan and the option to select a pricing tier will not be available.</span></span>  <span data-ttu-id="3768f-130">If you are creating a workspace for an existing subscription created before April 2, or to subscription that was tied to an existing Enterprise Agreement (EA) enrollment, select your preferred pricing tier.</span><span class="sxs-lookup"><span data-stu-id="3768f-130">If you are creating a workspace for an existing subscription created before April 2, or to subscription that was tied to an existing Enterprise Agreement (EA) enrollment, select your preferred pricing tier.</span></span>  <span data-ttu-id="3768f-131">For more information about the particular tiers, see [Log Analytics Pricing Details](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3768f-131">For more information about the particular tiers, see [Log Analytics Pricing Details](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span>

        ![Create Log Analytics resource blade](media/log-analytics-quick-collect-azurevm/create-loganalytics-workspace-02.png)  

3. <span data-ttu-id="3768f-132">After providing the required information on the **OMS Workspace** pane, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3768f-132">After providing the required information on the **OMS Workspace** pane, click **OK**.</span></span>  

<span data-ttu-id="3768f-133">While the information is verified and the workspace is created, you can track its progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="3768f-133">While the information is verified and the workspace is created, you can track its progress under **Notifications** from the menu.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3768f-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="3768f-134">Next steps</span></span>
<span data-ttu-id="3768f-135">Now that you have a workspace available, you can configure collection of monitoring telemetry, run log searches to analyze that data, and add a management solution to provide additional data and analytic insights.</span><span class="sxs-lookup"><span data-stu-id="3768f-135">Now that you have a workspace available, you can configure collection of monitoring telemetry, run log searches to analyze that data, and add a management solution to provide additional data and analytic insights.</span></span> 

* <span data-ttu-id="3768f-136">To enable data collection from Azure resources with Azure Diagnostics or Azure storage, see [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3768f-136">To enable data collection from Azure resources with Azure Diagnostics or Azure storage, see [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md).</span></span>  
* <span data-ttu-id="3768f-137">[Add System Center Operations Manager as a data source](log-analytics-om-agents.md) to collect data from agents reporting your Operations Manager management group and store it in your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="3768f-137">[Add System Center Operations Manager as a data source](log-analytics-om-agents.md) to collect data from agents reporting your Operations Manager management group and store it in your Log Analytics workspace.</span></span> 
* <span data-ttu-id="3768f-138">Connect [Configuration Manager](log-analytics-sccm.md) to import computers that are members of collections in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="3768f-138">Connect [Configuration Manager](log-analytics-sccm.md) to import computers that are members of collections in the hierarchy.</span></span>  
* <span data-ttu-id="3768f-139">Review the [management solutions](log-analytics-add-solutions.md) available and how to add or remove a solution from your workspace.</span><span class="sxs-lookup"><span data-stu-id="3768f-139">Review the [management solutions](log-analytics-add-solutions.md) available and how to add or remove a solution from your workspace.</span></span>
