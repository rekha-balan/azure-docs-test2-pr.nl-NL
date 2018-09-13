---
title: Connect Operations Manager to Log Analytics | Microsoft Docs
description: To maintain your existing investment in System Center Operations Manager and use extended capabilities with Log Analytics, you can integrate Operations Manager with your OMS workspace.
services: log-analytics
documentationcenter: ''
author: MGoedtel
manager: jwhit
editor: ''
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: magoedte
ms.openlocfilehash: 863bddab1b4ea31197254c3d5356c6f017d3a917
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556597"
---
# <a name="connect-operations-manager-to-log-analytics"></a><span data-ttu-id="8a7af-103">Connect Operations Manager to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8a7af-103">Connect Operations Manager to Log Analytics</span></span>
<span data-ttu-id="8a7af-104">To maintain your existing investment in System Center Operations Manager and use extended capabilities with Log Analytics, you can integrate Operations Manager with your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-104">To maintain your existing investment in System Center Operations Manager and use extended capabilities with Log Analytics, you can integrate Operations Manager with your OMS workspace.</span></span>  <span data-ttu-id="8a7af-105">This allows you leverage the opportunities of OMS while continuing to use Operations Manager to:</span><span class="sxs-lookup"><span data-stu-id="8a7af-105">This allows you leverage the opportunities of OMS while continuing to use Operations Manager to:</span></span>

* <span data-ttu-id="8a7af-106">Continue monitoring the health of your IT services with Operations Manager</span><span class="sxs-lookup"><span data-stu-id="8a7af-106">Continue monitoring the health of your IT services with Operations Manager</span></span>
* <span data-ttu-id="8a7af-107">Maintain integration with your ITSM solutions supporting incident and problem management</span><span class="sxs-lookup"><span data-stu-id="8a7af-107">Maintain integration with your ITSM solutions supporting incident and problem management</span></span>
* <span data-ttu-id="8a7af-108">Manage the lifecycle of agents deployed to on-premises and public cloud IaaS virtual machines that you monitor with Operations Manager</span><span class="sxs-lookup"><span data-stu-id="8a7af-108">Manage the lifecycle of agents deployed to on-premises and public cloud IaaS virtual machines that you monitor with Operations Manager</span></span>

<span data-ttu-id="8a7af-109">Integrating with System Center Operations Manager adds value to your service operations strategy by leveraging the speed and efficiency of OMS in collecting, storing and analyzing data from Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="8a7af-109">Integrating with System Center Operations Manager adds value to your service operations strategy by leveraging the speed and efficiency of OMS in collecting, storing and analyzing data from Operations Manager.</span></span>  <span data-ttu-id="8a7af-110">OMS helps correlate and work towards identifying the faults of problems and surfacing reoccurrences in support of your existing problem management process.</span><span class="sxs-lookup"><span data-stu-id="8a7af-110">OMS helps correlate and work towards identifying the faults of problems and surfacing reoccurrences in support of your existing problem management process.</span></span>   <span data-ttu-id="8a7af-111">The flexibility of the search engine to examine performance, event and alert data, with rich dashboards and reporting capabilities to expose this data in meaningful ways, demonstrates the strength OMS brings in complimenting Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="8a7af-111">The flexibility of the search engine to examine performance, event and alert data, with rich dashboards and reporting capabilities to expose this data in meaningful ways, demonstrates the strength OMS brings in complimenting Operations Manager.</span></span>

<span data-ttu-id="8a7af-112">The agents reporting to the Operations Manager management group collect data from your servers based on the Log Analytics data sources and solutions you have enabled in your OMS subscription.</span><span class="sxs-lookup"><span data-stu-id="8a7af-112">The agents reporting to the Operations Manager management group collect data from your servers based on the Log Analytics data sources and solutions you have enabled in your OMS subscription.</span></span>  <span data-ttu-id="8a7af-113">Depending on the solution you have enabled, data from these solutions are either sent directly from an Operations Manager management server to the OMS web service, or because of the volume of data collected on the agent-managed system, are sent directly from the agent to OMS web service.</span><span class="sxs-lookup"><span data-stu-id="8a7af-113">Depending on the solution you have enabled, data from these solutions are either sent directly from an Operations Manager management server to the OMS web service, or because of the volume of data collected on the agent-managed system, are sent directly from the agent to OMS web service.</span></span> <span data-ttu-id="8a7af-114">The management server directly forwards the OMS data to the OMS web service, it is never written to the OperationsManager or OperationsManagerDW database.</span><span class="sxs-lookup"><span data-stu-id="8a7af-114">The management server directly forwards the OMS data to the OMS web service, it is never written to the OperationsManager or OperationsManagerDW database.</span></span>  <span data-ttu-id="8a7af-115">When a management server loses connectivity with the OMS web service, it caches the data locally until communication is re-established with OMS.</span><span class="sxs-lookup"><span data-stu-id="8a7af-115">When a management server loses connectivity with the OMS web service, it caches the data locally until communication is re-established with OMS.</span></span>  <span data-ttu-id="8a7af-116">If the management server is offline due to planned maintenance or unplanned outage, another management server in the management group will resume connectivity with OMS.</span><span class="sxs-lookup"><span data-stu-id="8a7af-116">If the management server is offline due to planned maintenance or unplanned outage, another management server in the management group will resume connectivity with OMS.</span></span>  

<span data-ttu-id="8a7af-117">The following diagram depicts the connection between the management servers and agents in a System Center Operations Manager management group and OMS, including the direction and ports.</span><span class="sxs-lookup"><span data-stu-id="8a7af-117">The following diagram depicts the connection between the management servers and agents in a System Center Operations Manager management group and OMS, including the direction and ports.</span></span>   

![oms-operations-manager-integration-diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-om-agents/oms-operations-manager-connection.png)

<span data-ttu-id="8a7af-119">If your IT security policies do not allow computers on your network to connect to the Internet, management servers can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span><span class="sxs-lookup"><span data-stu-id="8a7af-119">If your IT security policies do not allow computers on your network to connect to the Internet, management servers can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span>  <span data-ttu-id="8a7af-120">For additional information and steps on how to configure your Operations Manager management group to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8a7af-120">For additional information and steps on how to configure your Operations Manager management group to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

## <a name="system-requirements"></a><span data-ttu-id="8a7af-121">System requirements</span><span class="sxs-lookup"><span data-stu-id="8a7af-121">System requirements</span></span>
<span data-ttu-id="8a7af-122">Before starting, review the following details to verify you meet necessary prerequisites.</span><span class="sxs-lookup"><span data-stu-id="8a7af-122">Before starting, review the following details to verify you meet necessary prerequisites.</span></span>

* <span data-ttu-id="8a7af-123">OMS only supports Operations Manager 2016, Operations Manager 2012 SP1 UR6 and greater, and Operations Manager 2012 R2 UR2 and greater.</span><span class="sxs-lookup"><span data-stu-id="8a7af-123">OMS only supports Operations Manager 2016, Operations Manager 2012 SP1 UR6 and greater, and Operations Manager 2012 R2 UR2 and greater.</span></span>  <span data-ttu-id="8a7af-124">Proxy support was added in Operations Manager 2012 SP1 UR7 and Operations Manager 2012 R2 UR3.</span><span class="sxs-lookup"><span data-stu-id="8a7af-124">Proxy support was added in Operations Manager 2012 SP1 UR7 and Operations Manager 2012 R2 UR3.</span></span>
* <span data-ttu-id="8a7af-125">All Operations Manager agents must meet minimum support requirements.</span><span class="sxs-lookup"><span data-stu-id="8a7af-125">All Operations Manager agents must meet minimum support requirements.</span></span> <span data-ttu-id="8a7af-126">Ensure that agents are up to the minimum update, otherwise Windows agent traffic will fail and many errors might fill the Operations Manager event log.</span><span class="sxs-lookup"><span data-stu-id="8a7af-126">Ensure that agents are up to the minimum update, otherwise Windows agent traffic will fail and many errors might fill the Operations Manager event log.</span></span>
* <span data-ttu-id="8a7af-127">An OMS subscription.</span><span class="sxs-lookup"><span data-stu-id="8a7af-127">An OMS subscription.</span></span>  <span data-ttu-id="8a7af-128">For further information, review [Get started with Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a7af-128">For further information, review [Get started with Log Analytics](log-analytics-get-started.md).</span></span>

## <a name="connecting-operations-manager-to-oms"></a><span data-ttu-id="8a7af-129">Connecting Operations Manager to OMS</span><span class="sxs-lookup"><span data-stu-id="8a7af-129">Connecting Operations Manager to OMS</span></span>
<span data-ttu-id="8a7af-130">Perform the following series of steps to configure your Operations Manager management group to connect to one of your OMS workspaces.</span><span class="sxs-lookup"><span data-stu-id="8a7af-130">Perform the following series of steps to configure your Operations Manager management group to connect to one of your OMS workspaces.</span></span>

1. <span data-ttu-id="8a7af-131">In the Operations Manager console, select the **Administration** workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-131">In the Operations Manager console, select the **Administration** workspace.</span></span>
2. <span data-ttu-id="8a7af-132">Expand the Operations Management Suite node and click **Connection**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-132">Expand the Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="8a7af-133">Click the **Register to Operations Management Suite** link.</span><span class="sxs-lookup"><span data-stu-id="8a7af-133">Click the **Register to Operations Management Suite** link.</span></span>
4. <span data-ttu-id="8a7af-134">On the **Operations Management Suite Onboarding Wizard: Authentication** page, enter the email address or phone number and password of the administrator account that is associated with your OMS subscription, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-134">On the **Operations Management Suite Onboarding Wizard: Authentication** page, enter the email address or phone number and password of the administrator account that is associated with your OMS subscription, and click **Sign in**.</span></span>
5. <span data-ttu-id="8a7af-135">After you are successfully authenticated, on the **Operations Management Suite Onboarding Wizard: Select Workspace** page, you will be prompted to select your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-135">After you are successfully authenticated, on the **Operations Management Suite Onboarding Wizard: Select Workspace** page, you will be prompted to select your OMS workspace.</span></span>  <span data-ttu-id="8a7af-136">If you have more than one workspace, select the workspace you want to register with the Operations Manager management group from the drop-down list, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-136">If you have more than one workspace, select the workspace you want to register with the Operations Manager management group from the drop-down list, and then click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a7af-137">Operations Manager only supports one OMS workspace at a time.</span><span class="sxs-lookup"><span data-stu-id="8a7af-137">Operations Manager only supports one OMS workspace at a time.</span></span> <span data-ttu-id="8a7af-138">The connection and the computers that were registered to OMS with the previous workspace are removed from OMS.</span><span class="sxs-lookup"><span data-stu-id="8a7af-138">The connection and the computers that were registered to OMS with the previous workspace are removed from OMS.</span></span>
   > 
   > 
6. <span data-ttu-id="8a7af-139">On the **Operations Management Suite Onboarding Wizard: Summary** page, confirm your settings and if they are correct, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-139">On the **Operations Management Suite Onboarding Wizard: Summary** page, confirm your settings and if they are correct, click **Create**.</span></span>
7. <span data-ttu-id="8a7af-140">On the **Operations Management Suite Onboarding Wizard: Finish** page, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-140">On the **Operations Management Suite Onboarding Wizard: Finish** page, click **Close**.</span></span>

### <a name="add-agent-managed-computers"></a><span data-ttu-id="8a7af-141">Add agent-managed computers</span><span class="sxs-lookup"><span data-stu-id="8a7af-141">Add agent-managed computers</span></span>
<span data-ttu-id="8a7af-142">After configuring integration with your OMS workspace, this only establishes a connection with OMS, no data is collected from the agents reporting to your management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-142">After configuring integration with your OMS workspace, this only establishes a connection with OMS, no data is collected from the agents reporting to your management group.</span></span> <span data-ttu-id="8a7af-143">This won’t happen until after you configure which specific agent-managed computers will collect data for Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8a7af-143">This won’t happen until after you configure which specific agent-managed computers will collect data for Log Analytics.</span></span> <span data-ttu-id="8a7af-144">You can either select the computer objects individually or you can select a group which contains Windows computer objects.</span><span class="sxs-lookup"><span data-stu-id="8a7af-144">You can either select the computer objects individually or you can select a group which contains Windows computer objects.</span></span> <span data-ttu-id="8a7af-145">You cannot select a group which contains instances of another class, such as logical disks or SQL databases.</span><span class="sxs-lookup"><span data-stu-id="8a7af-145">You cannot select a group which contains instances of another class, such as logical disks or SQL databases.</span></span>

1. <span data-ttu-id="8a7af-146">Open the Operations Manager console and select the **Administration** workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-146">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="8a7af-147">Expand the Operations Management Suite node and click **Connection**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-147">Expand the Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="8a7af-148">Click the **Add a Computer/Group** link under the Actions heading on the right-side of the pane.</span><span class="sxs-lookup"><span data-stu-id="8a7af-148">Click the **Add a Computer/Group** link under the Actions heading on the right-side of the pane.</span></span>
4. <span data-ttu-id="8a7af-149">In the **Computer Search** dialog box you can search for computers or groups monitored by Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="8a7af-149">In the **Computer Search** dialog box you can search for computers or groups monitored by Operations Manager.</span></span> <span data-ttu-id="8a7af-150">Select computers or groups to onboard to OMS, click **Add**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-150">Select computers or groups to onboard to OMS, click **Add**, and then click **OK**.</span></span>

<span data-ttu-id="8a7af-151">You can view computers and groups configured to collect data from the Managed Computers node under Operations Management Suite in the **Administration** workspace of the Operations console.</span><span class="sxs-lookup"><span data-stu-id="8a7af-151">You can view computers and groups configured to collect data from the Managed Computers node under Operations Management Suite in the **Administration** workspace of the Operations console.</span></span>  <span data-ttu-id="8a7af-152">From here you can add or remove computers and groups as necessary.</span><span class="sxs-lookup"><span data-stu-id="8a7af-152">From here you can add or remove computers and groups as necessary.</span></span>

### <a name="configure-oms-proxy-settings-in-the-operations-console"></a><span data-ttu-id="8a7af-153">Configure OMS proxy settings in the Operations console</span><span class="sxs-lookup"><span data-stu-id="8a7af-153">Configure OMS proxy settings in the Operations console</span></span>
<span data-ttu-id="8a7af-154">Perform the following steps if an internal proxy server is between the management group and OMS web service.</span><span class="sxs-lookup"><span data-stu-id="8a7af-154">Perform the following steps if an internal proxy server is between the management group and OMS web service.</span></span>  <span data-ttu-id="8a7af-155">These settings are centrally managed from the management group and distributed to agent-managed systems that are included in the scope to collect data for OMS.</span><span class="sxs-lookup"><span data-stu-id="8a7af-155">These settings are centrally managed from the management group and distributed to agent-managed systems that are included in the scope to collect data for OMS.</span></span>  <span data-ttu-id="8a7af-156">This is beneficial for when certain solutions bypass the management server and send data directly to OMS web service.</span><span class="sxs-lookup"><span data-stu-id="8a7af-156">This is beneficial for when certain solutions bypass the management server and send data directly to OMS web service.</span></span>

1. <span data-ttu-id="8a7af-157">Open the Operations Manager console and select the **Administration** workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-157">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="8a7af-158">Expand Operations Management Suite, and then click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-158">Expand Operations Management Suite, and then click **Connections**.</span></span>
3. <span data-ttu-id="8a7af-159">In the OMS Connection view, click **Configure Proxy Server**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-159">In the OMS Connection view, click **Configure Proxy Server**.</span></span>
4. <span data-ttu-id="8a7af-160">On **Operations Management Suite Wizard: Proxy Server** page, select **Use a proxy server to access the Operations Management Suite**, and then type the URL with the port number, for example, http://corpproxy:80 and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-160">On **Operations Management Suite Wizard: Proxy Server** page, select **Use a proxy server to access the Operations Management Suite**, and then type the URL with the port number, for example, http://corpproxy:80 and then click **Finish**.</span></span>

<span data-ttu-id="8a7af-161">If your proxy server requires authentication, perform the following steps to configure credentials and settings that need to propagate to managed computers that will report to OMS in the management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-161">If your proxy server requires authentication, perform the following steps to configure credentials and settings that need to propagate to managed computers that will report to OMS in the management group.</span></span>

1. <span data-ttu-id="8a7af-162">Open the Operations Manager console and select the **Administration** workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-162">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="8a7af-163">Under **RunAs Configuration**, select **Profiles**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-163">Under **RunAs Configuration**, select **Profiles**.</span></span>
3. <span data-ttu-id="8a7af-164">Open the **System Center Advisor Run As Profile Proxy** profile.</span><span class="sxs-lookup"><span data-stu-id="8a7af-164">Open the **System Center Advisor Run As Profile Proxy** profile.</span></span>
4. <span data-ttu-id="8a7af-165">In the Run As Profile Wizard, click Add to use a Run As account.</span><span class="sxs-lookup"><span data-stu-id="8a7af-165">In the Run As Profile Wizard, click Add to use a Run As account.</span></span> <span data-ttu-id="8a7af-166">You can create a new [Run As account](https://technet.microsoft.com/library/hh321655.aspx) or use an existing account.</span><span class="sxs-lookup"><span data-stu-id="8a7af-166">You can create a new [Run As account](https://technet.microsoft.com/library/hh321655.aspx) or use an existing account.</span></span> <span data-ttu-id="8a7af-167">This account needs to have sufficient permissions to pass through the proxy server.</span><span class="sxs-lookup"><span data-stu-id="8a7af-167">This account needs to have sufficient permissions to pass through the proxy server.</span></span>
5. <span data-ttu-id="8a7af-168">To set the account to manage, choose **A selected class, group, or object**, click **Select…**</span><span class="sxs-lookup"><span data-stu-id="8a7af-168">To set the account to manage, choose **A selected class, group, or object**, click **Select…**</span></span> <span data-ttu-id="8a7af-169">and then click **Group…**</span><span class="sxs-lookup"><span data-stu-id="8a7af-169">and then click **Group…**</span></span> <span data-ttu-id="8a7af-170">to open the **Group Search** box.</span><span class="sxs-lookup"><span data-stu-id="8a7af-170">to open the **Group Search** box.</span></span>
6. <span data-ttu-id="8a7af-171">Search for and then select **Microsoft System Center Advisor Monitoring Server Group**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-171">Search for and then select **Microsoft System Center Advisor Monitoring Server Group**.</span></span>  <span data-ttu-id="8a7af-172">Click **OK** after selecting the group to close the **Group Search** box.</span><span class="sxs-lookup"><span data-stu-id="8a7af-172">Click **OK** after selecting the group to close the **Group Search** box.</span></span>
7. <span data-ttu-id="8a7af-173">Click **OK** to close the **Add a Run As account** box.</span><span class="sxs-lookup"><span data-stu-id="8a7af-173">Click **OK** to close the **Add a Run As account** box.</span></span>
8. <span data-ttu-id="8a7af-174">Click **Save** to complete the wizard and save your changes.</span><span class="sxs-lookup"><span data-stu-id="8a7af-174">Click **Save** to complete the wizard and save your changes.</span></span>

<span data-ttu-id="8a7af-175">After the connection is created and you configure which agents will be collecting and reporting data to OMS, the following configuration is applied in the management group, not necessarily in order:</span><span class="sxs-lookup"><span data-stu-id="8a7af-175">After the connection is created and you configure which agents will be collecting and reporting data to OMS, the following configuration is applied in the management group, not necessarily in order:</span></span>

* <span data-ttu-id="8a7af-176">The Run As Account **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** is created.</span><span class="sxs-lookup"><span data-stu-id="8a7af-176">The Run As Account **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** is created.</span></span>  <span data-ttu-id="8a7af-177">It is associated with the Run As profile **Microsoft System Center Advisor Run As Profile Blob** and is targeting two classes - **Collection Server** and **Operations Manager Management Group**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-177">It is associated with the Run As profile **Microsoft System Center Advisor Run As Profile Blob** and is targeting two classes - **Collection Server** and **Operations Manager Management Group**.</span></span>
* <span data-ttu-id="8a7af-178">Two connectors are created.</span><span class="sxs-lookup"><span data-stu-id="8a7af-178">Two connectors are created.</span></span>  <span data-ttu-id="8a7af-179">The first is named **Microsoft.SystemCenter.Advisor.DataConnector** and is automatically configured with a subscription that will forward all alerts generated from instances of all classes in the management group to OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8a7af-179">The first is named **Microsoft.SystemCenter.Advisor.DataConnector** and is automatically configured with a subscription that will forward all alerts generated from instances of all classes in the management group to OMS Log Analytics.</span></span> <span data-ttu-id="8a7af-180">The second connector is **Advisor Connector**, which is responsible for communicating with OMS web service and sharing data.</span><span class="sxs-lookup"><span data-stu-id="8a7af-180">The second connector is **Advisor Connector**, which is responsible for communicating with OMS web service and sharing data.</span></span>
* <span data-ttu-id="8a7af-181">Agents and groups that you have selected to collect data in the management group will be added to the **Microsoft System Center Advisor Monitoring Server Group**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-181">Agents and groups that you have selected to collect data in the management group will be added to the **Microsoft System Center Advisor Monitoring Server Group**.</span></span>

## <a name="management-pack-updates"></a><span data-ttu-id="8a7af-182">Management pack updates</span><span class="sxs-lookup"><span data-stu-id="8a7af-182">Management pack updates</span></span>
<span data-ttu-id="8a7af-183">After configuration is completed, the Operations Manager management group establishes a connection with the OMS service.</span><span class="sxs-lookup"><span data-stu-id="8a7af-183">After configuration is completed, the Operations Manager management group establishes a connection with the OMS service.</span></span>  <span data-ttu-id="8a7af-184">The management server will synchronize with the web service and receive updated configuration information in the form of management packs for the solutions you have enabled that integrate with Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="8a7af-184">The management server will synchronize with the web service and receive updated configuration information in the form of management packs for the solutions you have enabled that integrate with Operations Manager.</span></span>   <span data-ttu-id="8a7af-185">Operations Manager will check for updates to these management packs automatically download and import them when they’re available.</span><span class="sxs-lookup"><span data-stu-id="8a7af-185">Operations Manager will check for updates to these management packs automatically download and import them when they’re available.</span></span>  <span data-ttu-id="8a7af-186">There are two rules in particular which control this behavior:</span><span class="sxs-lookup"><span data-stu-id="8a7af-186">There are two rules in particular which control this behavior:</span></span>

* <span data-ttu-id="8a7af-187">**Microsoft.SystemCenter.Advisor.MPUpdate** - Updates the base OMS management packs.</span><span class="sxs-lookup"><span data-stu-id="8a7af-187">**Microsoft.SystemCenter.Advisor.MPUpdate** - Updates the base OMS management packs.</span></span> <span data-ttu-id="8a7af-188">Runs every twelve (12) hours by default.</span><span class="sxs-lookup"><span data-stu-id="8a7af-188">Runs every twelve (12) hours by default.</span></span>
* <span data-ttu-id="8a7af-189">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - Updates solution management packs enabled in your workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-189">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - Updates solution management packs enabled in your workspace.</span></span> <span data-ttu-id="8a7af-190">Runs every five (5) minutes by default.</span><span class="sxs-lookup"><span data-stu-id="8a7af-190">Runs every five (5) minutes by default.</span></span>

<span data-ttu-id="8a7af-191">You can override these two rules to either prevent automatic download by disabling them, or modify the frequency for how often the management server synchronizes with OMS to determine if a new management pack is available and should be downloaded.</span><span class="sxs-lookup"><span data-stu-id="8a7af-191">You can override these two rules to either prevent automatic download by disabling them, or modify the frequency for how often the management server synchronizes with OMS to determine if a new management pack is available and should be downloaded.</span></span>  <span data-ttu-id="8a7af-192">Follow the steps [How to Override a Rule or Monitor](https://technet.microsoft.com/library/hh212869.aspx) to modify the **Frequency** parameter with a value in seconds to change the synchronization schedule, or modify the **Enabled** parameter to disable the rules.</span><span class="sxs-lookup"><span data-stu-id="8a7af-192">Follow the steps [How to Override a Rule or Monitor](https://technet.microsoft.com/library/hh212869.aspx) to modify the **Frequency** parameter with a value in seconds to change the synchronization schedule, or modify the **Enabled** parameter to disable the rules.</span></span>  <span data-ttu-id="8a7af-193">Target the overrides to all objects of class Operations Manager Management Group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-193">Target the overrides to all objects of class Operations Manager Management Group.</span></span>

<span data-ttu-id="8a7af-194">If you want to continue following your existing change control process for controlling management pack releases in your production management group, you can disable the rules and enable them during specific times when updates are allowed.</span><span class="sxs-lookup"><span data-stu-id="8a7af-194">If you want to continue following your existing change control process for controlling management pack releases in your production management group, you can disable the rules and enable them during specific times when updates are allowed.</span></span> <span data-ttu-id="8a7af-195">If you have a development or QA management group in your environment and it has connectivity to the Internet, you can configure that management group with an OMS workspace to support this scenario.</span><span class="sxs-lookup"><span data-stu-id="8a7af-195">If you have a development or QA management group in your environment and it has connectivity to the Internet, you can configure that management group with an OMS workspace to support this scenario.</span></span>  <span data-ttu-id="8a7af-196">This will allow you to review and evaluate the iterative releases of the OMS management packs before releasing them into your production management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-196">This will allow you to review and evaluate the iterative releases of the OMS management packs before releasing them into your production management group.</span></span>

## <a name="switch-an-operations-manager-group-to-a-new-oms-workspace"></a><span data-ttu-id="8a7af-197">Switch an Operations Manager group to a new OMS Workspace</span><span class="sxs-lookup"><span data-stu-id="8a7af-197">Switch an Operations Manager group to a new OMS Workspace</span></span>
1. <span data-ttu-id="8a7af-198">Log in to your OMS subscription and create new workspace in [Microsoft Operations Management Suite](http://oms.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8a7af-198">Log in to your OMS subscription and create new workspace in [Microsoft Operations Management Suite](http://oms.microsoft.com/).</span></span>
2. <span data-ttu-id="8a7af-199">Open the Operations Manager console with an account that is a member of the Operations Manager Administrators role and select the **Administration** workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-199">Open the Operations Manager console with an account that is a member of the Operations Manager Administrators role and select the **Administration** workspace.</span></span>
3. <span data-ttu-id="8a7af-200">Expand Operations Management Suite, and select **Connections**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-200">Expand Operations Management Suite, and select **Connections**.</span></span>
4. <span data-ttu-id="8a7af-201">Select the **Re-configure Operation Management Suite** link on the middle-side of the pane.</span><span class="sxs-lookup"><span data-stu-id="8a7af-201">Select the **Re-configure Operation Management Suite** link on the middle-side of the pane.</span></span>
5. <span data-ttu-id="8a7af-202">Follow the **Operations Management Suite Onboarding Wizard** and enter the email address or phone number and password of the administrator account that is associated with your new OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-202">Follow the **Operations Management Suite Onboarding Wizard** and enter the email address or phone number and password of the administrator account that is associated with your new OMS workspace.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a7af-203">The **Operations Management Suite Onboarding Wizard: Select Workspace** page will present the existing workspace that is in use.</span><span class="sxs-lookup"><span data-stu-id="8a7af-203">The **Operations Management Suite Onboarding Wizard: Select Workspace** page will present the existing workspace that is in use.</span></span>
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a><span data-ttu-id="8a7af-204">Validate Operations Manager Integration with OMS</span><span class="sxs-lookup"><span data-stu-id="8a7af-204">Validate Operations Manager Integration with OMS</span></span>
<span data-ttu-id="8a7af-205">There are a few different ways you can verify that your OMS to Operations Manager integration is successful.</span><span class="sxs-lookup"><span data-stu-id="8a7af-205">There are a few different ways you can verify that your OMS to Operations Manager integration is successful.</span></span>

### <a name="to-confirm-integration-from-the-oms-portal"></a><span data-ttu-id="8a7af-206">To confirm integration from the OMS portal</span><span class="sxs-lookup"><span data-stu-id="8a7af-206">To confirm integration from the OMS portal</span></span>
1. <span data-ttu-id="8a7af-207">In the OMS portal, click on the **Settings** tile</span><span class="sxs-lookup"><span data-stu-id="8a7af-207">In the OMS portal, click on the **Settings** tile</span></span>
2. <span data-ttu-id="8a7af-208">Select  **Connected Sources**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-208">Select  **Connected Sources**.</span></span>
3. <span data-ttu-id="8a7af-209">In the table under the System Center Operations Manager section, you should see the name of the management group listed with the number of agents and status when data was last received.</span><span class="sxs-lookup"><span data-stu-id="8a7af-209">In the table under the System Center Operations Manager section, you should see the name of the management group listed with the number of agents and status when data was last received.</span></span>
   
   ![oms-settings-connectedsources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. <span data-ttu-id="8a7af-211">Note the **Workspace ID** value under the left-side of the Settings page.</span><span class="sxs-lookup"><span data-stu-id="8a7af-211">Note the **Workspace ID** value under the left-side of the Settings page.</span></span>  <span data-ttu-id="8a7af-212">You will validate it against your Operations Manager management group below.</span><span class="sxs-lookup"><span data-stu-id="8a7af-212">You will validate it against your Operations Manager management group below.</span></span>  

### <a name="to-confirm-integration-from-the-operations-console"></a><span data-ttu-id="8a7af-213">To confirm integration from the Operations console</span><span class="sxs-lookup"><span data-stu-id="8a7af-213">To confirm integration from the Operations console</span></span>
1. <span data-ttu-id="8a7af-214">Open the Operations Manager console and select the **Administration** workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-214">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="8a7af-215">Select **Management Packs** and in the **Look for:** text box type **Advisor** or **Intelligence**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-215">Select **Management Packs** and in the **Look for:** text box type **Advisor** or **Intelligence**.</span></span>
3. <span data-ttu-id="8a7af-216">Depending on the solutions you have enabled, you will see a corresponding management pack listed in the search results.</span><span class="sxs-lookup"><span data-stu-id="8a7af-216">Depending on the solutions you have enabled, you will see a corresponding management pack listed in the search results.</span></span>  <span data-ttu-id="8a7af-217">For example, if you have enabled the Alert Management solution, the management pack Microsoft System Center Advisor Alert Management will be in the list.</span><span class="sxs-lookup"><span data-stu-id="8a7af-217">For example, if you have enabled the Alert Management solution, the management pack Microsoft System Center Advisor Alert Management will be in the list.</span></span>
4. <span data-ttu-id="8a7af-218">From the **Monitoring** view, navigate to the **Operations Management Suite\Health State** view.</span><span class="sxs-lookup"><span data-stu-id="8a7af-218">From the **Monitoring** view, navigate to the **Operations Management Suite\Health State** view.</span></span>  <span data-ttu-id="8a7af-219">Select a Management server under the **Management Server State** pane, and in the **Detail View** pane confirm the value for property **Authentication service URI** matches the OMS Workspace ID.</span><span class="sxs-lookup"><span data-stu-id="8a7af-219">Select a Management server under the **Management Server State** pane, and in the **Detail View** pane confirm the value for property **Authentication service URI** matches the OMS Workspace ID.</span></span>
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a><span data-ttu-id="8a7af-221">Remove Integration with OMS</span><span class="sxs-lookup"><span data-stu-id="8a7af-221">Remove Integration with OMS</span></span>
<span data-ttu-id="8a7af-222">When you no longer require integration between your Operations Manager management group and OMS workspace, there are several steps required to properly remove the connection and configuration in the management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-222">When you no longer require integration between your Operations Manager management group and OMS workspace, there are several steps required to properly remove the connection and configuration in the management group.</span></span> <span data-ttu-id="8a7af-223">The following procedure will have you update your OMS workspace by deleting the reference of your management group, delete the OMS connectors, and then delete management packs supporting OMS.</span><span class="sxs-lookup"><span data-stu-id="8a7af-223">The following procedure will have you update your OMS workspace by deleting the reference of your management group, delete the OMS connectors, and then delete management packs supporting OMS.</span></span>   

<span data-ttu-id="8a7af-224">Management packs for the solutions you have enabled that integrate with Operations Manager as well as the management packs required to support integration with the OMS service cannot be easily deleted from the management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-224">Management packs for the solutions you have enabled that integrate with Operations Manager as well as the management packs required to support integration with the OMS service cannot be easily deleted from the management group.</span></span>  <span data-ttu-id="8a7af-225">This is because some of the OMS management packs have dependencies on other related management packs.</span><span class="sxs-lookup"><span data-stu-id="8a7af-225">This is because some of the OMS management packs have dependencies on other related management packs.</span></span>  <span data-ttu-id="8a7af-226">To delete management packs having a dependency on other management packs, download the script [remove a management pack with dependencies](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) from TechNet Script Center.</span><span class="sxs-lookup"><span data-stu-id="8a7af-226">To delete management packs having a dependency on other management packs, download the script [remove a management pack with dependencies](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) from TechNet Script Center.</span></span>  

1. <span data-ttu-id="8a7af-227">Open the Operations Manager Command Shell with an account that is a member of the Operations Manager Administrators role.</span><span class="sxs-lookup"><span data-stu-id="8a7af-227">Open the Operations Manager Command Shell with an account that is a member of the Operations Manager Administrators role.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="8a7af-228">Verify you do not have any custom management packs with the word Advisor or IntelligencePack in the name before proceeding, otherwise the following steps will delete them from the management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-228">Verify you do not have any custom management packs with the word Advisor or IntelligencePack in the name before proceeding, otherwise the following steps will delete them from the management group.</span></span>
    > 

2. <span data-ttu-id="8a7af-229">From the command shell prompt, type `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="8a7af-229">From the command shell prompt, type `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
3. <span data-ttu-id="8a7af-230">Next type, `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="8a7af-230">Next type, `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
4. <span data-ttu-id="8a7af-231">To remove any management packs remaining which have a dependency on other System Center Advisor management packs, use the script *RecursiveRemove.ps1* you downloaded from the TechNet Script Center earlier.</span><span class="sxs-lookup"><span data-stu-id="8a7af-231">To remove any management packs remaining which have a dependency on other System Center Advisor management packs, use the script *RecursiveRemove.ps1* you downloaded from the TechNet Script Center earlier.</span></span>  
 
    > [!NOTE]
    > <span data-ttu-id="8a7af-232">Do not delete the Microsoft System Center Advisor or Microsoft System Center Advisor Internal management packs.</span><span class="sxs-lookup"><span data-stu-id="8a7af-232">Do not delete the Microsoft System Center Advisor or Microsoft System Center Advisor Internal management packs.</span></span>  
    >  

5. <span data-ttu-id="8a7af-233">Open the Operations Manager Operations console with an account that is a member of the Operations Manager Administrators role.</span><span class="sxs-lookup"><span data-stu-id="8a7af-233">Open the Operations Manager Operations console with an account that is a member of the Operations Manager Administrators role.</span></span>
6. <span data-ttu-id="8a7af-234">Under **Administration**, select the **Management Packs** node and in the **Look for:** box, type **Advisor** and verify the following management packs are still imported in your management group:</span><span class="sxs-lookup"><span data-stu-id="8a7af-234">Under **Administration**, select the **Management Packs** node and in the **Look for:** box, type **Advisor** and verify the following management packs are still imported in your management group:</span></span>
   
   * <span data-ttu-id="8a7af-235">Microsoft System Center Advisor</span><span class="sxs-lookup"><span data-stu-id="8a7af-235">Microsoft System Center Advisor</span></span>
   * <span data-ttu-id="8a7af-236">Microsoft System Center Advisor Internal</span><span class="sxs-lookup"><span data-stu-id="8a7af-236">Microsoft System Center Advisor Internal</span></span>
7. <span data-ttu-id="8a7af-237">In the OMS portal, click on the **Settings** tile.</span><span class="sxs-lookup"><span data-stu-id="8a7af-237">In the OMS portal, click on the **Settings** tile.</span></span>
8. <span data-ttu-id="8a7af-238">Select **Connected Sources**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-238">Select **Connected Sources**.</span></span>
9. <span data-ttu-id="8a7af-239">In the table under the System Center Operations Manager section, you should see the name of the management group you want to remove from the workspace.</span><span class="sxs-lookup"><span data-stu-id="8a7af-239">In the table under the System Center Operations Manager section, you should see the name of the management group you want to remove from the workspace.</span></span>  <span data-ttu-id="8a7af-240">Under the column **Last Data**, click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="8a7af-240">Under the column **Last Data**, click **Remove**.</span></span>  
   
    > [!NOTE]
    > <span data-ttu-id="8a7af-241">The **Remove** link will not be availble until after 14 days if there is no activity detected from the connected management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-241">The **Remove** link will not be availble until after 14 days if there is no activity detected from the connected management group.</span></span>  
    > 

10. <span data-ttu-id="8a7af-242">A window will appear asking you to confirm that you want to proceed with the removal.</span><span class="sxs-lookup"><span data-stu-id="8a7af-242">A window will appear asking you to confirm that you want to proceed with the removal.</span></span>  <span data-ttu-id="8a7af-243">Click **Yes** to proceed.</span><span class="sxs-lookup"><span data-stu-id="8a7af-243">Click **Yes** to proceed.</span></span> 

<span data-ttu-id="8a7af-244">To delete the two connectors - Microsoft.SystemCenter.Advisor.DataConnector and Advisor Connector, save the PowerShell script below to your computer and execute using the following examples.</span><span class="sxs-lookup"><span data-stu-id="8a7af-244">To delete the two connectors - Microsoft.SystemCenter.Advisor.DataConnector and Advisor Connector, save the PowerShell script below to your computer and execute using the following examples.</span></span>

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> <span data-ttu-id="8a7af-245">The computer you run this script from, if not a management server, should have the Operations Manager command shell installed depending on the version of your management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-245">The computer you run this script from, if not a management server, should have the Operations Manager command shell installed depending on the version of your management group.</span></span>
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with the specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with the specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

<span data-ttu-id="8a7af-246">In the future if you plan on reconnecting your management group to an OMS workspace, you will need to re-import the `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` management pack file from the most recent update rollup applied to your management group.</span><span class="sxs-lookup"><span data-stu-id="8a7af-246">In the future if you plan on reconnecting your management group to an OMS workspace, you will need to re-import the `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` management pack file from the most recent update rollup applied to your management group.</span></span>  <span data-ttu-id="8a7af-247">You can find this file in the `%ProgramFiles%\Microsoft System Center 2012` or the `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` folder.</span><span class="sxs-lookup"><span data-stu-id="8a7af-247">You can find this file in the `%ProgramFiles%\Microsoft System Center 2012` or the `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a7af-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a7af-248">Next steps</span></span>
* <span data-ttu-id="8a7af-249">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span><span class="sxs-lookup"><span data-stu-id="8a7af-249">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="8a7af-250">[Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md) if your organization uses a proxy server or firewall so that agents can communicate with the Log Analytics service.</span><span class="sxs-lookup"><span data-stu-id="8a7af-250">[Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md) if your organization uses a proxy server or firewall so that agents can communicate with the Log Analytics service.</span></span>




