---
title: IT Service Management Connector in Azure Log Analytics | Microsoft Docs
description: This article provides an overview of IT Service Management Connector (ITSMC) and information about how to use this solution to centrally monitor and manage the ITSM work items in Azure Log Analytics, and resolve any issues quickly.
services: log-analytics
documentationcenter: ''
author: jyothirmaisuri
manager: riyazp
editor: ''
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/24/2018
ms.author: v-jysur
ms.component: na
ms.openlocfilehash: da37e7558f93bc5073cd4ee1726a409c7defe127
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966676"
---
# <a name="connect-azure-to-itsm-tools-using-it-service-management-connector"></a><span data-ttu-id="1f771-103">Connect Azure to ITSM tools using IT Service Management Connector</span><span class="sxs-lookup"><span data-stu-id="1f771-103">Connect Azure to ITSM tools using IT Service Management Connector</span></span>

![IT Service Management Connector symbol](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="1f771-105">The IT Service Management Connector (ITSMC) allows you to connect Azure and a supported IT Service Management (ITSM) product/service.</span><span class="sxs-lookup"><span data-stu-id="1f771-105">The IT Service Management Connector (ITSMC) allows you to connect Azure and a supported IT Service Management (ITSM) product/service.</span></span>

<span data-ttu-id="1f771-106">Azure services like Log Analytics and Azure Monitor provide tools to detect, analyze and troubleshoot issues with your Azure and non-Azure resources.</span><span class="sxs-lookup"><span data-stu-id="1f771-106">Azure services like Log Analytics and Azure Monitor provide tools to detect, analyze and troubleshoot issues with your Azure and non-Azure resources.</span></span> <span data-ttu-id="1f771-107">However, the work items related to an issue  typically reside in an ITSM product/service.</span><span class="sxs-lookup"><span data-stu-id="1f771-107">However, the work items related to an issue  typically reside in an ITSM product/service.</span></span> <span data-ttu-id="1f771-108">The ITSM connector provides a bi-directional connection between Azure and ITSM tools to help you resolve issues faster.</span><span class="sxs-lookup"><span data-stu-id="1f771-108">The ITSM connector provides a bi-directional connection between Azure and ITSM tools to help you resolve issues faster.</span></span>

<span data-ttu-id="1f771-109">ITSMC supports connections with the following ITSM tools:</span><span class="sxs-lookup"><span data-stu-id="1f771-109">ITSMC supports connections with the following ITSM tools:</span></span>

-   <span data-ttu-id="1f771-110">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="1f771-110">ServiceNow</span></span>
-   <span data-ttu-id="1f771-111">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="1f771-111">System Center Service Manager</span></span>
-   <span data-ttu-id="1f771-112">Provance</span><span class="sxs-lookup"><span data-stu-id="1f771-112">Provance</span></span>
-   <span data-ttu-id="1f771-113">Cherwell</span><span class="sxs-lookup"><span data-stu-id="1f771-113">Cherwell</span></span>

<span data-ttu-id="1f771-114">With ITSMC, you can</span><span class="sxs-lookup"><span data-stu-id="1f771-114">With ITSMC, you can</span></span>

-  <span data-ttu-id="1f771-115">Create work items in ITSM tool, based on your Azure alerts (metric alerts, Activity Log alerts and Log Analytics alerts).</span><span class="sxs-lookup"><span data-stu-id="1f771-115">Create work items in ITSM tool, based on your Azure alerts (metric alerts, Activity Log alerts and Log Analytics alerts).</span></span>
-  <span data-ttu-id="1f771-116">Optionally, you can sync your incident and change request data from your ITSM tool to an Azure Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="1f771-116">Optionally, you can sync your incident and change request data from your ITSM tool to an Azure Log Analytics workspace.</span></span>


<span data-ttu-id="1f771-117">You can start using the ITSM Connector using the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f771-117">You can start using the ITSM Connector using the following steps:</span></span>

1.  [<span data-ttu-id="1f771-118">Add the ITSM Connector Solution</span><span class="sxs-lookup"><span data-stu-id="1f771-118">Add the ITSM Connector Solution</span></span>](#adding-the-it-service-management-connector-solution)
2.  [<span data-ttu-id="1f771-119">Create an ITSM connection</span><span class="sxs-lookup"><span data-stu-id="1f771-119">Create an ITSM connection</span></span>](#creating-an-itsm-connection)
3.  [<span data-ttu-id="1f771-120">Use the connection</span><span class="sxs-lookup"><span data-stu-id="1f771-120">Use the connection</span></span>](#using-the-solution)


##  <a name="adding-the-it-service-management-connector-solution"></a><span data-ttu-id="1f771-121">Adding the IT Service Management Connector Solution</span><span class="sxs-lookup"><span data-stu-id="1f771-121">Adding the IT Service Management Connector Solution</span></span>

<span data-ttu-id="1f771-122">Before you can create a connection, you need to add the ITSM Connector Solution.</span><span class="sxs-lookup"><span data-stu-id="1f771-122">Before you can create a connection, you need to add the ITSM Connector Solution.</span></span>

1.  <span data-ttu-id="1f771-123">In Azure portal, click **+ New** icon.</span><span class="sxs-lookup"><span data-stu-id="1f771-123">In Azure portal, click **+ New** icon.</span></span>

    ![Azure new resource](./media/log-analytics-itsmc/azure-add-new-resource.png)

2.  <span data-ttu-id="1f771-125">Search for **IT Service Management Connector** in the Marketplace and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f771-125">Search for **IT Service Management Connector** in the Marketplace and click **Create**.</span></span>

    ![Add ITSMC solution](./media/log-analytics-itsmc/add-itsmc-solution.png)

3.  <span data-ttu-id="1f771-127">In the **OMS Workspace** section, select the Azure Log Analytics workspace where you want to install the solution.</span><span class="sxs-lookup"><span data-stu-id="1f771-127">In the **OMS Workspace** section, select the Azure Log Analytics workspace where you want to install the solution.</span></span>
4.  <span data-ttu-id="1f771-128">In the **OMS Workspace Settings** section, select the ResourceGroup where you want to create the solution resource.</span><span class="sxs-lookup"><span data-stu-id="1f771-128">In the **OMS Workspace Settings** section, select the ResourceGroup where you want to create the solution resource.</span></span>

    ![ITSMC workspace](./media/log-analytics-itsmc/itsmc-solution-workspace.png)

5.  <span data-ttu-id="1f771-130">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f771-130">Click **Create**.</span></span>

<span data-ttu-id="1f771-131">When the solution resource is deployed, a notification appears at the top right of the window.</span><span class="sxs-lookup"><span data-stu-id="1f771-131">When the solution resource is deployed, a notification appears at the top right of the window.</span></span>


## <a name="creating-an-itsm--connection"></a><span data-ttu-id="1f771-132">Creating an ITSM  connection</span><span class="sxs-lookup"><span data-stu-id="1f771-132">Creating an ITSM  connection</span></span>

<span data-ttu-id="1f771-133">Once you have installed the solution, you can create a connection.</span><span class="sxs-lookup"><span data-stu-id="1f771-133">Once you have installed the solution, you can create a connection.</span></span>

<span data-ttu-id="1f771-134">For creating a connection, you will need to prep your ITSM tool to allow the connection from the ITSM Connector solution.</span><span class="sxs-lookup"><span data-stu-id="1f771-134">For creating a connection, you will need to prep your ITSM tool to allow the connection from the ITSM Connector solution.</span></span>  

<span data-ttu-id="1f771-135">Depending on the ITSM product you are connecting to, use the following steps :</span><span class="sxs-lookup"><span data-stu-id="1f771-135">Depending on the ITSM product you are connecting to, use the following steps :</span></span>

- [<span data-ttu-id="1f771-136">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="1f771-136">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="1f771-137">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="1f771-137">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="1f771-138">Provance</span><span class="sxs-lookup"><span data-stu-id="1f771-138">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-azure)  
- [<span data-ttu-id="1f771-139">Cherwell</span><span class="sxs-lookup"><span data-stu-id="1f771-139">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-azure)

<span data-ttu-id="1f771-140">Once you have prepped your ITSM tools, follow the steps below to create a connection:</span><span class="sxs-lookup"><span data-stu-id="1f771-140">Once you have prepped your ITSM tools, follow the steps below to create a connection:</span></span>

1.  <span data-ttu-id="1f771-141">Go to **All Resources**, look for **ServiceDesk(YourWorkspaceName)**.</span><span class="sxs-lookup"><span data-stu-id="1f771-141">Go to **All Resources**, look for **ServiceDesk(YourWorkspaceName)**.</span></span>
2.  <span data-ttu-id="1f771-142">Under **WORKSPACE DATA SOURCES** in the left pane, click **ITSM Connections**.</span><span class="sxs-lookup"><span data-stu-id="1f771-142">Under **WORKSPACE DATA SOURCES** in the left pane, click **ITSM Connections**.</span></span>
    <span data-ttu-id="1f771-143">![ITSM connections](./media/log-analytics-itsmc/itsm-connections.png)</span><span class="sxs-lookup"><span data-stu-id="1f771-143">![ITSM connections](./media/log-analytics-itsmc/itsm-connections.png)</span></span>

    <span data-ttu-id="1f771-144">This page displays the list of connections.</span><span class="sxs-lookup"><span data-stu-id="1f771-144">This page displays the list of connections.</span></span>
3.  <span data-ttu-id="1f771-145">Click **Add Connection**.</span><span class="sxs-lookup"><span data-stu-id="1f771-145">Click **Add Connection**.</span></span>

    ![Add ITSM connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)

4.  <span data-ttu-id="1f771-147">Specify the connection settings as described in [Configuring the ITSMC connection with your ITSM products/services article](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="1f771-147">Specify the connection settings as described in [Configuring the ITSMC connection with your ITSM products/services article](log-analytics-itsmc-connections.md).</span></span>

    > [!NOTE]

    > <span data-ttu-id="1f771-148">By default, ITSMC refreshes the connection's configuration data once in every 24 hours.</span><span class="sxs-lookup"><span data-stu-id="1f771-148">By default, ITSMC refreshes the connection's configuration data once in every 24 hours.</span></span> <span data-ttu-id="1f771-149">To refresh your connection's data instantly for any edits or template updates that you make, click the **Sync** button on your connection's blade.</span><span class="sxs-lookup"><span data-stu-id="1f771-149">To refresh your connection's data instantly for any edits or template updates that you make, click the **Sync** button on your connection's blade.</span></span>

    ![Connection refresh](./media/log-analytics-itsmc/itsmc-connections-refresh.png)


## <a name="using-the-solution"></a><span data-ttu-id="1f771-151">Using the solution</span><span class="sxs-lookup"><span data-stu-id="1f771-151">Using the solution</span></span>
   <span data-ttu-id="1f771-152">By using the ITSM Connector solution, you can create work items from Azure alerts, Log Analytics alerts  and  Log Analytics log records.</span><span class="sxs-lookup"><span data-stu-id="1f771-152">By using the ITSM Connector solution, you can create work items from Azure alerts, Log Analytics alerts  and  Log Analytics log records.</span></span>

## <a name="create-itsm-work-items-from-azure-alerts"></a><span data-ttu-id="1f771-153">Create ITSM work items from Azure alerts</span><span class="sxs-lookup"><span data-stu-id="1f771-153">Create ITSM work items from Azure alerts</span></span>

<span data-ttu-id="1f771-154">Once you have your ITSM connection created, you can create work item(s) in your ITSM tool based on Azure alerts, by using the **ITSM Action** in **Action Groups**.</span><span class="sxs-lookup"><span data-stu-id="1f771-154">Once you have your ITSM connection created, you can create work item(s) in your ITSM tool based on Azure alerts, by using the **ITSM Action** in **Action Groups**.</span></span>

<span data-ttu-id="1f771-155">Action Groups provide a modular and reusable way of triggering actions for your Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="1f771-155">Action Groups provide a modular and reusable way of triggering actions for your Azure Alerts.</span></span> <span data-ttu-id="1f771-156">You can use Action Groups with metric alerts, Activity Log alerts and Azure Log Analytics alerts in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f771-156">You can use Action Groups with metric alerts, Activity Log alerts and Azure Log Analytics alerts in Azure portal.</span></span>

<span data-ttu-id="1f771-157">Use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="1f771-157">Use the following procedure:</span></span>

1. <span data-ttu-id="1f771-158">In Azure portal, click  **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="1f771-158">In Azure portal, click  **Monitor**.</span></span>
2. <span data-ttu-id="1f771-159">In the left pane, click  **Action groups**.</span><span class="sxs-lookup"><span data-stu-id="1f771-159">In the left pane, click  **Action groups**.</span></span> <span data-ttu-id="1f771-160">The **Add action group** window appears.</span><span class="sxs-lookup"><span data-stu-id="1f771-160">The **Add action group** window appears.</span></span>

    ![Action Groups](media/log-analytics-itsmc/action-groups.png)

3. <span data-ttu-id="1f771-162">Provide **Name** and **ShortName** for your action group.</span><span class="sxs-lookup"><span data-stu-id="1f771-162">Provide **Name** and **ShortName** for your action group.</span></span> <span data-ttu-id="1f771-163">Select the **Resource Group** and **Subscription** where you want to create your action group.</span><span class="sxs-lookup"><span data-stu-id="1f771-163">Select the **Resource Group** and **Subscription** where you want to create your action group.</span></span>

    ![Action Groups detail](media/log-analytics-itsmc/action-groups-details.png)

4. <span data-ttu-id="1f771-165">In the Actions list, select **ITSM** from the drop-down menu for **Action Type**.</span><span class="sxs-lookup"><span data-stu-id="1f771-165">In the Actions list, select **ITSM** from the drop-down menu for **Action Type**.</span></span> <span data-ttu-id="1f771-166">Provide a **Name** for the action and click **Edit details**.</span><span class="sxs-lookup"><span data-stu-id="1f771-166">Provide a **Name** for the action and click **Edit details**.</span></span>
5. <span data-ttu-id="1f771-167">Select the **Subscription** where your Log Analytics workspace is located.</span><span class="sxs-lookup"><span data-stu-id="1f771-167">Select the **Subscription** where your Log Analytics workspace is located.</span></span> <span data-ttu-id="1f771-168">Select the **Connection** name (your ITSM Connector name) followed by your Workspace name.</span><span class="sxs-lookup"><span data-stu-id="1f771-168">Select the **Connection** name (your ITSM Connector name) followed by your Workspace name.</span></span> <span data-ttu-id="1f771-169">For example, "MyITSMMConnector(MyWorkspace)."</span><span class="sxs-lookup"><span data-stu-id="1f771-169">For example, "MyITSMMConnector(MyWorkspace)."</span></span>

    ![ITSM Action details](./media/log-analytics-itsmc/itsm-action-details.png)

6. <span data-ttu-id="1f771-171">Select **Work Item** type from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="1f771-171">Select **Work Item** type from the drop-down menu.</span></span>
   <span data-ttu-id="1f771-172">Choose to use an existing template or fill the fields required by your ITSM product.</span><span class="sxs-lookup"><span data-stu-id="1f771-172">Choose to use an existing template or fill the fields required by your ITSM product.</span></span>
7. <span data-ttu-id="1f771-173">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f771-173">Click **OK**.</span></span>

<span data-ttu-id="1f771-174">When creating/editing an Azure alert rule, use an Action group, which has an ITSM Action.</span><span class="sxs-lookup"><span data-stu-id="1f771-174">When creating/editing an Azure alert rule, use an Action group, which has an ITSM Action.</span></span> <span data-ttu-id="1f771-175">When the alert triggers, work item is created/updated in the ITSM tool.</span><span class="sxs-lookup"><span data-stu-id="1f771-175">When the alert triggers, work item is created/updated in the ITSM tool.</span></span>

>[!NOTE]

> <span data-ttu-id="1f771-176">For information on pricing of ITSM Action, see the [pricing page](https://azure.microsoft.com/pricing/details/monitor/) for Action Groups.</span><span class="sxs-lookup"><span data-stu-id="1f771-176">For information on pricing of ITSM Action, see the [pricing page](https://azure.microsoft.com/pricing/details/monitor/) for Action Groups.</span></span>


## <a name="visualize-and-analyze-the-incident-and-change-request-data"></a><span data-ttu-id="1f771-177">Visualize and analyze the incident and change request data</span><span class="sxs-lookup"><span data-stu-id="1f771-177">Visualize and analyze the incident and change request data</span></span>

<span data-ttu-id="1f771-178">Based on your configuration when setting up a connection, ITSM connector can sync up to 120 days of Incident and Change request data.</span><span class="sxs-lookup"><span data-stu-id="1f771-178">Based on your configuration when setting up a connection, ITSM connector can sync up to 120 days of Incident and Change request data.</span></span> <span data-ttu-id="1f771-179">The log record schema for this data is provided in the [next section](#additional-information).</span><span class="sxs-lookup"><span data-stu-id="1f771-179">The log record schema for this data is provided in the [next section](#additional-information).</span></span>

<span data-ttu-id="1f771-180">The incident and change request data can be visualized using the ITSM Connector dashboard in the solution.</span><span class="sxs-lookup"><span data-stu-id="1f771-180">The incident and change request data can be visualized using the ITSM Connector dashboard in the solution.</span></span>

![Log Analytics screen](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

<span data-ttu-id="1f771-182">The dashboard also provides information on connector status which can be used as a starting point to analyze any issues with the connections.</span><span class="sxs-lookup"><span data-stu-id="1f771-182">The dashboard also provides information on connector status which can be used as a starting point to analyze any issues with the connections.</span></span>

<span data-ttu-id="1f771-183">You can also visualize the incidents synced against the impacted computers, within the Service Map solution.</span><span class="sxs-lookup"><span data-stu-id="1f771-183">You can also visualize the incidents synced against the impacted computers, within the Service Map solution.</span></span>

<span data-ttu-id="1f771-184">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span><span class="sxs-lookup"><span data-stu-id="1f771-184">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="1f771-185">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span><span class="sxs-lookup"><span data-stu-id="1f771-185">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="1f771-186">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span><span class="sxs-lookup"><span data-stu-id="1f771-186">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="1f771-187">[Learn more](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="1f771-187">[Learn more](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="1f771-188">If you are using the Service Map solution, you can view the service desk items created in the ITSM solutions as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1f771-188">If you are using the Service Map solution, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![Log Analytics screen](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)

<span data-ttu-id="1f771-190">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md)</span><span class="sxs-lookup"><span data-stu-id="1f771-190">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md)</span></span>


## <a name="additional-information"></a><span data-ttu-id="1f771-191">Additional information</span><span class="sxs-lookup"><span data-stu-id="1f771-191">Additional information</span></span>

### <a name="data-synced-from-itsm-product"></a><span data-ttu-id="1f771-192">Data synced from ITSM product</span><span class="sxs-lookup"><span data-stu-id="1f771-192">Data synced from ITSM product</span></span>
<span data-ttu-id="1f771-193">Incidents and change requests are synced from your ITSM product to your Log Analytics workspace based on the connection's configuration.</span><span class="sxs-lookup"><span data-stu-id="1f771-193">Incidents and change requests are synced from your ITSM product to your Log Analytics workspace based on the connection's configuration.</span></span>

<span data-ttu-id="1f771-194">The following information shows examples of data gathered by ITSMC:</span><span class="sxs-lookup"><span data-stu-id="1f771-194">The following information shows examples of data gathered by ITSMC:</span></span>

> [!NOTE]

> <span data-ttu-id="1f771-195">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="1f771-195">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="1f771-196">**Work item:** **Incidents**</span><span class="sxs-lookup"><span data-stu-id="1f771-196">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="1f771-197">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="1f771-197">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="1f771-198">**Fields**</span><span class="sxs-lookup"><span data-stu-id="1f771-198">**Fields**</span></span>

- <span data-ttu-id="1f771-199">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="1f771-199">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="1f771-200">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="1f771-200">Service Desk ID</span></span>
- <span data-ttu-id="1f771-201">State</span><span class="sxs-lookup"><span data-stu-id="1f771-201">State</span></span>
- <span data-ttu-id="1f771-202">Urgency</span><span class="sxs-lookup"><span data-stu-id="1f771-202">Urgency</span></span>
- <span data-ttu-id="1f771-203">Impact</span><span class="sxs-lookup"><span data-stu-id="1f771-203">Impact</span></span>
- <span data-ttu-id="1f771-204">Priority</span><span class="sxs-lookup"><span data-stu-id="1f771-204">Priority</span></span>
- <span data-ttu-id="1f771-205">Escalation</span><span class="sxs-lookup"><span data-stu-id="1f771-205">Escalation</span></span>
- <span data-ttu-id="1f771-206">Created By</span><span class="sxs-lookup"><span data-stu-id="1f771-206">Created By</span></span>
- <span data-ttu-id="1f771-207">Resolved By</span><span class="sxs-lookup"><span data-stu-id="1f771-207">Resolved By</span></span>
- <span data-ttu-id="1f771-208">Closed By</span><span class="sxs-lookup"><span data-stu-id="1f771-208">Closed By</span></span>
- <span data-ttu-id="1f771-209">Source</span><span class="sxs-lookup"><span data-stu-id="1f771-209">Source</span></span>
- <span data-ttu-id="1f771-210">Assigned To</span><span class="sxs-lookup"><span data-stu-id="1f771-210">Assigned To</span></span>
- <span data-ttu-id="1f771-211">Category</span><span class="sxs-lookup"><span data-stu-id="1f771-211">Category</span></span>
- <span data-ttu-id="1f771-212">Title</span><span class="sxs-lookup"><span data-stu-id="1f771-212">Title</span></span>
- <span data-ttu-id="1f771-213">Description</span><span class="sxs-lookup"><span data-stu-id="1f771-213">Description</span></span>
- <span data-ttu-id="1f771-214">Created Date</span><span class="sxs-lookup"><span data-stu-id="1f771-214">Created Date</span></span>
- <span data-ttu-id="1f771-215">Closed Date</span><span class="sxs-lookup"><span data-stu-id="1f771-215">Closed Date</span></span>
- <span data-ttu-id="1f771-216">Resolved Date</span><span class="sxs-lookup"><span data-stu-id="1f771-216">Resolved Date</span></span>
- <span data-ttu-id="1f771-217">Last Modified Date</span><span class="sxs-lookup"><span data-stu-id="1f771-217">Last Modified Date</span></span>
- <span data-ttu-id="1f771-218">Computer</span><span class="sxs-lookup"><span data-stu-id="1f771-218">Computer</span></span>


<span data-ttu-id="1f771-219">**Work item:** **Change Requests**</span><span class="sxs-lookup"><span data-stu-id="1f771-219">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="1f771-220">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="1f771-220">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="1f771-221">**Fields**</span><span class="sxs-lookup"><span data-stu-id="1f771-221">**Fields**</span></span>
- <span data-ttu-id="1f771-222">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="1f771-222">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="1f771-223">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="1f771-223">Service Desk ID</span></span>
- <span data-ttu-id="1f771-224">Created By</span><span class="sxs-lookup"><span data-stu-id="1f771-224">Created By</span></span>
- <span data-ttu-id="1f771-225">Closed By</span><span class="sxs-lookup"><span data-stu-id="1f771-225">Closed By</span></span>
- <span data-ttu-id="1f771-226">Source</span><span class="sxs-lookup"><span data-stu-id="1f771-226">Source</span></span>
- <span data-ttu-id="1f771-227">Assigned To</span><span class="sxs-lookup"><span data-stu-id="1f771-227">Assigned To</span></span>
- <span data-ttu-id="1f771-228">Title</span><span class="sxs-lookup"><span data-stu-id="1f771-228">Title</span></span>
- <span data-ttu-id="1f771-229">Type</span><span class="sxs-lookup"><span data-stu-id="1f771-229">Type</span></span>
- <span data-ttu-id="1f771-230">Category</span><span class="sxs-lookup"><span data-stu-id="1f771-230">Category</span></span>
- <span data-ttu-id="1f771-231">State</span><span class="sxs-lookup"><span data-stu-id="1f771-231">State</span></span>
- <span data-ttu-id="1f771-232">Escalation</span><span class="sxs-lookup"><span data-stu-id="1f771-232">Escalation</span></span>
- <span data-ttu-id="1f771-233">Conflict Status</span><span class="sxs-lookup"><span data-stu-id="1f771-233">Conflict Status</span></span>
- <span data-ttu-id="1f771-234">Urgency</span><span class="sxs-lookup"><span data-stu-id="1f771-234">Urgency</span></span>
- <span data-ttu-id="1f771-235">Priority</span><span class="sxs-lookup"><span data-stu-id="1f771-235">Priority</span></span>
- <span data-ttu-id="1f771-236">Risk</span><span class="sxs-lookup"><span data-stu-id="1f771-236">Risk</span></span>
- <span data-ttu-id="1f771-237">Impact</span><span class="sxs-lookup"><span data-stu-id="1f771-237">Impact</span></span>
- <span data-ttu-id="1f771-238">Assigned To</span><span class="sxs-lookup"><span data-stu-id="1f771-238">Assigned To</span></span>
- <span data-ttu-id="1f771-239">Created Date</span><span class="sxs-lookup"><span data-stu-id="1f771-239">Created Date</span></span>
- <span data-ttu-id="1f771-240">Closed Date</span><span class="sxs-lookup"><span data-stu-id="1f771-240">Closed Date</span></span>
- <span data-ttu-id="1f771-241">Last Modified Date</span><span class="sxs-lookup"><span data-stu-id="1f771-241">Last Modified Date</span></span>
- <span data-ttu-id="1f771-242">Requested Date</span><span class="sxs-lookup"><span data-stu-id="1f771-242">Requested Date</span></span>
- <span data-ttu-id="1f771-243">Planned Start Date</span><span class="sxs-lookup"><span data-stu-id="1f771-243">Planned Start Date</span></span>
- <span data-ttu-id="1f771-244">Planned End Date</span><span class="sxs-lookup"><span data-stu-id="1f771-244">Planned End Date</span></span>
- <span data-ttu-id="1f771-245">Work Start Date</span><span class="sxs-lookup"><span data-stu-id="1f771-245">Work Start Date</span></span>
- <span data-ttu-id="1f771-246">Work End Date</span><span class="sxs-lookup"><span data-stu-id="1f771-246">Work End Date</span></span>
- <span data-ttu-id="1f771-247">Description</span><span class="sxs-lookup"><span data-stu-id="1f771-247">Description</span></span>
- <span data-ttu-id="1f771-248">Computer</span><span class="sxs-lookup"><span data-stu-id="1f771-248">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="1f771-249">Output data for a ServiceNow incident</span><span class="sxs-lookup"><span data-stu-id="1f771-249">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="1f771-250">Log Analytics field</span><span class="sxs-lookup"><span data-stu-id="1f771-250">Log Analytics field</span></span> | <span data-ttu-id="1f771-251">ServiceNow field</span><span class="sxs-lookup"><span data-stu-id="1f771-251">ServiceNow field</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f771-252">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="1f771-252">ServiceDeskId_s</span></span>| <span data-ttu-id="1f771-253">Number</span><span class="sxs-lookup"><span data-stu-id="1f771-253">Number</span></span> |
| <span data-ttu-id="1f771-254">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="1f771-254">IncidentState_s</span></span> | <span data-ttu-id="1f771-255">State</span><span class="sxs-lookup"><span data-stu-id="1f771-255">State</span></span> |
| <span data-ttu-id="1f771-256">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="1f771-256">Urgency_s</span></span> |<span data-ttu-id="1f771-257">Urgency</span><span class="sxs-lookup"><span data-stu-id="1f771-257">Urgency</span></span> |
| <span data-ttu-id="1f771-258">Impact_s</span><span class="sxs-lookup"><span data-stu-id="1f771-258">Impact_s</span></span> |<span data-ttu-id="1f771-259">Impact</span><span class="sxs-lookup"><span data-stu-id="1f771-259">Impact</span></span>|
| <span data-ttu-id="1f771-260">Priority_s</span><span class="sxs-lookup"><span data-stu-id="1f771-260">Priority_s</span></span> | <span data-ttu-id="1f771-261">Priority</span><span class="sxs-lookup"><span data-stu-id="1f771-261">Priority</span></span> |
| <span data-ttu-id="1f771-262">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="1f771-262">CreatedBy_s</span></span> | <span data-ttu-id="1f771-263">Opened by</span><span class="sxs-lookup"><span data-stu-id="1f771-263">Opened by</span></span> |
| <span data-ttu-id="1f771-264">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="1f771-264">ResolvedBy_s</span></span> | <span data-ttu-id="1f771-265">Resolved by</span><span class="sxs-lookup"><span data-stu-id="1f771-265">Resolved by</span></span>|
| <span data-ttu-id="1f771-266">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="1f771-266">ClosedBy_s</span></span>  | <span data-ttu-id="1f771-267">Closed by</span><span class="sxs-lookup"><span data-stu-id="1f771-267">Closed by</span></span> |
| <span data-ttu-id="1f771-268">Source_s</span><span class="sxs-lookup"><span data-stu-id="1f771-268">Source_s</span></span>| <span data-ttu-id="1f771-269">Contact type</span><span class="sxs-lookup"><span data-stu-id="1f771-269">Contact type</span></span> |
| <span data-ttu-id="1f771-270">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="1f771-270">AssignedTo_s</span></span> | <span data-ttu-id="1f771-271">Assigned to</span><span class="sxs-lookup"><span data-stu-id="1f771-271">Assigned to</span></span>  |
| <span data-ttu-id="1f771-272">Category_s</span><span class="sxs-lookup"><span data-stu-id="1f771-272">Category_s</span></span> | <span data-ttu-id="1f771-273">Category</span><span class="sxs-lookup"><span data-stu-id="1f771-273">Category</span></span> |
| <span data-ttu-id="1f771-274">Title_s</span><span class="sxs-lookup"><span data-stu-id="1f771-274">Title_s</span></span>|  <span data-ttu-id="1f771-275">Short description</span><span class="sxs-lookup"><span data-stu-id="1f771-275">Short description</span></span> |
| <span data-ttu-id="1f771-276">Description_s</span><span class="sxs-lookup"><span data-stu-id="1f771-276">Description_s</span></span>|  <span data-ttu-id="1f771-277">Notes</span><span class="sxs-lookup"><span data-stu-id="1f771-277">Notes</span></span> |
| <span data-ttu-id="1f771-278">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-278">CreatedDate_t</span></span>|  <span data-ttu-id="1f771-279">Opened</span><span class="sxs-lookup"><span data-stu-id="1f771-279">Opened</span></span> |
| <span data-ttu-id="1f771-280">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-280">ClosedDate_t</span></span>| <span data-ttu-id="1f771-281">closed</span><span class="sxs-lookup"><span data-stu-id="1f771-281">closed</span></span>|
| <span data-ttu-id="1f771-282">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-282">ResolvedDate_t</span></span>|<span data-ttu-id="1f771-283">Resolved</span><span class="sxs-lookup"><span data-stu-id="1f771-283">Resolved</span></span>|
| <span data-ttu-id="1f771-284">Computer</span><span class="sxs-lookup"><span data-stu-id="1f771-284">Computer</span></span>  | <span data-ttu-id="1f771-285">Configuration item</span><span class="sxs-lookup"><span data-stu-id="1f771-285">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="1f771-286">Output data for a ServiceNow change request</span><span class="sxs-lookup"><span data-stu-id="1f771-286">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="1f771-287">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1f771-287">Log Analytics</span></span> | <span data-ttu-id="1f771-288">ServieNow field</span><span class="sxs-lookup"><span data-stu-id="1f771-288">ServieNow field</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f771-289">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="1f771-289">ServiceDeskId_s</span></span>| <span data-ttu-id="1f771-290">Number</span><span class="sxs-lookup"><span data-stu-id="1f771-290">Number</span></span> |
| <span data-ttu-id="1f771-291">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="1f771-291">CreatedBy_s</span></span> | <span data-ttu-id="1f771-292">Requested by</span><span class="sxs-lookup"><span data-stu-id="1f771-292">Requested by</span></span> |
| <span data-ttu-id="1f771-293">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="1f771-293">ClosedBy_s</span></span> | <span data-ttu-id="1f771-294">Closed by</span><span class="sxs-lookup"><span data-stu-id="1f771-294">Closed by</span></span> |
| <span data-ttu-id="1f771-295">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="1f771-295">AssignedTo_s</span></span> | <span data-ttu-id="1f771-296">Assigned to</span><span class="sxs-lookup"><span data-stu-id="1f771-296">Assigned to</span></span>  |
| <span data-ttu-id="1f771-297">Title_s</span><span class="sxs-lookup"><span data-stu-id="1f771-297">Title_s</span></span>|  <span data-ttu-id="1f771-298">Short description</span><span class="sxs-lookup"><span data-stu-id="1f771-298">Short description</span></span> |
| <span data-ttu-id="1f771-299">Type_s</span><span class="sxs-lookup"><span data-stu-id="1f771-299">Type_s</span></span>|  <span data-ttu-id="1f771-300">Type</span><span class="sxs-lookup"><span data-stu-id="1f771-300">Type</span></span> |
| <span data-ttu-id="1f771-301">Category_s</span><span class="sxs-lookup"><span data-stu-id="1f771-301">Category_s</span></span>|  <span data-ttu-id="1f771-302">Category</span><span class="sxs-lookup"><span data-stu-id="1f771-302">Category</span></span> |
| <span data-ttu-id="1f771-303">CRState_s</span><span class="sxs-lookup"><span data-stu-id="1f771-303">CRState_s</span></span>|  <span data-ttu-id="1f771-304">State</span><span class="sxs-lookup"><span data-stu-id="1f771-304">State</span></span>|
| <span data-ttu-id="1f771-305">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="1f771-305">Urgency_s</span></span>|  <span data-ttu-id="1f771-306">Urgency</span><span class="sxs-lookup"><span data-stu-id="1f771-306">Urgency</span></span> |
| <span data-ttu-id="1f771-307">Priority_s</span><span class="sxs-lookup"><span data-stu-id="1f771-307">Priority_s</span></span>| <span data-ttu-id="1f771-308">Priority</span><span class="sxs-lookup"><span data-stu-id="1f771-308">Priority</span></span>|
| <span data-ttu-id="1f771-309">Risk_s</span><span class="sxs-lookup"><span data-stu-id="1f771-309">Risk_s</span></span>| <span data-ttu-id="1f771-310">Risk</span><span class="sxs-lookup"><span data-stu-id="1f771-310">Risk</span></span>|
| <span data-ttu-id="1f771-311">Impact_s</span><span class="sxs-lookup"><span data-stu-id="1f771-311">Impact_s</span></span>| <span data-ttu-id="1f771-312">Impact</span><span class="sxs-lookup"><span data-stu-id="1f771-312">Impact</span></span>|
| <span data-ttu-id="1f771-313">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-313">RequestedDate_t</span></span>  | <span data-ttu-id="1f771-314">Requested by date</span><span class="sxs-lookup"><span data-stu-id="1f771-314">Requested by date</span></span> |
| <span data-ttu-id="1f771-315">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-315">ClosedDate_t</span></span> | <span data-ttu-id="1f771-316">Closed date</span><span class="sxs-lookup"><span data-stu-id="1f771-316">Closed date</span></span> |
| <span data-ttu-id="1f771-317">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-317">PlannedStartDate_t</span></span>  |     <span data-ttu-id="1f771-318">Planned start date</span><span class="sxs-lookup"><span data-stu-id="1f771-318">Planned start date</span></span> |
| <span data-ttu-id="1f771-319">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-319">PlannedEndDate_t</span></span>  |   <span data-ttu-id="1f771-320">Planned end date</span><span class="sxs-lookup"><span data-stu-id="1f771-320">Planned end date</span></span> |
| <span data-ttu-id="1f771-321">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-321">WorkStartDate_t</span></span>  | <span data-ttu-id="1f771-322">Actual start date</span><span class="sxs-lookup"><span data-stu-id="1f771-322">Actual start date</span></span> |
| <span data-ttu-id="1f771-323">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="1f771-323">WorkEndDate_t</span></span> | <span data-ttu-id="1f771-324">Actual end date</span><span class="sxs-lookup"><span data-stu-id="1f771-324">Actual end date</span></span>|
| <span data-ttu-id="1f771-325">Description_s</span><span class="sxs-lookup"><span data-stu-id="1f771-325">Description_s</span></span> | <span data-ttu-id="1f771-326">Description</span><span class="sxs-lookup"><span data-stu-id="1f771-326">Description</span></span> |
| <span data-ttu-id="1f771-327">Computer</span><span class="sxs-lookup"><span data-stu-id="1f771-327">Computer</span></span>  | <span data-ttu-id="1f771-328">Configuration Item</span><span class="sxs-lookup"><span data-stu-id="1f771-328">Configuration Item</span></span> |


## <a name="troubleshoot-itsm-connections"></a><span data-ttu-id="1f771-329">Troubleshoot ITSM connections</span><span class="sxs-lookup"><span data-stu-id="1f771-329">Troubleshoot ITSM connections</span></span>
1.  <span data-ttu-id="1f771-330">If connection fails from connected source's UI with an **Error in saving connection** message, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f771-330">If connection fails from connected source's UI with an **Error in saving connection** message, take the following steps:</span></span>
 - <span data-ttu-id="1f771-331">For ServiceNow, Cherwell and Provance connections,</span><span class="sxs-lookup"><span data-stu-id="1f771-331">For ServiceNow, Cherwell and Provance connections,</span></span>  
    - <span data-ttu-id="1f771-332">ensure you correctly entered  the username, password, client ID, and client secret  for each of the connections.</span><span class="sxs-lookup"><span data-stu-id="1f771-332">ensure you correctly entered  the username, password, client ID, and client secret  for each of the connections.</span></span>  
    - <span data-ttu-id="1f771-333">check if you have sufficient privileges in the corresponding ITSM product to make the connection.</span><span class="sxs-lookup"><span data-stu-id="1f771-333">check if you have sufficient privileges in the corresponding ITSM product to make the connection.</span></span>  
 - <span data-ttu-id="1f771-334">For Service Manager connections,</span><span class="sxs-lookup"><span data-stu-id="1f771-334">For Service Manager connections,</span></span>  
    - <span data-ttu-id="1f771-335">ensure that the Web app is successfully deployed and hybrid connection is created.</span><span class="sxs-lookup"><span data-stu-id="1f771-335">ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="1f771-336">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="1f771-336">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>  

2.  <span data-ttu-id="1f771-337">If data from ServiceNow is not getting synced to Log Analytics, ensure that the ServiceNow instance is not sleeping.</span><span class="sxs-lookup"><span data-stu-id="1f771-337">If data from ServiceNow is not getting synced to Log Analytics, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="1f771-338">ServiceNow Dev Instances sometimes go to sleep when idle for a long period.</span><span class="sxs-lookup"><span data-stu-id="1f771-338">ServiceNow Dev Instances sometimes go to sleep when idle for a long period.</span></span> <span data-ttu-id="1f771-339">Else, report the issue.</span><span class="sxs-lookup"><span data-stu-id="1f771-339">Else, report the issue.</span></span>
3.  <span data-ttu-id="1f771-340">If OMS Alerts fire but work items are not created in ITSM product or configuration items are not created/linked to work items or for any other generic information, look in the following places:</span><span class="sxs-lookup"><span data-stu-id="1f771-340">If OMS Alerts fire but work items are not created in ITSM product or configuration items are not created/linked to work items or for any other generic information, look in the following places:</span></span>
 -  <span data-ttu-id="1f771-341">ITSMC: The solution shows a summary of connections/work items/computers etc. Click the tile showing **Connector Status**, which takes you to **Log Search**  with the relevant query.</span><span class="sxs-lookup"><span data-stu-id="1f771-341">ITSMC: The solution shows a summary of connections/work items/computers etc. Click the tile showing **Connector Status**, which takes you to **Log Search**  with the relevant query.</span></span> <span data-ttu-id="1f771-342">Look at the log records with LogType_S as ERROR for more information.</span><span class="sxs-lookup"><span data-stu-id="1f771-342">Look at the log records with LogType_S as ERROR for more information.</span></span>
 - <span data-ttu-id="1f771-343">**Log Search** page: view the errors/related information directly using the query `*`ServiceDeskLog_CL`*`.</span><span class="sxs-lookup"><span data-stu-id="1f771-343">**Log Search** page: view the errors/related information directly using the query `*`ServiceDeskLog_CL`*`.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="1f771-344">Troubleshoot Service Manager Web App deployment</span><span class="sxs-lookup"><span data-stu-id="1f771-344">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="1f771-345">In case of any issues with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span><span class="sxs-lookup"><span data-stu-id="1f771-345">In case of any issues with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="1f771-346">If you get an **"Object reference not set to instance of an object"** error when you run the [script](log-analytics-itsmc-service-manager-script.md), ensure that you entered valid values  under **User Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="1f771-346">If you get an **"Object reference not set to instance of an object"** error when you run the [script](log-analytics-itsmc-service-manager-script.md), ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="1f771-347">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span><span class="sxs-lookup"><span data-stu-id="1f771-347">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="1f771-348">If not registered, manually create service bus relay namespace from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f771-348">If not registered, manually create service bus relay namespace from the Azure portal.</span></span> <span data-ttu-id="1f771-349">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f771-349">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="1f771-350">Contact us</span><span class="sxs-lookup"><span data-stu-id="1f771-350">Contact us</span></span>

<span data-ttu-id="1f771-351">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1f771-351">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f771-352">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f771-352">Next steps</span></span>
<span data-ttu-id="1f771-353">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="1f771-353">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
