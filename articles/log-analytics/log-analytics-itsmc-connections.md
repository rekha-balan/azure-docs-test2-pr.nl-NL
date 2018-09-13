---
title: Supported connections with IT Service Management Connector in Azure Log Analytics | Microsoft Docs
description: This article provides information about how to connect your ITSM products/services with the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage the ITSM work items.
documentationcenter: ''
author: jyothirmaisuri
manager: riyazp
editor: ''
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/24/2018
ms.author: v-jysur
ms.component: na
ms.openlocfilehash: 661107779b74b6e21dec01aecf6d545ec2b7a702
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868652"
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector"></a><span data-ttu-id="b65ce-103">Connect ITSM products/services with IT Service Management Connector</span><span class="sxs-lookup"><span data-stu-id="b65ce-103">Connect ITSM products/services with IT Service Management Connector</span></span>
<span data-ttu-id="b65ce-104">This article provides information about how to configure the connection between your ITSM product/service and the IT Service Management Connector (ITSMC) in Log Analytics to centrally manage your work items.</span><span class="sxs-lookup"><span data-stu-id="b65ce-104">This article provides information about how to configure the connection between your ITSM product/service and the IT Service Management Connector (ITSMC) in Log Analytics to centrally manage your work items.</span></span> <span data-ttu-id="b65ce-105">For more information about ITSMC,  see [Overview](log-analytics-itsmc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b65ce-105">For more information about ITSMC,  see [Overview](log-analytics-itsmc-overview.md).</span></span>

<span data-ttu-id="b65ce-106">The following ITSM products/services are supported.</span><span class="sxs-lookup"><span data-stu-id="b65ce-106">The following ITSM products/services are supported.</span></span> <span data-ttu-id="b65ce-107">Select the product to view detailed information about how to connect the product to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-107">Select the product to view detailed information about how to connect the product to ITSMC.</span></span>

- [<span data-ttu-id="b65ce-108">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="b65ce-108">System Center Service Manager</span></span>](#connect-system-center-service-manager-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="b65ce-109">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="b65ce-109">ServiceNow</span></span>](#connect-servicenow-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="b65ce-110">Provance</span><span class="sxs-lookup"><span data-stu-id="b65ce-110">Provance</span></span>](#connect-provance-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="b65ce-111">Cherwell</span><span class="sxs-lookup"><span data-stu-id="b65ce-111">Cherwell</span></span>](#connect-cherwell-to-it-service-management-connector-in-azure)

> [!NOTE]

> <span data-ttu-id="b65ce-112">ITSM Connector can only connect to cloud-based ServiceNow instances.</span><span class="sxs-lookup"><span data-stu-id="b65ce-112">ITSM Connector can only connect to cloud-based ServiceNow instances.</span></span> <span data-ttu-id="b65ce-113">On-premises ServiceNow instances are currently not supported.</span><span class="sxs-lookup"><span data-stu-id="b65ce-113">On-premises ServiceNow instances are currently not supported.</span></span>

## <a name="connect-system-center-service-manager-to-it-service-management-connector-in-azure"></a><span data-ttu-id="b65ce-114">Connect System Center Service Manager to IT Service Management Connector in Azure</span><span class="sxs-lookup"><span data-stu-id="b65ce-114">Connect System Center Service Manager to IT Service Management Connector in Azure</span></span>

<span data-ttu-id="b65ce-115">The following sections provide details about how to connect your System Center Service Manager product to ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-115">The following sections provide details about how to connect your System Center Service Manager product to ITSMC in Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b65ce-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b65ce-116">Prerequisites</span></span>

<span data-ttu-id="b65ce-117">Ensure the following prerequisites are met:</span><span class="sxs-lookup"><span data-stu-id="b65ce-117">Ensure the following prerequisites are met:</span></span>

- <span data-ttu-id="b65ce-118">ITSMC installed.</span><span class="sxs-lookup"><span data-stu-id="b65ce-118">ITSMC installed.</span></span> <span data-ttu-id="b65ce-119">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span><span class="sxs-lookup"><span data-stu-id="b65ce-119">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span></span>
- <span data-ttu-id="b65ce-120">The Service Manager Web application (Web app) is deployed and configured.</span><span class="sxs-lookup"><span data-stu-id="b65ce-120">The Service Manager Web application (Web app) is deployed and configured.</span></span> <span data-ttu-id="b65ce-121">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span><span class="sxs-lookup"><span data-stu-id="b65ce-121">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
- <span data-ttu-id="b65ce-122">Hybrid connection created and configured.</span><span class="sxs-lookup"><span data-stu-id="b65ce-122">Hybrid connection created and configured.</span></span> <span data-ttu-id="b65ce-123">More information: [Configure the hybrid Connection](#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="b65ce-123">More information: [Configure the hybrid Connection](#configure-the-hybrid-connection).</span></span>
- <span data-ttu-id="b65ce-124">Supported versions of Service Manager:  2012 R2 or 2016.</span><span class="sxs-lookup"><span data-stu-id="b65ce-124">Supported versions of Service Manager:  2012 R2 or 2016.</span></span>
- <span data-ttu-id="b65ce-125">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span><span class="sxs-lookup"><span data-stu-id="b65ce-125">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="b65ce-126">Connection procedure</span><span class="sxs-lookup"><span data-stu-id="b65ce-126">Connection procedure</span></span>

<span data-ttu-id="b65ce-127">Use the following procedure to connect your System Center Service Manager instance to ITSMC:</span><span class="sxs-lookup"><span data-stu-id="b65ce-127">Use the following procedure to connect your System Center Service Manager instance to ITSMC:</span></span>

1. <span data-ttu-id="b65ce-128">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span><span class="sxs-lookup"><span data-stu-id="b65ce-128">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span></span>

2.  <span data-ttu-id="b65ce-129">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-129">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span></span>

    ![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)

3. <span data-ttu-id="b65ce-131">At the top of the right pane, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-131">At the top of the right pane, click **Add**.</span></span>

4. <span data-ttu-id="b65ce-132">Provide the information as described in the following table, and click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-132">Provide the information as described in the following table, and click **OK** to create the connection.</span></span>

> [!NOTE]

> <span data-ttu-id="b65ce-133">All these parameters are mandatory.</span><span class="sxs-lookup"><span data-stu-id="b65ce-133">All these parameters are mandatory.</span></span>

| <span data-ttu-id="b65ce-134">**Field**</span><span class="sxs-lookup"><span data-stu-id="b65ce-134">**Field**</span></span> | <span data-ttu-id="b65ce-135">**Description**</span><span class="sxs-lookup"><span data-stu-id="b65ce-135">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b65ce-136">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="b65ce-136">**Connection Name**</span></span>   | <span data-ttu-id="b65ce-137">Type a name for the System Center Service Manager instance that you want to connect with ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-137">Type a name for the System Center Service Manager instance that you want to connect with ITSMC.</span></span>  <span data-ttu-id="b65ce-138">You use this name later when you configure work items in this instance/ view detailed log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-138">You use this name later when you configure work items in this instance/ view detailed log analytics.</span></span> |
| <span data-ttu-id="b65ce-139">**Partner type**</span><span class="sxs-lookup"><span data-stu-id="b65ce-139">**Partner type**</span></span>   | <span data-ttu-id="b65ce-140">Select **System Center Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-140">Select **System Center Service Manager**.</span></span> |
| <span data-ttu-id="b65ce-141">**Server URL**</span><span class="sxs-lookup"><span data-stu-id="b65ce-141">**Server URL**</span></span>   | <span data-ttu-id="b65ce-142">Type the URL of the Service Manager Web app.</span><span class="sxs-lookup"><span data-stu-id="b65ce-142">Type the URL of the Service Manager Web app.</span></span> <span data-ttu-id="b65ce-143">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span><span class="sxs-lookup"><span data-stu-id="b65ce-143">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
| <span data-ttu-id="b65ce-144">**Client ID**</span><span class="sxs-lookup"><span data-stu-id="b65ce-144">**Client ID**</span></span>   | <span data-ttu-id="b65ce-145">Type the client ID that you generated (using the automatic script) for authenticating the Web app.</span><span class="sxs-lookup"><span data-stu-id="b65ce-145">Type the client ID that you generated (using the automatic script) for authenticating the Web app.</span></span> <span data-ttu-id="b65ce-146">More information about the automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span><span class="sxs-lookup"><span data-stu-id="b65ce-146">More information about the automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span></span>|
| <span data-ttu-id="b65ce-147">**Client Secret**</span><span class="sxs-lookup"><span data-stu-id="b65ce-147">**Client Secret**</span></span>   | <span data-ttu-id="b65ce-148">Type the client secret, generated for this ID.</span><span class="sxs-lookup"><span data-stu-id="b65ce-148">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="b65ce-149">**Data Sync Scope**</span><span class="sxs-lookup"><span data-stu-id="b65ce-149">**Data Sync Scope**</span></span>   | <span data-ttu-id="b65ce-150">Select the Service Manager work items that you want to sync through ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-150">Select the Service Manager work items that you want to sync through ITSMC.</span></span>  <span data-ttu-id="b65ce-151">These work items are imported into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-151">These work items are imported into Log Analytics.</span></span> <span data-ttu-id="b65ce-152">**Options:**  Incidents, Change Requests.</span><span class="sxs-lookup"><span data-stu-id="b65ce-152">**Options:**  Incidents, Change Requests.</span></span>|
| <span data-ttu-id="b65ce-153">**Sync Data**</span><span class="sxs-lookup"><span data-stu-id="b65ce-153">**Sync Data**</span></span> | <span data-ttu-id="b65ce-154">Type the number of past days that you want the data from.</span><span class="sxs-lookup"><span data-stu-id="b65ce-154">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="b65ce-155">**Maximum limit**: 120 days.</span><span class="sxs-lookup"><span data-stu-id="b65ce-155">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="b65ce-156">**Create new configuration item in ITSM solution**</span><span class="sxs-lookup"><span data-stu-id="b65ce-156">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="b65ce-157">Select this option if you want to create the configuration items in the ITSM product.</span><span class="sxs-lookup"><span data-stu-id="b65ce-157">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="b65ce-158">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span><span class="sxs-lookup"><span data-stu-id="b65ce-158">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="b65ce-159">**Default**: disabled.</span><span class="sxs-lookup"><span data-stu-id="b65ce-159">**Default**: disabled.</span></span> |

![Service manager connection](./media/log-analytics-itsmc/service-manager-connection.png)

<span data-ttu-id="b65ce-161">**When successfully connected, and synced**:</span><span class="sxs-lookup"><span data-stu-id="b65ce-161">**When successfully connected, and synced**:</span></span>

- <span data-ttu-id="b65ce-162">Selected work items from Service Manager are imported into Azure **Log Analytics.**</span><span class="sxs-lookup"><span data-stu-id="b65ce-162">Selected work items from Service Manager are imported into Azure **Log Analytics.**</span></span> <span data-ttu-id="b65ce-163">You can view the summary of these work items on the IT Service Management Connector tile.</span><span class="sxs-lookup"><span data-stu-id="b65ce-163">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="b65ce-164">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this Service Manager instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-164">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this Service Manager instance.</span></span>


<span data-ttu-id="b65ce-165">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="b65ce-165">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span></span>

### <a name="create-and-deploy-service-manager-web-app-service"></a><span data-ttu-id="b65ce-166">Create and deploy Service Manager web app service</span><span class="sxs-lookup"><span data-stu-id="b65ce-166">Create and deploy Service Manager web app service</span></span>

<span data-ttu-id="b65ce-167">To connect the on-premises Service Manager with ITSMC in Azure, Microsoft has created a Service Manager Web app on the GitHub.</span><span class="sxs-lookup"><span data-stu-id="b65ce-167">To connect the on-premises Service Manager with ITSMC in Azure, Microsoft has created a Service Manager Web app on the GitHub.</span></span>

<span data-ttu-id="b65ce-168">To set up the ITSM Web app for your Service Manager, do the following:</span><span class="sxs-lookup"><span data-stu-id="b65ce-168">To set up the ITSM Web app for your Service Manager, do the following:</span></span>

- <span data-ttu-id="b65ce-169">**Deploy the Web app** – Deploy the Web app, set the properties, and authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b65ce-169">**Deploy the Web app** – Deploy the Web app, set the properties, and authenticate with Azure AD.</span></span> <span data-ttu-id="b65ce-170">You can deploy the web app by using the [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span><span class="sxs-lookup"><span data-stu-id="b65ce-170">You can deploy the web app by using the [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span></span>
- <span data-ttu-id="b65ce-171">**Configure the hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span><span class="sxs-lookup"><span data-stu-id="b65ce-171">**Configure the hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span></span>

#### <a name="deploy-the-web-app"></a><span data-ttu-id="b65ce-172">Deploy the web app</span><span class="sxs-lookup"><span data-stu-id="b65ce-172">Deploy the web app</span></span>
<span data-ttu-id="b65ce-173">Use the automated [script](log-analytics-itsmc-service-manager-script.md) to deploy the Web app, set the properties, and authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b65ce-173">Use the automated [script](log-analytics-itsmc-service-manager-script.md) to deploy the Web app, set the properties, and authenticate with Azure AD.</span></span>

<span data-ttu-id="b65ce-174">Run the script by providing the following required details:</span><span class="sxs-lookup"><span data-stu-id="b65ce-174">Run the script by providing the following required details:</span></span>

- <span data-ttu-id="b65ce-175">Azure subscription details</span><span class="sxs-lookup"><span data-stu-id="b65ce-175">Azure subscription details</span></span>
- <span data-ttu-id="b65ce-176">Resource group name</span><span class="sxs-lookup"><span data-stu-id="b65ce-176">Resource group name</span></span>
- <span data-ttu-id="b65ce-177">Location</span><span class="sxs-lookup"><span data-stu-id="b65ce-177">Location</span></span>
- <span data-ttu-id="b65ce-178">Service Manager server details (server name, domain, user name, and password)</span><span class="sxs-lookup"><span data-stu-id="b65ce-178">Service Manager server details (server name, domain, user name, and password)</span></span>
- <span data-ttu-id="b65ce-179">Site name prefix for your Web app</span><span class="sxs-lookup"><span data-stu-id="b65ce-179">Site name prefix for your Web app</span></span>
- <span data-ttu-id="b65ce-180">ServiceBus Namespace.</span><span class="sxs-lookup"><span data-stu-id="b65ce-180">ServiceBus Namespace.</span></span>

<span data-ttu-id="b65ce-181">The script creates the Web app using the name that you specified (along with few additional strings to make it unique).</span><span class="sxs-lookup"><span data-stu-id="b65ce-181">The script creates the Web app using the name that you specified (along with few additional strings to make it unique).</span></span> <span data-ttu-id="b65ce-182">It generates the **Web app URL**, **client ID** and **client secret**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-182">It generates the **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="b65ce-183">Save the values, you use them when you create a connection with ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-183">Save the values, you use them when you create a connection with ITSMC.</span></span>

<span data-ttu-id="b65ce-184">**Check the Web app installation**</span><span class="sxs-lookup"><span data-stu-id="b65ce-184">**Check the Web app installation**</span></span>

1. <span data-ttu-id="b65ce-185">Go to **Azure portal** > **Resources**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-185">Go to **Azure portal** > **Resources**.</span></span>
2. <span data-ttu-id="b65ce-186">Select the Web app, click **Settings** > **Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-186">Select the Web app, click **Settings** > **Application Settings**.</span></span>
3. <span data-ttu-id="b65ce-187">Confirm the information about the Service Manager instance that you provided at the time of deploying the app through the script.</span><span class="sxs-lookup"><span data-stu-id="b65ce-187">Confirm the information about the Service Manager instance that you provided at the time of deploying the app through the script.</span></span>

### <a name="configure-the-hybrid-connection"></a><span data-ttu-id="b65ce-188">Configure the hybrid connection</span><span class="sxs-lookup"><span data-stu-id="b65ce-188">Configure the hybrid connection</span></span>

<span data-ttu-id="b65ce-189">Use the following procedure to configure the hybrid connection that connects the Service Manager instance with ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-189">Use the following procedure to configure the hybrid connection that connects the Service Manager instance with ITSMC in Azure.</span></span>

1. <span data-ttu-id="b65ce-190">Find the Service Manager Web app, under **Azure Resources**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-190">Find the Service Manager Web app, under **Azure Resources**.</span></span>
2. <span data-ttu-id="b65ce-191">Click **Settings** > **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-191">Click **Settings** > **Networking**.</span></span>
3. <span data-ttu-id="b65ce-192">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-192">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span></span>

    ![Hybrid connection networking](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. <span data-ttu-id="b65ce-194">In the **Hybrid Connections** blade, click **Add hybrid connection**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-194">In the **Hybrid Connections** blade, click **Add hybrid connection**.</span></span>

    ![Hybrid connection add](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. <span data-ttu-id="b65ce-196">In the **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-196">In the **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span></span>

    ![New Hybrid connection](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. <span data-ttu-id="b65ce-198">Type the following values:</span><span class="sxs-lookup"><span data-stu-id="b65ce-198">Type the following values:</span></span>

    - <span data-ttu-id="b65ce-199">**EndPoint Name**: Specify a name for the new Hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-199">**EndPoint Name**: Specify a name for the new Hybrid connection.</span></span>
    -  <span data-ttu-id="b65ce-200">**EndPoint Host**: FQDN of the Service Manager management server.</span><span class="sxs-lookup"><span data-stu-id="b65ce-200">**EndPoint Host**: FQDN of the Service Manager management server.</span></span>
    - <span data-ttu-id="b65ce-201">**EndPoint Port**: Type 5724</span><span class="sxs-lookup"><span data-stu-id="b65ce-201">**EndPoint Port**: Type 5724</span></span>
    - <span data-ttu-id="b65ce-202">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span><span class="sxs-lookup"><span data-stu-id="b65ce-202">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span></span>
    - <span data-ttu-id="b65ce-203">**Location**: select the location.</span><span class="sxs-lookup"><span data-stu-id="b65ce-203">**Location**: select the location.</span></span>
    -  <span data-ttu-id="b65ce-204">**Name**: Specify a name to the servicebus if you are creating it.</span><span class="sxs-lookup"><span data-stu-id="b65ce-204">**Name**: Specify a name to the servicebus if you are creating it.</span></span>

    ![Hybrid connection values](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. <span data-ttu-id="b65ce-206">Click **OK** to close the **Create hybrid connection** blade and start creating the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-206">Click **OK** to close the **Create hybrid connection** blade and start creating the hybrid connection.</span></span>

    <span data-ttu-id="b65ce-207">Once the Hybrid connection is created, it is displayed under the blade.</span><span class="sxs-lookup"><span data-stu-id="b65ce-207">Once the Hybrid connection is created, it is displayed under the blade.</span></span>

7. <span data-ttu-id="b65ce-208">After the hybrid connection is created, select the connection and click **Add selected hybrid connection**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-208">After the hybrid connection is created, select the connection and click **Add selected hybrid connection**.</span></span>

    ![New hybrid connection](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-the-listener-setup"></a><span data-ttu-id="b65ce-210">Configure the listener setup</span><span class="sxs-lookup"><span data-stu-id="b65ce-210">Configure the listener setup</span></span>

<span data-ttu-id="b65ce-211">Use the following procedure to configure the listener setup for the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-211">Use the following procedure to configure the listener setup for the hybrid connection.</span></span>

1. <span data-ttu-id="b65ce-212">In the **Hybrid Connections** blade, click **Download the Connection Manager** and install it on the machine where System Center Service Manager instance is running.</span><span class="sxs-lookup"><span data-stu-id="b65ce-212">In the **Hybrid Connections** blade, click **Download the Connection Manager** and install it on the machine where System Center Service Manager instance is running.</span></span>

    <span data-ttu-id="b65ce-213">Once the installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span><span class="sxs-lookup"><span data-stu-id="b65ce-213">Once the installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span></span>

2. <span data-ttu-id="b65ce-214">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="b65ce-214">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span></span>

3. <span data-ttu-id="b65ce-215">Login with your Azure credentials and select your subscription where the Hybrid connection was created.</span><span class="sxs-lookup"><span data-stu-id="b65ce-215">Login with your Azure credentials and select your subscription where the Hybrid connection was created.</span></span>

4. <span data-ttu-id="b65ce-216">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-216">Click **Save**.</span></span>

<span data-ttu-id="b65ce-217">Your hybrid connection is successfully connected.</span><span class="sxs-lookup"><span data-stu-id="b65ce-217">Your hybrid connection is successfully connected.</span></span>

![successful hybrid connection](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> <span data-ttu-id="b65ce-219">After the hybrid connection is created, verify and test the connection by visiting the deployed Service Manager Web app.</span><span class="sxs-lookup"><span data-stu-id="b65ce-219">After the hybrid connection is created, verify and test the connection by visiting the deployed Service Manager Web app.</span></span> <span data-ttu-id="b65ce-220">Ensure the connection is successful before you try to connect to ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-220">Ensure the connection is successful before you try to connect to ITSMC in Azure.</span></span>

<span data-ttu-id="b65ce-221">The following sample image shows the details of a successful connection:</span><span class="sxs-lookup"><span data-stu-id="b65ce-221">The following sample image shows the details of a successful connection:</span></span>

![Hybrid connection test](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-to-it-service-management-connector-in-azure"></a><span data-ttu-id="b65ce-223">Connect ServiceNow to IT Service Management Connector in Azure</span><span class="sxs-lookup"><span data-stu-id="b65ce-223">Connect ServiceNow to IT Service Management Connector in Azure</span></span>

<span data-ttu-id="b65ce-224">The following sections provide details about how to connect your ServiceNow product to ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-224">The following sections provide details about how to connect your ServiceNow product to ITSMC in Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b65ce-225">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b65ce-225">Prerequisites</span></span>
<span data-ttu-id="b65ce-226">Ensure the following prerequisites are met:</span><span class="sxs-lookup"><span data-stu-id="b65ce-226">Ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="b65ce-227">ITSMC installed.</span><span class="sxs-lookup"><span data-stu-id="b65ce-227">ITSMC installed.</span></span> <span data-ttu-id="b65ce-228">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span><span class="sxs-lookup"><span data-stu-id="b65ce-228">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span></span>
- <span data-ttu-id="b65ce-229">ServiceNow supported versions: Kingston, Jakarta, Istanbul, Helsinki, Geneva.</span><span class="sxs-lookup"><span data-stu-id="b65ce-229">ServiceNow supported versions: Kingston, Jakarta, Istanbul, Helsinki, Geneva.</span></span>

<span data-ttu-id="b65ce-230">**ServiceNow Admins must do the following in their ServiceNow instance**:</span><span class="sxs-lookup"><span data-stu-id="b65ce-230">**ServiceNow Admins must do the following in their ServiceNow instance**:</span></span>
- <span data-ttu-id="b65ce-231">Generate client ID and client secret for the ServiceNow product.</span><span class="sxs-lookup"><span data-stu-id="b65ce-231">Generate client ID and client secret for the ServiceNow product.</span></span> <span data-ttu-id="b65ce-232">For information on how to generate client ID and secret, see the following information as required:</span><span class="sxs-lookup"><span data-stu-id="b65ce-232">For information on how to generate client ID and secret, see the following information as required:</span></span>

    - [<span data-ttu-id="b65ce-233">Set up OAuth for Kingston</span><span class="sxs-lookup"><span data-stu-id="b65ce-233">Set up OAuth for Kingston</span></span>](https://docs.servicenow.com/bundle/kingston-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [<span data-ttu-id="b65ce-234">Set up OAuth for Jakarta</span><span class="sxs-lookup"><span data-stu-id="b65ce-234">Set up OAuth for Jakarta</span></span>](https://docs.servicenow.com/bundle/jakarta-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [<span data-ttu-id="b65ce-235">Set up OAuth for Istanbul</span><span class="sxs-lookup"><span data-stu-id="b65ce-235">Set up OAuth for Istanbul</span></span>](https://docs.servicenow.com/bundle/istanbul-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [<span data-ttu-id="b65ce-236">Set up OAuth for Helsinki</span><span class="sxs-lookup"><span data-stu-id="b65ce-236">Set up OAuth for Helsinki</span></span>](https://docs.servicenow.com/bundle/helsinki-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [<span data-ttu-id="b65ce-237">Set up OAuth for Geneva</span><span class="sxs-lookup"><span data-stu-id="b65ce-237">Set up OAuth for Geneva</span></span>](https://docs.servicenow.com/bundle/geneva-servicenow-platform/page/administer/security/task/t_SettingUpOAuth.html)


- <span data-ttu-id="b65ce-238">Install the User App for Microsoft OMS integration (ServiceNow app).</span><span class="sxs-lookup"><span data-stu-id="b65ce-238">Install the User App for Microsoft OMS integration (ServiceNow app).</span></span> <span data-ttu-id="b65ce-239">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.1 ).</span><span class="sxs-lookup"><span data-stu-id="b65ce-239">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.1 ).</span></span>
- <span data-ttu-id="b65ce-240">Create integration user role for the user app installed.</span><span class="sxs-lookup"><span data-stu-id="b65ce-240">Create integration user role for the user app installed.</span></span> <span data-ttu-id="b65ce-241">Information on how to create the integration user role is [here](#create-integration-user-role-in-servicenow-app).</span><span class="sxs-lookup"><span data-stu-id="b65ce-241">Information on how to create the integration user role is [here](#create-integration-user-role-in-servicenow-app).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="b65ce-242">**Connection procedure**</span><span class="sxs-lookup"><span data-stu-id="b65ce-242">**Connection procedure**</span></span>
<span data-ttu-id="b65ce-243">Use the following procedure to create a ServiceNow connection:</span><span class="sxs-lookup"><span data-stu-id="b65ce-243">Use the following procedure to create a ServiceNow connection:</span></span>


1. <span data-ttu-id="b65ce-244">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span><span class="sxs-lookup"><span data-stu-id="b65ce-244">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span></span>

2.  <span data-ttu-id="b65ce-245">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-245">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span></span>
    <span data-ttu-id="b65ce-246">![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)</span><span class="sxs-lookup"><span data-stu-id="b65ce-246">![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)</span></span>

3. <span data-ttu-id="b65ce-247">At the top of the right pane, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-247">At the top of the right pane, click **Add**.</span></span>

4. <span data-ttu-id="b65ce-248">Provide the information as described in the following table, and click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-248">Provide the information as described in the following table, and click **OK** to create the connection.</span></span>


> [!NOTE]
> <span data-ttu-id="b65ce-249">All these parameters are mandatory.</span><span class="sxs-lookup"><span data-stu-id="b65ce-249">All these parameters are mandatory.</span></span>

| <span data-ttu-id="b65ce-250">**Field**</span><span class="sxs-lookup"><span data-stu-id="b65ce-250">**Field**</span></span> | <span data-ttu-id="b65ce-251">**Description**</span><span class="sxs-lookup"><span data-stu-id="b65ce-251">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b65ce-252">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="b65ce-252">**Connection Name**</span></span>   | <span data-ttu-id="b65ce-253">Type a name for the ServiceNow instance that you want to connect with ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-253">Type a name for the ServiceNow instance that you want to connect with ITSMC.</span></span>  <span data-ttu-id="b65ce-254">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-254">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="b65ce-255">**Partner type**</span><span class="sxs-lookup"><span data-stu-id="b65ce-255">**Partner type**</span></span>   | <span data-ttu-id="b65ce-256">Select **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-256">Select **ServiceNow**.</span></span> |
| <span data-ttu-id="b65ce-257">**Username**</span><span class="sxs-lookup"><span data-stu-id="b65ce-257">**Username**</span></span>   | <span data-ttu-id="b65ce-258">Type the integration user name that you created in the ServiceNow app to support the connection to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-258">Type the integration user name that you created in the ServiceNow app to support the connection to ITSMC.</span></span> <span data-ttu-id="b65ce-259">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span><span class="sxs-lookup"><span data-stu-id="b65ce-259">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span></span>|
| <span data-ttu-id="b65ce-260">**Password**</span><span class="sxs-lookup"><span data-stu-id="b65ce-260">**Password**</span></span>   | <span data-ttu-id="b65ce-261">Type the password associated with this user name.</span><span class="sxs-lookup"><span data-stu-id="b65ce-261">Type the password associated with this user name.</span></span> <span data-ttu-id="b65ce-262">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within the ITSMC service.</span><span class="sxs-lookup"><span data-stu-id="b65ce-262">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within the ITSMC service.</span></span>  |
| <span data-ttu-id="b65ce-263">**Server URL**</span><span class="sxs-lookup"><span data-stu-id="b65ce-263">**Server URL**</span></span>   | <span data-ttu-id="b65ce-264">Type the URL of the ServiceNow instance that you want to connect to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-264">Type the URL of the ServiceNow instance that you want to connect to ITSMC.</span></span> |
| <span data-ttu-id="b65ce-265">**Client ID**</span><span class="sxs-lookup"><span data-stu-id="b65ce-265">**Client ID**</span></span>   | <span data-ttu-id="b65ce-266">Type the client ID that you want to use for OAuth2 Authentication, which you generated earlier.</span><span class="sxs-lookup"><span data-stu-id="b65ce-266">Type the client ID that you want to use for OAuth2 Authentication, which you generated earlier.</span></span>  <span data-ttu-id="b65ce-267">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span><span class="sxs-lookup"><span data-stu-id="b65ce-267">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span> |
| <span data-ttu-id="b65ce-268">**Client Secret**</span><span class="sxs-lookup"><span data-stu-id="b65ce-268">**Client Secret**</span></span>   | <span data-ttu-id="b65ce-269">Type the client secret, generated for this ID.</span><span class="sxs-lookup"><span data-stu-id="b65ce-269">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="b65ce-270">**Data Sync Scope**</span><span class="sxs-lookup"><span data-stu-id="b65ce-270">**Data Sync Scope**</span></span>   | <span data-ttu-id="b65ce-271">Select the ServiceNow work items that you want to sync to Azure Log Analytics, through the ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-271">Select the ServiceNow work items that you want to sync to Azure Log Analytics, through the ITSMC.</span></span>  <span data-ttu-id="b65ce-272">The selected values are imported into log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-272">The selected values are imported into log analytics.</span></span>   <span data-ttu-id="b65ce-273">**Options:**  Incidents and Change Requests.</span><span class="sxs-lookup"><span data-stu-id="b65ce-273">**Options:**  Incidents and Change Requests.</span></span>|
| <span data-ttu-id="b65ce-274">**Sync Data**</span><span class="sxs-lookup"><span data-stu-id="b65ce-274">**Sync Data**</span></span> | <span data-ttu-id="b65ce-275">Type the number of past days that you want the data from.</span><span class="sxs-lookup"><span data-stu-id="b65ce-275">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="b65ce-276">**Maximum limit**: 120 days.</span><span class="sxs-lookup"><span data-stu-id="b65ce-276">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="b65ce-277">**Create new configuration item in ITSM solution**</span><span class="sxs-lookup"><span data-stu-id="b65ce-277">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="b65ce-278">Select this option if you want to create the configuration items in the ITSM product.</span><span class="sxs-lookup"><span data-stu-id="b65ce-278">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="b65ce-279">When selected, ITSMC creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span><span class="sxs-lookup"><span data-stu-id="b65ce-279">When selected, ITSMC creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="b65ce-280">**Default**: disabled.</span><span class="sxs-lookup"><span data-stu-id="b65ce-280">**Default**: disabled.</span></span> |

![ServiceNow connection](./media/log-analytics-itsmc/itsm-connection-servicenow-connection-latest.png)

<span data-ttu-id="b65ce-282">**When successfully connected, and synced**:</span><span class="sxs-lookup"><span data-stu-id="b65ce-282">**When successfully connected, and synced**:</span></span>

- <span data-ttu-id="b65ce-283">Selected work items from ServiceNow instance are imported into Azure **Log Analytics.**</span><span class="sxs-lookup"><span data-stu-id="b65ce-283">Selected work items from ServiceNow instance are imported into Azure **Log Analytics.**</span></span> <span data-ttu-id="b65ce-284">You can view the summary of these work items on the IT Service Management Connector tile.</span><span class="sxs-lookup"><span data-stu-id="b65ce-284">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="b65ce-285">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this ServiceNow instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-285">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this ServiceNow instance.</span></span>

<span data-ttu-id="b65ce-286">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="b65ce-286">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span></span>

### <a name="create-integration-user-role-in-servicenow-app"></a><span data-ttu-id="b65ce-287">Create integration user role in ServiceNow app</span><span class="sxs-lookup"><span data-stu-id="b65ce-287">Create integration user role in ServiceNow app</span></span>

<span data-ttu-id="b65ce-288">User the following procedure:</span><span class="sxs-lookup"><span data-stu-id="b65ce-288">User the following procedure:</span></span>

1.  <span data-ttu-id="b65ce-289">Visit the [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.1) and install the **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-289">Visit the [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.1) and install the **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span></span>
2.  <span data-ttu-id="b65ce-290">After installation, visit the left navigation bar of the ServiceNow instance, search, and select Microsoft OMS integrator.</span><span class="sxs-lookup"><span data-stu-id="b65ce-290">After installation, visit the left navigation bar of the ServiceNow instance, search, and select Microsoft OMS integrator.</span></span>  
3.  <span data-ttu-id="b65ce-291">Click **Installation Checklist**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-291">Click **Installation Checklist**.</span></span>

    <span data-ttu-id="b65ce-292">The status is displayed as  **Not complete** if the user role is yet to be created.</span><span class="sxs-lookup"><span data-stu-id="b65ce-292">The status is displayed as  **Not complete** if the user role is yet to be created.</span></span>

4.  <span data-ttu-id="b65ce-293">In the text boxes, next to **Create integration user**, enter the user name for the user that can connect to ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-293">In the text boxes, next to **Create integration user**, enter the user name for the user that can connect to ITSMC in Azure.</span></span>
5.  <span data-ttu-id="b65ce-294">Enter the password for this user, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-294">Enter the password for this user, and click **OK**.</span></span>  

>[!NOTE]

> <span data-ttu-id="b65ce-295">You use these credentials to make the ServiceNow connection in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-295">You use these credentials to make the ServiceNow connection in Azure.</span></span>

<span data-ttu-id="b65ce-296">The newly created user is displayed with the default roles assigned.</span><span class="sxs-lookup"><span data-stu-id="b65ce-296">The newly created user is displayed with the default roles assigned.</span></span>

<span data-ttu-id="b65ce-297">**Default roles**:</span><span class="sxs-lookup"><span data-stu-id="b65ce-297">**Default roles**:</span></span>
- <span data-ttu-id="b65ce-298">personalize_choices</span><span class="sxs-lookup"><span data-stu-id="b65ce-298">personalize_choices</span></span>
- <span data-ttu-id="b65ce-299">import_transformer</span><span class="sxs-lookup"><span data-stu-id="b65ce-299">import_transformer</span></span>
-   <span data-ttu-id="b65ce-300">x_mioms_microsoft.user</span><span class="sxs-lookup"><span data-stu-id="b65ce-300">x_mioms_microsoft.user</span></span>
-   <span data-ttu-id="b65ce-301">itil</span><span class="sxs-lookup"><span data-stu-id="b65ce-301">itil</span></span>
-   <span data-ttu-id="b65ce-302">template_editor</span><span class="sxs-lookup"><span data-stu-id="b65ce-302">template_editor</span></span>
-   <span data-ttu-id="b65ce-303">view_changer</span><span class="sxs-lookup"><span data-stu-id="b65ce-303">view_changer</span></span>

<span data-ttu-id="b65ce-304">Once the user is successfully created, the status of **Check Installation Checklist** moves to Completed, listing the details of the user role created for the app.</span><span class="sxs-lookup"><span data-stu-id="b65ce-304">Once the user is successfully created, the status of **Check Installation Checklist** moves to Completed, listing the details of the user role created for the app.</span></span>

> [!NOTE]

> <span data-ttu-id="b65ce-305">ITSM Connector can send incidents to ServiceNow without any other modules installed on your ServiceNow instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-305">ITSM Connector can send incidents to ServiceNow without any other modules installed on your ServiceNow instance.</span></span> <span data-ttu-id="b65ce-306">If you are using EventManagement module in your ServiceNow instance and wish to create Events or Alerts in ServiceNow using the connector, add the following roles to the integration user:</span><span class="sxs-lookup"><span data-stu-id="b65ce-306">If you are using EventManagement module in your ServiceNow instance and wish to create Events or Alerts in ServiceNow using the connector, add the following roles to the integration user:</span></span>

>    - <span data-ttu-id="b65ce-307">evt_mgmt_integration</span><span class="sxs-lookup"><span data-stu-id="b65ce-307">evt_mgmt_integration</span></span>
>    - <span data-ttu-id="b65ce-308">evt_mgmt_operator</span><span class="sxs-lookup"><span data-stu-id="b65ce-308">evt_mgmt_operator</span></span>  


## <a name="connect-provance-to-it-service-management-connector-in-azure"></a><span data-ttu-id="b65ce-309">Connect Provance to IT Service Management Connector in Azure</span><span class="sxs-lookup"><span data-stu-id="b65ce-309">Connect Provance to IT Service Management Connector in Azure</span></span>

<span data-ttu-id="b65ce-310">The following sections provide details about how to connect your Provance product to ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-310">The following sections provide details about how to connect your Provance product to ITSMC in Azure.</span></span>


### <a name="prerequisites"></a><span data-ttu-id="b65ce-311">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b65ce-311">Prerequisites</span></span>

<span data-ttu-id="b65ce-312">Ensure the following prerequisites are met:</span><span class="sxs-lookup"><span data-stu-id="b65ce-312">Ensure the following prerequisites are met:</span></span>


- <span data-ttu-id="b65ce-313">ITSMC installed.</span><span class="sxs-lookup"><span data-stu-id="b65ce-313">ITSMC installed.</span></span> <span data-ttu-id="b65ce-314">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span><span class="sxs-lookup"><span data-stu-id="b65ce-314">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span></span>
- <span data-ttu-id="b65ce-315">Provance App should be registered with Azure AD - and client ID is made available.</span><span class="sxs-lookup"><span data-stu-id="b65ce-315">Provance App should be registered with Azure AD - and client ID is made available.</span></span> <span data-ttu-id="b65ce-316">For detailed information, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b65ce-316">For detailed information, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

- <span data-ttu-id="b65ce-317">User role:  Administrator.</span><span class="sxs-lookup"><span data-stu-id="b65ce-317">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="b65ce-318">Connection Procedure</span><span class="sxs-lookup"><span data-stu-id="b65ce-318">Connection Procedure</span></span>

<span data-ttu-id="b65ce-319">Use the following procedure to create a Provance connection:</span><span class="sxs-lookup"><span data-stu-id="b65ce-319">Use the following procedure to create a Provance connection:</span></span>

1. <span data-ttu-id="b65ce-320">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span><span class="sxs-lookup"><span data-stu-id="b65ce-320">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span></span>

2.  <span data-ttu-id="b65ce-321">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-321">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span></span>
    <span data-ttu-id="b65ce-322">![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)</span><span class="sxs-lookup"><span data-stu-id="b65ce-322">![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)</span></span>

3. <span data-ttu-id="b65ce-323">At the top of the right pane, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-323">At the top of the right pane, click **Add**.</span></span>

4. <span data-ttu-id="b65ce-324">Provide the information as described in the following table, and click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-324">Provide the information as described in the following table, and click **OK** to create the connection.</span></span>

> [!NOTE]

> <span data-ttu-id="b65ce-325">All these parameters are mandatory.</span><span class="sxs-lookup"><span data-stu-id="b65ce-325">All these parameters are mandatory.</span></span>

| <span data-ttu-id="b65ce-326">**Field**</span><span class="sxs-lookup"><span data-stu-id="b65ce-326">**Field**</span></span> | <span data-ttu-id="b65ce-327">**Description**</span><span class="sxs-lookup"><span data-stu-id="b65ce-327">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b65ce-328">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="b65ce-328">**Connection Name**</span></span>   | <span data-ttu-id="b65ce-329">Type a name for the Provance instance that you want to connect with ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-329">Type a name for the Provance instance that you want to connect with ITSMC.</span></span>  <span data-ttu-id="b65ce-330">You use this name later when you configure work items in this ITSM/ view detailed log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-330">You use this name later when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="b65ce-331">**Partner type**</span><span class="sxs-lookup"><span data-stu-id="b65ce-331">**Partner type**</span></span>   | <span data-ttu-id="b65ce-332">Select **Provance**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-332">Select **Provance**.</span></span> |
| <span data-ttu-id="b65ce-333">**Username**</span><span class="sxs-lookup"><span data-stu-id="b65ce-333">**Username**</span></span>   | <span data-ttu-id="b65ce-334">Type the user name that can connect to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-334">Type the user name that can connect to ITSMC.</span></span>    |
| <span data-ttu-id="b65ce-335">**Password**</span><span class="sxs-lookup"><span data-stu-id="b65ce-335">**Password**</span></span>   | <span data-ttu-id="b65ce-336">Type the password associated with this user name.</span><span class="sxs-lookup"><span data-stu-id="b65ce-336">Type the password associated with this user name.</span></span> <span data-ttu-id="b65ce-337">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the ITSMC service._</span><span class="sxs-lookup"><span data-stu-id="b65ce-337">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the ITSMC service._</span></span>|
| <span data-ttu-id="b65ce-338">**Server URL**</span><span class="sxs-lookup"><span data-stu-id="b65ce-338">**Server URL**</span></span>   | <span data-ttu-id="b65ce-339">Type the URL of your Provance instance that you want to connect to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-339">Type the URL of your Provance instance that you want to connect to ITSMC.</span></span> |
| <span data-ttu-id="b65ce-340">**Client ID**</span><span class="sxs-lookup"><span data-stu-id="b65ce-340">**Client ID**</span></span>   | <span data-ttu-id="b65ce-341">Type the client ID for authenticating this connection, which you generated in your Provance instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-341">Type the client ID for authenticating this connection, which you generated in your Provance instance.</span></span>  <span data-ttu-id="b65ce-342">More information on client ID, see [how to configure active directory authentication](../app-service/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b65ce-342">More information on client ID, see [how to configure active directory authentication](../app-service/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> |
| <span data-ttu-id="b65ce-343">**Data Sync Scope**</span><span class="sxs-lookup"><span data-stu-id="b65ce-343">**Data Sync Scope**</span></span>   | <span data-ttu-id="b65ce-344">Select the Provance work items that you want to sync to Azure Log Analytics, through ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-344">Select the Provance work items that you want to sync to Azure Log Analytics, through ITSMC.</span></span>  <span data-ttu-id="b65ce-345">These work items are imported into log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-345">These work items are imported into log analytics.</span></span>   <span data-ttu-id="b65ce-346">**Options:**   Incidents, Change Requests.</span><span class="sxs-lookup"><span data-stu-id="b65ce-346">**Options:**   Incidents, Change Requests.</span></span>|
| <span data-ttu-id="b65ce-347">**Sync Data**</span><span class="sxs-lookup"><span data-stu-id="b65ce-347">**Sync Data**</span></span> | <span data-ttu-id="b65ce-348">Type the number of past days that you want the data from.</span><span class="sxs-lookup"><span data-stu-id="b65ce-348">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="b65ce-349">**Maximum limit**: 120 days.</span><span class="sxs-lookup"><span data-stu-id="b65ce-349">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="b65ce-350">**Create new configuration item in ITSM solution**</span><span class="sxs-lookup"><span data-stu-id="b65ce-350">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="b65ce-351">Select this option if you want to create the configuration items in the ITSM product.</span><span class="sxs-lookup"><span data-stu-id="b65ce-351">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="b65ce-352">When selected, ITSMC creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span><span class="sxs-lookup"><span data-stu-id="b65ce-352">When selected, ITSMC creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="b65ce-353">**Default**: disabled.</span><span class="sxs-lookup"><span data-stu-id="b65ce-353">**Default**: disabled.</span></span>|

![Provance connection](./media/log-analytics-itsmc/itsm-connections-provance-latest.png)

<span data-ttu-id="b65ce-355">**When successfully connected, and synced**:</span><span class="sxs-lookup"><span data-stu-id="b65ce-355">**When successfully connected, and synced**:</span></span>

- <span data-ttu-id="b65ce-356">Selected work items from this Provance instance are imported into Azure **Log Analytics.**</span><span class="sxs-lookup"><span data-stu-id="b65ce-356">Selected work items from this Provance instance are imported into Azure **Log Analytics.**</span></span> <span data-ttu-id="b65ce-357">You can view the summary of these work items on the IT Service Management Connector tile.</span><span class="sxs-lookup"><span data-stu-id="b65ce-357">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="b65ce-358">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this Provance instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-358">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this Provance instance.</span></span>

<span data-ttu-id="b65ce-359">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="b65ce-359">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span></span>

## <a name="connect-cherwell-to-it-service-management-connector-in-azure"></a><span data-ttu-id="b65ce-360">Connect Cherwell to IT Service Management Connector in Azure</span><span class="sxs-lookup"><span data-stu-id="b65ce-360">Connect Cherwell to IT Service Management Connector in Azure</span></span>

<span data-ttu-id="b65ce-361">The following sections provide details about how to connect your Cherwell product to ITSMC in Azure.</span><span class="sxs-lookup"><span data-stu-id="b65ce-361">The following sections provide details about how to connect your Cherwell product to ITSMC in Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b65ce-362">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b65ce-362">Prerequisites</span></span>

<span data-ttu-id="b65ce-363">Ensure the following prerequisites are met:</span><span class="sxs-lookup"><span data-stu-id="b65ce-363">Ensure the following prerequisites are met:</span></span>

- <span data-ttu-id="b65ce-364">ITSMC installed.</span><span class="sxs-lookup"><span data-stu-id="b65ce-364">ITSMC installed.</span></span> <span data-ttu-id="b65ce-365">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span><span class="sxs-lookup"><span data-stu-id="b65ce-365">More information: [Adding the IT Service Management Connector Solution](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).</span></span>
- <span data-ttu-id="b65ce-366">Client ID generated.</span><span class="sxs-lookup"><span data-stu-id="b65ce-366">Client ID generated.</span></span> <span data-ttu-id="b65ce-367">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span><span class="sxs-lookup"><span data-stu-id="b65ce-367">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span></span>
- <span data-ttu-id="b65ce-368">User role:  Administrator.</span><span class="sxs-lookup"><span data-stu-id="b65ce-368">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="b65ce-369">Connection Procedure</span><span class="sxs-lookup"><span data-stu-id="b65ce-369">Connection Procedure</span></span>

<span data-ttu-id="b65ce-370">Use the following procedure to create a Provance connection:</span><span class="sxs-lookup"><span data-stu-id="b65ce-370">Use the following procedure to create a Provance connection:</span></span>

1. <span data-ttu-id="b65ce-371">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span><span class="sxs-lookup"><span data-stu-id="b65ce-371">In Azure portal, go to **All Resources** and look for **ServiceDesk(YourWorkspaceName)**</span></span>

2.  <span data-ttu-id="b65ce-372">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-372">Under **WORKSPACE DATA SOURCES** click **ITSM Connections**.</span></span>
    <span data-ttu-id="b65ce-373">![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)</span><span class="sxs-lookup"><span data-stu-id="b65ce-373">![New connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)</span></span>

3. <span data-ttu-id="b65ce-374">At the top of the right pane, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-374">At the top of the right pane, click **Add**.</span></span>

4. <span data-ttu-id="b65ce-375">Provide the information as described in the following table, and click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="b65ce-375">Provide the information as described in the following table, and click **OK** to create the connection.</span></span>

> [!NOTE]

> <span data-ttu-id="b65ce-376">All these parameters are mandatory.</span><span class="sxs-lookup"><span data-stu-id="b65ce-376">All these parameters are mandatory.</span></span>

| <span data-ttu-id="b65ce-377">**Field**</span><span class="sxs-lookup"><span data-stu-id="b65ce-377">**Field**</span></span> | <span data-ttu-id="b65ce-378">**Description**</span><span class="sxs-lookup"><span data-stu-id="b65ce-378">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b65ce-379">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="b65ce-379">**Connection Name**</span></span>   | <span data-ttu-id="b65ce-380">Type a name for the Cherwell instance that you want to connect to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-380">Type a name for the Cherwell instance that you want to connect to ITSMC.</span></span>  <span data-ttu-id="b65ce-381">You use this name later when you configure work items in this ITSM/ view detailed log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-381">You use this name later when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="b65ce-382">**Partner type**</span><span class="sxs-lookup"><span data-stu-id="b65ce-382">**Partner type**</span></span>   | <span data-ttu-id="b65ce-383">Select **Cherwell.**</span><span class="sxs-lookup"><span data-stu-id="b65ce-383">Select **Cherwell.**</span></span> |
| <span data-ttu-id="b65ce-384">**Username**</span><span class="sxs-lookup"><span data-stu-id="b65ce-384">**Username**</span></span>   | <span data-ttu-id="b65ce-385">Type the Cherwell user name that can connect to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-385">Type the Cherwell user name that can connect to ITSMC.</span></span> |
| <span data-ttu-id="b65ce-386">**Password**</span><span class="sxs-lookup"><span data-stu-id="b65ce-386">**Password**</span></span>   | <span data-ttu-id="b65ce-387">Type the password associated with this user name.</span><span class="sxs-lookup"><span data-stu-id="b65ce-387">Type the password associated with this user name.</span></span> <span data-ttu-id="b65ce-388">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the ITSMC service.</span><span class="sxs-lookup"><span data-stu-id="b65ce-388">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the ITSMC service.</span></span>|
| <span data-ttu-id="b65ce-389">**Server URL**</span><span class="sxs-lookup"><span data-stu-id="b65ce-389">**Server URL**</span></span>   | <span data-ttu-id="b65ce-390">Type the URL of your Cherwell instance that you want to connect to ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-390">Type the URL of your Cherwell instance that you want to connect to ITSMC.</span></span> |
| <span data-ttu-id="b65ce-391">**Client ID**</span><span class="sxs-lookup"><span data-stu-id="b65ce-391">**Client ID**</span></span>   | <span data-ttu-id="b65ce-392">Type the client ID for authenticating this connection, which you generated in your Cherwell instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-392">Type the client ID for authenticating this connection, which you generated in your Cherwell instance.</span></span>   |
| <span data-ttu-id="b65ce-393">**Data Sync Scope**</span><span class="sxs-lookup"><span data-stu-id="b65ce-393">**Data Sync Scope**</span></span>   | <span data-ttu-id="b65ce-394">Select the Cherwell work items that you want to sync through ITSMC.</span><span class="sxs-lookup"><span data-stu-id="b65ce-394">Select the Cherwell work items that you want to sync through ITSMC.</span></span>  <span data-ttu-id="b65ce-395">These work items are imported into log analytics.</span><span class="sxs-lookup"><span data-stu-id="b65ce-395">These work items are imported into log analytics.</span></span>   <span data-ttu-id="b65ce-396">**Options:**  Incidents, Change Requests.</span><span class="sxs-lookup"><span data-stu-id="b65ce-396">**Options:**  Incidents, Change Requests.</span></span> |
| <span data-ttu-id="b65ce-397">**Sync Data**</span><span class="sxs-lookup"><span data-stu-id="b65ce-397">**Sync Data**</span></span> | <span data-ttu-id="b65ce-398">Type the number of past days that you want the data from.</span><span class="sxs-lookup"><span data-stu-id="b65ce-398">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="b65ce-399">**Maximum limit**: 120 days.</span><span class="sxs-lookup"><span data-stu-id="b65ce-399">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="b65ce-400">**Create new configuration item in ITSM solution**</span><span class="sxs-lookup"><span data-stu-id="b65ce-400">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="b65ce-401">Select this option if you want to create the configuration items in the ITSM product.</span><span class="sxs-lookup"><span data-stu-id="b65ce-401">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="b65ce-402">When selected, ITSMC creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span><span class="sxs-lookup"><span data-stu-id="b65ce-402">When selected, ITSMC creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="b65ce-403">**Default**: disabled.</span><span class="sxs-lookup"><span data-stu-id="b65ce-403">**Default**: disabled.</span></span> |


![Provance connection](./media/log-analytics-itsmc/itsm-connections-cherwell-latest.png)

<span data-ttu-id="b65ce-405">**When successfully connected, and synced**:</span><span class="sxs-lookup"><span data-stu-id="b65ce-405">**When successfully connected, and synced**:</span></span>

- <span data-ttu-id="b65ce-406">Selected work items from this Cherwell instance are imported into Azure **Log Analytics.**</span><span class="sxs-lookup"><span data-stu-id="b65ce-406">Selected work items from this Cherwell instance are imported into Azure **Log Analytics.**</span></span> <span data-ttu-id="b65ce-407">You can view the summary of these work items on the IT Service Management Connector tile.</span><span class="sxs-lookup"><span data-stu-id="b65ce-407">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="b65ce-408">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this Cherwell instance.</span><span class="sxs-lookup"><span data-stu-id="b65ce-408">You can create incidents from Log Analytics alerts or from log records, or from Azure alerts in this Cherwell instance.</span></span>

<span data-ttu-id="b65ce-409">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="b65ce-409">Learn more: [Create ITSM work items from Azure alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).</span></span>

### <a name="generate-client-id-for-cherwell"></a><span data-ttu-id="b65ce-410">Generate client ID for Cherwell</span><span class="sxs-lookup"><span data-stu-id="b65ce-410">Generate client ID for Cherwell</span></span>

<span data-ttu-id="b65ce-411">To generate the client ID/key for Cherwell, use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="b65ce-411">To generate the client ID/key for Cherwell, use the following procedure:</span></span>

1. <span data-ttu-id="b65ce-412">Log in to your Cherwell instance as admin.</span><span class="sxs-lookup"><span data-stu-id="b65ce-412">Log in to your Cherwell instance as admin.</span></span>
2. <span data-ttu-id="b65ce-413">Click **Security** > **Edit REST API client settings**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-413">Click **Security** > **Edit REST API client settings**.</span></span>
3. <span data-ttu-id="b65ce-414">Select **Create new client** > **client secret**.</span><span class="sxs-lookup"><span data-stu-id="b65ce-414">Select **Create new client** > **client secret**.</span></span>

    ![Cherwell user id](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a><span data-ttu-id="b65ce-416">Next steps</span><span class="sxs-lookup"><span data-stu-id="b65ce-416">Next steps</span></span>
 - [<span data-ttu-id="b65ce-417">Create ITSM work items from Azure alerts</span><span class="sxs-lookup"><span data-stu-id="b65ce-417">Create ITSM work items from Azure alerts</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts)
