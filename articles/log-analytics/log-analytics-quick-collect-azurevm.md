---
title: Collect data about Azure Virtual Machines | Microsoft Docs
description: Learn how to enable the OMS Agent VM Extension and enable collection of data from your Azure VMs with Log Analytics.
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
ms.topic: quickstart
ms.date: 06/26/2018
ms.author: magoedte
ms.custom: mvc
ms.component: na
ms.openlocfilehash: a79679068b03103bd8ca63455dd2d1758751aa6f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858004"
---
# <a name="collect-data-about-azure-virtual-machines"></a><span data-ttu-id="36225-103">Collect data about Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="36225-103">Collect data about Azure Virtual Machines</span></span>
<span data-ttu-id="36225-104">[Azure Log Analytics](log-analytics-overview.md) can collect data directly from your Azure virtual machines and other resources in your environment into a single repository for detailed analysis and correlation.</span><span class="sxs-lookup"><span data-stu-id="36225-104">[Azure Log Analytics](log-analytics-overview.md) can collect data directly from your Azure virtual machines and other resources in your environment into a single repository for detailed analysis and correlation.</span></span>  <span data-ttu-id="36225-105">This quickstart shows you how to configure and collect data from your Azure Linux or Windows VMs with a few easy steps.</span><span class="sxs-lookup"><span data-stu-id="36225-105">This quickstart shows you how to configure and collect data from your Azure Linux or Windows VMs with a few easy steps.</span></span>  
 
<span data-ttu-id="36225-106">This quickstart assumes you have an existing Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="36225-106">This quickstart assumes you have an existing Azure virtual machine.</span></span> <span data-ttu-id="36225-107">If not you can [create a Windows VM](../virtual-machines/windows/quick-create-portal.md) or [create a Linux VM](../virtual-machines/linux/quick-create-cli.md) following our VM quickstarts.</span><span class="sxs-lookup"><span data-stu-id="36225-107">If not you can [create a Windows VM](../virtual-machines/windows/quick-create-portal.md) or [create a Linux VM](../virtual-machines/linux/quick-create-cli.md) following our VM quickstarts.</span></span>

## <a name="log-in-to-azure-portal"></a><span data-ttu-id="36225-108">Log in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="36225-108">Log in to Azure portal</span></span>
<span data-ttu-id="36225-109">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36225-109">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span> 

## <a name="create-a-workspace"></a><span data-ttu-id="36225-110">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="36225-110">Create a workspace</span></span>
1. <span data-ttu-id="36225-111">In the Azure portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="36225-111">In the Azure portal, click **All services**.</span></span> <span data-ttu-id="36225-112">In the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="36225-112">In the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="36225-113">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="36225-113">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="36225-114">Select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="36225-114">Select **Log Analytics**.</span></span>

    ![Azure portal](media/log-analytics-quick-collect-azurevm/azure-portal-01.png)<br>  

2. <span data-ttu-id="36225-116">Click **Create**, and then select choices for the following items:</span><span class="sxs-lookup"><span data-stu-id="36225-116">Click **Create**, and then select choices for the following items:</span></span>

  * <span data-ttu-id="36225-117">Provide a name for the new **OMS Workspace**, such as *DefaultLAWorkspace*.</span><span class="sxs-lookup"><span data-stu-id="36225-117">Provide a name for the new **OMS Workspace**, such as *DefaultLAWorkspace*.</span></span> 
  * <span data-ttu-id="36225-118">Select a **Subscription** to link to by selecting from the drop-down list if the default selected is not appropriate.</span><span class="sxs-lookup"><span data-stu-id="36225-118">Select a **Subscription** to link to by selecting from the drop-down list if the default selected is not appropriate.</span></span>
  * <span data-ttu-id="36225-119">For **Resource Group**, select an existing resource group that contains one or more Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="36225-119">For **Resource Group**, select an existing resource group that contains one or more Azure virtual machines.</span></span>  
  * <span data-ttu-id="36225-120">Select the **Location** your VMs are deployed to.</span><span class="sxs-lookup"><span data-stu-id="36225-120">Select the **Location** your VMs are deployed to.</span></span>  <span data-ttu-id="36225-121">For additional information, see which [regions Log Analytics is available in](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="36225-121">For additional information, see which [regions Log Analytics is available in](https://azure.microsoft.com/regions/services/).</span></span>
  * <span data-ttu-id="36225-122">If you are creating a workspace in a new subscription created after April 2, 2018, it will automatically use the *Per GB* pricing plan and the option to select a pricing tier will not be available.</span><span class="sxs-lookup"><span data-stu-id="36225-122">If you are creating a workspace in a new subscription created after April 2, 2018, it will automatically use the *Per GB* pricing plan and the option to select a pricing tier will not be available.</span></span>  <span data-ttu-id="36225-123">If you are creating a workspace for an existing subscription created before April 2, or to subscription that was tied to an existing EA enrollment, select your preferred pricing tier.</span><span class="sxs-lookup"><span data-stu-id="36225-123">If you are creating a workspace for an existing subscription created before April 2, or to subscription that was tied to an existing EA enrollment, select your preferred pricing tier.</span></span>  <span data-ttu-id="36225-124">For additional information about the particular tiers, see [Log Analytics Pricing Details](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="36225-124">For additional information about the particular tiers, see [Log Analytics Pricing Details](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span>
  
        ![Create Log Analytics resource blade](media/log-analytics-quick-collect-azurevm/create-loganalytics-workspace-02.png) 

3. <span data-ttu-id="36225-125">After providing the required information on the **OMS Workspace** pane, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="36225-125">After providing the required information on the **OMS Workspace** pane, click **OK**.</span></span>  

<span data-ttu-id="36225-126">While the information is verified and the workspace is created, you can track its progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="36225-126">While the information is verified and the workspace is created, you can track its progress under **Notifications** from the menu.</span></span> 

## <a name="enable-the-log-analytics-vm-extension"></a><span data-ttu-id="36225-127">Enable the Log Analytics VM Extension</span><span class="sxs-lookup"><span data-stu-id="36225-127">Enable the Log Analytics VM Extension</span></span>
<span data-ttu-id="36225-128">For Windows and Linux virtual machines already deployed in Azure, you install the Log Analytics agent with the Log Analytics VM Extension.</span><span class="sxs-lookup"><span data-stu-id="36225-128">For Windows and Linux virtual machines already deployed in Azure, you install the Log Analytics agent with the Log Analytics VM Extension.</span></span>  <span data-ttu-id="36225-129">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span><span class="sxs-lookup"><span data-stu-id="36225-129">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="36225-130">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span><span class="sxs-lookup"><span data-stu-id="36225-130">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

>[!NOTE]
><span data-ttu-id="36225-131">The OMS agent for Linux cannot be configured to report to more than one Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="36225-131">The OMS agent for Linux cannot be configured to report to more than one Log Analytics workspace.</span></span> 

1. <span data-ttu-id="36225-132">In the Azure portal, click **All services** found in the upper left-hand corner.</span><span class="sxs-lookup"><span data-stu-id="36225-132">In the Azure portal, click **All services** found in the upper left-hand corner.</span></span> <span data-ttu-id="36225-133">In the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="36225-133">In the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="36225-134">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="36225-134">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="36225-135">Select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="36225-135">Select **Log Analytics**.</span></span>
2. <span data-ttu-id="36225-136">In your list of Log Analytics workspaces, select *DefaultLAWorkspace* created earlier.</span><span class="sxs-lookup"><span data-stu-id="36225-136">In your list of Log Analytics workspaces, select *DefaultLAWorkspace* created earlier.</span></span>
3. <span data-ttu-id="36225-137">On the left-hand menu, under Workspace Data Sources, click **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="36225-137">On the left-hand menu, under Workspace Data Sources, click **Virtual machines**.</span></span>  
4. <span data-ttu-id="36225-138">In the list of **Virtual machines**, select a virtual machine you want to install the agent on.</span><span class="sxs-lookup"><span data-stu-id="36225-138">In the list of **Virtual machines**, select a virtual machine you want to install the agent on.</span></span> <span data-ttu-id="36225-139">Notice that the **OMS connection status** for the VM indicates that it is **Not connected**.</span><span class="sxs-lookup"><span data-stu-id="36225-139">Notice that the **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>
5. <span data-ttu-id="36225-140">In the details for your virtual machine, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="36225-140">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="36225-141">The agent is automatically installed and configured for your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="36225-141">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="36225-142">This process takes a few minutes, during which time the **Status** is **Connecting**.</span><span class="sxs-lookup"><span data-stu-id="36225-142">This process takes a few minutes, during which time the **Status** is **Connecting**.</span></span>
6. <span data-ttu-id="36225-143">After you install and connect the agent, the **OMS connection status** will be updated with **This workspace**.</span><span class="sxs-lookup"><span data-stu-id="36225-143">After you install and connect the agent, the **OMS connection status** will be updated with **This workspace**.</span></span>

## <a name="collect-event-and-performance-data"></a><span data-ttu-id="36225-144">Collect event and performance data</span><span class="sxs-lookup"><span data-stu-id="36225-144">Collect event and performance data</span></span>
<span data-ttu-id="36225-145">Log Analytics can collect events from the Windows event logs or Linux Syslog and performance counters that you specify for longer term analysis and reporting, and take action when a particular condition is detected.</span><span class="sxs-lookup"><span data-stu-id="36225-145">Log Analytics can collect events from the Windows event logs or Linux Syslog and performance counters that you specify for longer term analysis and reporting, and take action when a particular condition is detected.</span></span>  <span data-ttu-id="36225-146">Follow these steps to configure collection of events from the Windows system log and Linux Syslog, and several common performance counters to start with.</span><span class="sxs-lookup"><span data-stu-id="36225-146">Follow these steps to configure collection of events from the Windows system log and Linux Syslog, and several common performance counters to start with.</span></span>  

### <a name="data-collection-from-windows-vm"></a><span data-ttu-id="36225-147">Data collection from Windows VM</span><span class="sxs-lookup"><span data-stu-id="36225-147">Data collection from Windows VM</span></span>
1. <span data-ttu-id="36225-148">Select **Advanced settings**.</span><span class="sxs-lookup"><span data-stu-id="36225-148">Select **Advanced settings**.</span></span>

    ![Log Analytics Advance Settings](media/log-analytics-quick-collect-azurevm/log-analytics-advanced-settings-01.png)

3. <span data-ttu-id="36225-150">Select **Data**, and then select **Windows Event Logs**.</span><span class="sxs-lookup"><span data-stu-id="36225-150">Select **Data**, and then select **Windows Event Logs**.</span></span>  
4. <span data-ttu-id="36225-151">You add an event log by typing in the name of the log.</span><span class="sxs-lookup"><span data-stu-id="36225-151">You add an event log by typing in the name of the log.</span></span>  <span data-ttu-id="36225-152">Type **System** and then click the plus sign **+**.</span><span class="sxs-lookup"><span data-stu-id="36225-152">Type **System** and then click the plus sign **+**.</span></span>  
5. <span data-ttu-id="36225-153">In the table, check the severities **Error** and **Warning**.</span><span class="sxs-lookup"><span data-stu-id="36225-153">In the table, check the severities **Error** and **Warning**.</span></span>   
6. <span data-ttu-id="36225-154">Click **Save** at the top of the page to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="36225-154">Click **Save** at the top of the page to save the configuration.</span></span>
7. <span data-ttu-id="36225-155">Select **Windows Performance Data** to enable collection of performance counters on a Windows computer.</span><span class="sxs-lookup"><span data-stu-id="36225-155">Select **Windows Performance Data** to enable collection of performance counters on a Windows computer.</span></span> 
8. <span data-ttu-id="36225-156">When you first configure Windows Performance counters for a new Log Analytics workspace, you are given the option to quickly create several common counters.</span><span class="sxs-lookup"><span data-stu-id="36225-156">When you first configure Windows Performance counters for a new Log Analytics workspace, you are given the option to quickly create several common counters.</span></span> <span data-ttu-id="36225-157">They are listed with a checkbox next to each.</span><span class="sxs-lookup"><span data-stu-id="36225-157">They are listed with a checkbox next to each.</span></span>

    ![Default Windows performance counters selected](media/log-analytics-quick-collect-azurevm/windows-perfcounters-default.png)<span data-ttu-id="36225-159">.</span><span class="sxs-lookup"><span data-stu-id="36225-159">.</span></span>

    <span data-ttu-id="36225-160">Click **Add the selected performance counters**.</span><span class="sxs-lookup"><span data-stu-id="36225-160">Click **Add the selected performance counters**.</span></span>  <span data-ttu-id="36225-161">They are added and preset with a ten second collection sample interval.</span><span class="sxs-lookup"><span data-stu-id="36225-161">They are added and preset with a ten second collection sample interval.</span></span>
  
9. <span data-ttu-id="36225-162">Click **Save** at the top of the page to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="36225-162">Click **Save** at the top of the page to save the configuration.</span></span>

### <a name="data-collection-from-linux-vm"></a><span data-ttu-id="36225-163">Data collection from Linux VM</span><span class="sxs-lookup"><span data-stu-id="36225-163">Data collection from Linux VM</span></span>

1. <span data-ttu-id="36225-164">Select **Syslog**.</span><span class="sxs-lookup"><span data-stu-id="36225-164">Select **Syslog**.</span></span>  
2. <span data-ttu-id="36225-165">You add an event log by typing in the name of the log.</span><span class="sxs-lookup"><span data-stu-id="36225-165">You add an event log by typing in the name of the log.</span></span>  <span data-ttu-id="36225-166">Type **Syslog** and then click the plus sign **+**.</span><span class="sxs-lookup"><span data-stu-id="36225-166">Type **Syslog** and then click the plus sign **+**.</span></span>  
3. <span data-ttu-id="36225-167">In the table, uncheck the severities **Info**, **Notice** and **Debug**.</span><span class="sxs-lookup"><span data-stu-id="36225-167">In the table, uncheck the severities **Info**, **Notice** and **Debug**.</span></span> 
4. <span data-ttu-id="36225-168">Click **Save** at the top of the page to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="36225-168">Click **Save** at the top of the page to save the configuration.</span></span>
5. <span data-ttu-id="36225-169">Select **Linux Performance Data** to enable collection of performance counters on a Linux computer.</span><span class="sxs-lookup"><span data-stu-id="36225-169">Select **Linux Performance Data** to enable collection of performance counters on a Linux computer.</span></span> 
6. <span data-ttu-id="36225-170">When you first configure Linux Performance counters for a new Log Analytics workspace, you are given the option to quickly create several common counters.</span><span class="sxs-lookup"><span data-stu-id="36225-170">When you first configure Linux Performance counters for a new Log Analytics workspace, you are given the option to quickly create several common counters.</span></span> <span data-ttu-id="36225-171">They are listed with a checkbox next to each.</span><span class="sxs-lookup"><span data-stu-id="36225-171">They are listed with a checkbox next to each.</span></span>

    ![Default Windows performance counters selected](media/log-analytics-quick-collect-azurevm/linux-perfcounters-default.png)<span data-ttu-id="36225-173">.</span><span class="sxs-lookup"><span data-stu-id="36225-173">.</span></span>

    <span data-ttu-id="36225-174">Click **Add the selected performance counters**.</span><span class="sxs-lookup"><span data-stu-id="36225-174">Click **Add the selected performance counters**.</span></span>  <span data-ttu-id="36225-175">They are added and preset with a ten second collection sample interval.</span><span class="sxs-lookup"><span data-stu-id="36225-175">They are added and preset with a ten second collection sample interval.</span></span>  

7. <span data-ttu-id="36225-176">Click **Save** at the top of the page to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="36225-176">Click **Save** at the top of the page to save the configuration.</span></span>

## <a name="view-data-collected"></a><span data-ttu-id="36225-177">View data collected</span><span class="sxs-lookup"><span data-stu-id="36225-177">View data collected</span></span>
<span data-ttu-id="36225-178">Now that you have enabled data collection, lets run a simple log search example to see some data from the target VMs.</span><span class="sxs-lookup"><span data-stu-id="36225-178">Now that you have enabled data collection, lets run a simple log search example to see some data from the target VMs.</span></span>  

1. <span data-ttu-id="36225-179">In the Azure portal, navigate to Log Analytics and select the workspace created earlier.</span><span class="sxs-lookup"><span data-stu-id="36225-179">In the Azure portal, navigate to Log Analytics and select the workspace created earlier.</span></span>
2. <span data-ttu-id="36225-180">Click the **Log Search** tile and on the Log Search pane, in the query field type `Perf` and then hit enter or click the search button to the right of the query field.</span><span class="sxs-lookup"><span data-stu-id="36225-180">Click the **Log Search** tile and on the Log Search pane, in the query field type `Perf` and then hit enter or click the search button to the right of the query field.</span></span>

    ![Log Analytics log search query example](./media/log-analytics-quick-collect-azurevm/log-analytics-portal-perf-query.png) 

<span data-ttu-id="36225-182">For example, the query in the following image returned 735 performance records.</span><span class="sxs-lookup"><span data-stu-id="36225-182">For example, the query in the following image returned 735 performance records.</span></span>  <span data-ttu-id="36225-183">Your results will be significantly less.</span><span class="sxs-lookup"><span data-stu-id="36225-183">Your results will be significantly less.</span></span> 

![Log Analytics log search result](media/log-analytics-quick-collect-azurevm/log-analytics-search-perf.png)

## <a name="clean-up-resources"></a><span data-ttu-id="36225-185">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="36225-185">Clean up resources</span></span>
<span data-ttu-id="36225-186">When no longer needed, delete the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="36225-186">When no longer needed, delete the Log Analytics workspace.</span></span> <span data-ttu-id="36225-187">To do so, select the Log Analytics workspace you created earlier and on the resource page click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="36225-187">To do so, select the Log Analytics workspace you created earlier and on the resource page click **Delete**.</span></span>


![Delete Log Analytics resource](media/log-analytics-quick-collect-azurevm/log-analytics-portal-delete-resource.png)

## <a name="next-steps"></a><span data-ttu-id="36225-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="36225-189">Next steps</span></span>
<span data-ttu-id="36225-190">Now that you are collecting operational and performance data from your Windows or Linux virtual machines, you can easily begin exploring, analyzing, and taking action on data that you collect for *free*.</span><span class="sxs-lookup"><span data-stu-id="36225-190">Now that you are collecting operational and performance data from your Windows or Linux virtual machines, you can easily begin exploring, analyzing, and taking action on data that you collect for *free*.</span></span>  

<span data-ttu-id="36225-191">To learn how to view and analyze the data, continue to the tutorial.</span><span class="sxs-lookup"><span data-stu-id="36225-191">To learn how to view and analyze the data, continue to the tutorial.</span></span>   

> [!div class="nextstepaction"]
> [<span data-ttu-id="36225-192">View or analyze data in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="36225-192">View or analyze data in Log Analytics</span></span>](log-analytics-tutorial-viewdata.md)
