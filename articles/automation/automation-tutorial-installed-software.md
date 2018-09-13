---
title: Discover what software is installed on your machines with Azure Automation | Microsoft Docs
description: Use Inventory to discover what software is installed on the machines across your environment.
services: automation
keywords: inventory, automation, change, tracking
author: jennyhunter-msft
ms.author: jehunte
ms.date: 04/11/2018
ms.topic: tutorial
ms.service: automation
ms.component: change-inventory-management
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: cb876a8d8019f5a2a7232c3093c6f64a7b2730e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868953"
---
# <a name="discover-what-software-is-installed-on-your-azure-and-non-azure-machines"></a><span data-ttu-id="019ec-104">Discover what software is installed on your Azure and non-Azure machines</span><span class="sxs-lookup"><span data-stu-id="019ec-104">Discover what software is installed on your Azure and non-Azure machines</span></span>

<span data-ttu-id="019ec-105">In this tutorial, you learn how to discover what software is installed in your environment.</span><span class="sxs-lookup"><span data-stu-id="019ec-105">In this tutorial, you learn how to discover what software is installed in your environment.</span></span> <span data-ttu-id="019ec-106">You can collect and view inventory for software, files, Linux daemons, Windows Services, and Windows Registry keys on your computers.</span><span class="sxs-lookup"><span data-stu-id="019ec-106">You can collect and view inventory for software, files, Linux daemons, Windows Services, and Windows Registry keys on your computers.</span></span> <span data-ttu-id="019ec-107">Tracking the configurations of your machines can help you pinpoint operational issues across your environment and better understand the state of your machines.</span><span class="sxs-lookup"><span data-stu-id="019ec-107">Tracking the configurations of your machines can help you pinpoint operational issues across your environment and better understand the state of your machines.</span></span>

<span data-ttu-id="019ec-108">In this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="019ec-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="019ec-109">Enable the solution</span><span class="sxs-lookup"><span data-stu-id="019ec-109">Enable the solution</span></span>
> * <span data-ttu-id="019ec-110">Onboard an Azure VM</span><span class="sxs-lookup"><span data-stu-id="019ec-110">Onboard an Azure VM</span></span>
> * <span data-ttu-id="019ec-111">Onboard a non-Azure VM</span><span class="sxs-lookup"><span data-stu-id="019ec-111">Onboard a non-Azure VM</span></span>
> * <span data-ttu-id="019ec-112">View installed software</span><span class="sxs-lookup"><span data-stu-id="019ec-112">View installed software</span></span>
> * <span data-ttu-id="019ec-113">Search inventory logs for installed software</span><span class="sxs-lookup"><span data-stu-id="019ec-113">Search inventory logs for installed software</span></span>

## <a name="prerequisites"></a><span data-ttu-id="019ec-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="019ec-114">Prerequisites</span></span>

<span data-ttu-id="019ec-115">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="019ec-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="019ec-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="019ec-116">An Azure subscription.</span></span> <span data-ttu-id="019ec-117">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="019ec-117">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="019ec-118">An [Automation Account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span><span class="sxs-lookup"><span data-stu-id="019ec-118">An [Automation Account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span></span>
* <span data-ttu-id="019ec-119">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span><span class="sxs-lookup"><span data-stu-id="019ec-119">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="019ec-120">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="019ec-120">Log in to Azure</span></span>

<span data-ttu-id="019ec-121">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="019ec-121">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="enable-change-tracking-and-inventory"></a><span data-ttu-id="019ec-122">Enable Change tracking and Inventory</span><span class="sxs-lookup"><span data-stu-id="019ec-122">Enable Change tracking and Inventory</span></span>

<span data-ttu-id="019ec-123">First you need to enable Change tracking and Inventory for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="019ec-123">First you need to enable Change tracking and Inventory for this tutorial.</span></span> <span data-ttu-id="019ec-124">If you've previously enabled the **Change Tracking** solution, this step is not necessary.</span><span class="sxs-lookup"><span data-stu-id="019ec-124">If you've previously enabled the **Change Tracking** solution, this step is not necessary.</span></span>

<span data-ttu-id="019ec-125">Navigate to your Automation Account and select **Inventory** under **CONFIGURATION MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="019ec-125">Navigate to your Automation Account and select **Inventory** under **CONFIGURATION MANAGEMENT**.</span></span>

<span data-ttu-id="019ec-126">Choose the Log Analytics workspace and Automation Account and click **Enable** to enable the solution.</span><span class="sxs-lookup"><span data-stu-id="019ec-126">Choose the Log Analytics workspace and Automation Account and click **Enable** to enable the solution.</span></span> <span data-ttu-id="019ec-127">The solution takes up to 15 minutes to enable.</span><span class="sxs-lookup"><span data-stu-id="019ec-127">The solution takes up to 15 minutes to enable.</span></span>

![Inventory onboard configuration banner](./media/automation-tutorial-installed-software/enableinventory.png)

<span data-ttu-id="019ec-129">To enable the solution, configure the location, Log analytics workspace, and Automation Account to use and click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="019ec-129">To enable the solution, configure the location, Log analytics workspace, and Automation Account to use and click **Enable**.</span></span> <span data-ttu-id="019ec-130">If the fields are grayed out, that means another automation solution is enabled for the VM and the same workspace and Automation Account must be used.</span><span class="sxs-lookup"><span data-stu-id="019ec-130">If the fields are grayed out, that means another automation solution is enabled for the VM and the same workspace and Automation Account must be used.</span></span>

<span data-ttu-id="019ec-131">A [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace is used to collect data that is generated by features and services such as Inventory.</span><span class="sxs-lookup"><span data-stu-id="019ec-131">A [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace is used to collect data that is generated by features and services such as Inventory.</span></span>
<span data-ttu-id="019ec-132">The workspace provides a single location to review and analyze data from multiple sources.</span><span class="sxs-lookup"><span data-stu-id="019ec-132">The workspace provides a single location to review and analyze data from multiple sources.</span></span>

<span data-ttu-id="019ec-133">Enabling the solution can take up to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="019ec-133">Enabling the solution can take up to 15 minutes.</span></span> <span data-ttu-id="019ec-134">During this time, you shouldn't close the browser window.</span><span class="sxs-lookup"><span data-stu-id="019ec-134">During this time, you shouldn't close the browser window.</span></span>
<span data-ttu-id="019ec-135">After the solution is enabled, information about installed software and changes on the VM flows to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="019ec-135">After the solution is enabled, information about installed software and changes on the VM flows to Log Analytics.</span></span>
<span data-ttu-id="019ec-136">It can take between 30 minutes and 6 hours for the data to be available for analysis.</span><span class="sxs-lookup"><span data-stu-id="019ec-136">It can take between 30 minutes and 6 hours for the data to be available for analysis.</span></span>

## <a name="onboard-a-vm"></a><span data-ttu-id="019ec-137">Onboard a VM</span><span class="sxs-lookup"><span data-stu-id="019ec-137">Onboard a VM</span></span>

<span data-ttu-id="019ec-138">In your Automation Account, navigate to **Inventory** under **CONFIGURATION MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="019ec-138">In your Automation Account, navigate to **Inventory** under **CONFIGURATION MANAGEMENT**.</span></span>

<span data-ttu-id="019ec-139">Select **+ Add Azure VM**, this opens up the **Virtual machines** page and allows you to select an existing VM from the list.</span><span class="sxs-lookup"><span data-stu-id="019ec-139">Select **+ Add Azure VM**, this opens up the **Virtual machines** page and allows you to select an existing VM from the list.</span></span> <span data-ttu-id="019ec-140">Select the VM you want to onboard.</span><span class="sxs-lookup"><span data-stu-id="019ec-140">Select the VM you want to onboard.</span></span> <span data-ttu-id="019ec-141">On the page that opens click **Enable** to enable the solution on the VM.</span><span class="sxs-lookup"><span data-stu-id="019ec-141">On the page that opens click **Enable** to enable the solution on the VM.</span></span> <span data-ttu-id="019ec-142">The Microsoft Management Agent is deployed to the VM and configures the agent to talk to the Log Analytics workspace you configured when enabling the solution.</span><span class="sxs-lookup"><span data-stu-id="019ec-142">The Microsoft Management Agent is deployed to the VM and configures the agent to talk to the Log Analytics workspace you configured when enabling the solution.</span></span> <span data-ttu-id="019ec-143">This can take a few minutes to complete the onboarding.</span><span class="sxs-lookup"><span data-stu-id="019ec-143">This can take a few minutes to complete the onboarding.</span></span> <span data-ttu-id="019ec-144">At this point, you can select a new VM from the list and onboard another VM.</span><span class="sxs-lookup"><span data-stu-id="019ec-144">At this point, you can select a new VM from the list and onboard another VM.</span></span>

## <a name="onboard-a-non-azure-machine"></a><span data-ttu-id="019ec-145">Onboard a non-Azure machine</span><span class="sxs-lookup"><span data-stu-id="019ec-145">Onboard a non-Azure machine</span></span>

<span data-ttu-id="019ec-146">To add non-Azure machines, install the agent for [Windows](../log-analytics/log-analytics-agent-windows.md) or [Linux](automation-linux-hrw-install.md) depending on your operating system.</span><span class="sxs-lookup"><span data-stu-id="019ec-146">To add non-Azure machines, install the agent for [Windows](../log-analytics/log-analytics-agent-windows.md) or [Linux](automation-linux-hrw-install.md) depending on your operating system.</span></span> <span data-ttu-id="019ec-147">Once the agent is installed, navigate to your Automation Account and go to **Inventory** under **CONFIGURATION MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="019ec-147">Once the agent is installed, navigate to your Automation Account and go to **Inventory** under **CONFIGURATION MANAGEMENT**.</span></span> <span data-ttu-id="019ec-148">When you click **Manage Machines**, you see a list of the machines reporting to your Log Analytics workspace that do not have the solution enabled.</span><span class="sxs-lookup"><span data-stu-id="019ec-148">When you click **Manage Machines**, you see a list of the machines reporting to your Log Analytics workspace that do not have the solution enabled.</span></span> <span data-ttu-id="019ec-149">Select the appropriate option for your environment.</span><span class="sxs-lookup"><span data-stu-id="019ec-149">Select the appropriate option for your environment.</span></span>

* <span data-ttu-id="019ec-150">**Enable on all available machines** - This option enables the solution on all the machines reporting to your Log Analytics workspace at this time.</span><span class="sxs-lookup"><span data-stu-id="019ec-150">**Enable on all available machines** - This option enables the solution on all the machines reporting to your Log Analytics workspace at this time.</span></span>
* <span data-ttu-id="019ec-151">**Enable on all available machines and future machines** - This option enables the solution on all machines reporting to your Log Analytics workspace and subsequently on all future machines added to the workspace.</span><span class="sxs-lookup"><span data-stu-id="019ec-151">**Enable on all available machines and future machines** - This option enables the solution on all machines reporting to your Log Analytics workspace and subsequently on all future machines added to the workspace.</span></span>
* <span data-ttu-id="019ec-152">**Enable on selected machines** - This option enables the solution only on the machines that you have selected.</span><span class="sxs-lookup"><span data-stu-id="019ec-152">**Enable on selected machines** - This option enables the solution only on the machines that you have selected.</span></span>

![Manage Machines](./media/automation-tutorial-installed-software/manage-machines.png)

## <a name="view-installed-software"></a><span data-ttu-id="019ec-154">View installed software</span><span class="sxs-lookup"><span data-stu-id="019ec-154">View installed software</span></span>

<span data-ttu-id="019ec-155">Once the Change tracking and Inventory solution is enabled, you can view the results on the **Inventory** page.</span><span class="sxs-lookup"><span data-stu-id="019ec-155">Once the Change tracking and Inventory solution is enabled, you can view the results on the **Inventory** page.</span></span>

<span data-ttu-id="019ec-156">From within your Automation Account, select **Inventory** under **CONFIGURATION MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="019ec-156">From within your Automation Account, select **Inventory** under **CONFIGURATION MANAGEMENT**.</span></span>

<span data-ttu-id="019ec-157">On the **Inventory** page, click on the **Software** tab.</span><span class="sxs-lookup"><span data-stu-id="019ec-157">On the **Inventory** page, click on the **Software** tab.</span></span>

<span data-ttu-id="019ec-158">On the **Software** tab, there is a table that lists the software that has been found.</span><span class="sxs-lookup"><span data-stu-id="019ec-158">On the **Software** tab, there is a table that lists the software that has been found.</span></span> <span data-ttu-id="019ec-159">The software is grouped by software name and version.</span><span class="sxs-lookup"><span data-stu-id="019ec-159">The software is grouped by software name and version.</span></span>

<span data-ttu-id="019ec-160">The high-level details for each software record are viewable in the table.</span><span class="sxs-lookup"><span data-stu-id="019ec-160">The high-level details for each software record are viewable in the table.</span></span> <span data-ttu-id="019ec-161">These details include the software name, version, publisher, last refreshed time (the most recent refresh time reported by a machine in the group), and machines (the count of machines with that software).</span><span class="sxs-lookup"><span data-stu-id="019ec-161">These details include the software name, version, publisher, last refreshed time (the most recent refresh time reported by a machine in the group), and machines (the count of machines with that software).</span></span>

![Software inventory](./media/automation-tutorial-installed-software/inventory-software.png)

<span data-ttu-id="019ec-163">Click on a row to view the properties of the software record and the names of the machines with that software.</span><span class="sxs-lookup"><span data-stu-id="019ec-163">Click on a row to view the properties of the software record and the names of the machines with that software.</span></span>

<span data-ttu-id="019ec-164">To look for a specific software or group of software, you can search in the text box directly above the software list.</span><span class="sxs-lookup"><span data-stu-id="019ec-164">To look for a specific software or group of software, you can search in the text box directly above the software list.</span></span>
<span data-ttu-id="019ec-165">The filter allows you to search based off the software name, version, or publisher.</span><span class="sxs-lookup"><span data-stu-id="019ec-165">The filter allows you to search based off the software name, version, or publisher.</span></span>

<span data-ttu-id="019ec-166">For instance, searching for "Contoso" returns all software with a name, publisher, or version containing "Contoso".</span><span class="sxs-lookup"><span data-stu-id="019ec-166">For instance, searching for "Contoso" returns all software with a name, publisher, or version containing "Contoso".</span></span>

## <a name="search-inventory-logs-for-installed-software"></a><span data-ttu-id="019ec-167">Search inventory logs for installed software</span><span class="sxs-lookup"><span data-stu-id="019ec-167">Search inventory logs for installed software</span></span>

<span data-ttu-id="019ec-168">Inventory generates log data that is sent to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="019ec-168">Inventory generates log data that is sent to Log Analytics.</span></span> <span data-ttu-id="019ec-169">To search the logs by running queries, select **Log Analytics** at the top of the **Inventory** window.</span><span class="sxs-lookup"><span data-stu-id="019ec-169">To search the logs by running queries, select **Log Analytics** at the top of the **Inventory** window.</span></span>

<span data-ttu-id="019ec-170">Inventory data is stored under the type **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="019ec-170">Inventory data is stored under the type **ConfigurationData**.</span></span>
<span data-ttu-id="019ec-171">The following sample Log Analytics query returns the inventory results where the Publisher equals "Microsoft Corporation".</span><span class="sxs-lookup"><span data-stu-id="019ec-171">The following sample Log Analytics query returns the inventory results where the Publisher equals "Microsoft Corporation".</span></span>

```loganalytics
ConfigurationData
| where ConfigDataType == "Software"
| where Publisher == "Microsoft Corporation"
| summarize arg_max(TimeGenerated, *) by SoftwareName, Computer
```

<span data-ttu-id="019ec-172">To learn more about running and searching log files in Log Analytics, see [Azure Log Analytics](https://docs.loganalytics.io/index).</span><span class="sxs-lookup"><span data-stu-id="019ec-172">To learn more about running and searching log files in Log Analytics, see [Azure Log Analytics](https://docs.loganalytics.io/index).</span></span>

### <a name="single-machine-inventory"></a><span data-ttu-id="019ec-173">Single machine inventory</span><span class="sxs-lookup"><span data-stu-id="019ec-173">Single machine inventory</span></span>

<span data-ttu-id="019ec-174">To see the software inventory for a single machine, you can access Inventory from the Azure VM resource page or use Log Analytics to filter down to the corresponding machine.</span><span class="sxs-lookup"><span data-stu-id="019ec-174">To see the software inventory for a single machine, you can access Inventory from the Azure VM resource page or use Log Analytics to filter down to the corresponding machine.</span></span>
<span data-ttu-id="019ec-175">The following example Log Analytics query returns the list of software for a machine named ContosoVM.</span><span class="sxs-lookup"><span data-stu-id="019ec-175">The following example Log Analytics query returns the list of software for a machine named ContosoVM.</span></span>

```loganalytics
ConfigurationData
| where ConfigDataType == "Software"
| summarize arg_max(TimeGenerated, *) by SoftwareName, CurrentVersion
| where Computer =="ContosoVM"
| render table
| summarize by Publisher, SoftwareName
```

## <a name="next-steps"></a><span data-ttu-id="019ec-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="019ec-176">Next steps</span></span>

<span data-ttu-id="019ec-177">In this tutorial you learned how view software inventory such as how to:</span><span class="sxs-lookup"><span data-stu-id="019ec-177">In this tutorial you learned how view software inventory such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="019ec-178">Enable the solution</span><span class="sxs-lookup"><span data-stu-id="019ec-178">Enable the solution</span></span>
> * <span data-ttu-id="019ec-179">Onboard an Azure VM</span><span class="sxs-lookup"><span data-stu-id="019ec-179">Onboard an Azure VM</span></span>
> * <span data-ttu-id="019ec-180">Onboard a non-Azure VM</span><span class="sxs-lookup"><span data-stu-id="019ec-180">Onboard a non-Azure VM</span></span>
> * <span data-ttu-id="019ec-181">View installed software</span><span class="sxs-lookup"><span data-stu-id="019ec-181">View installed software</span></span>
> * <span data-ttu-id="019ec-182">Search inventory logs for installed software</span><span class="sxs-lookup"><span data-stu-id="019ec-182">Search inventory logs for installed software</span></span>

<span data-ttu-id="019ec-183">Continue to the overview for the Change tracking and Inventory solution to learn more about it.</span><span class="sxs-lookup"><span data-stu-id="019ec-183">Continue to the overview for the Change tracking and Inventory solution to learn more about it.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="019ec-184">Change management and Inventory solution</span><span class="sxs-lookup"><span data-stu-id="019ec-184">Change management and Inventory solution</span></span>](automation-change-tracking.md)