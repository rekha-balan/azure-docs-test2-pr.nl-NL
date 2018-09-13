---
title: Service Map integration with System Center Operations Manager | Microsoft Docs
description: Service Map is a solution in Azure that automatically discovers application components on Windows and Linux systems and maps the communication between services. This article discusses using Service Map to automatically create distributed application diagrams in Operations Manager.
services: monitoring
documentationcenter: ''
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: 5aca1400ddfe1522cd9dc8d68d8cba8a222e4d21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867217"
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="6eeef-104">Service Map integration with System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="6eeef-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="6eeef-105">This feature is in public preview.</span><span class="sxs-lookup"><span data-stu-id="6eeef-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="6eeef-106">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span><span class="sxs-lookup"><span data-stu-id="6eeef-106">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="6eeef-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span><span class="sxs-lookup"><span data-stu-id="6eeef-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="6eeef-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span><span class="sxs-lookup"><span data-stu-id="6eeef-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="6eeef-109">For more information, see the [Service Map documentation]( monitoring-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="6eeef-109">For more information, see the [Service Map documentation]( monitoring-service-map.md).</span></span>

<span data-ttu-id="6eeef-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eeef-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6eeef-111">Prerequisites</span></span>
* <span data-ttu-id="6eeef-112">An Operations Manager management group (2012 R2 or later) that is managing a set of servers.</span><span class="sxs-lookup"><span data-stu-id="6eeef-112">An Operations Manager management group (2012 R2 or later) that is managing a set of servers.</span></span>
* <span data-ttu-id="6eeef-113">A Log Analytics workspace with the Service Map solution enabled.</span><span class="sxs-lookup"><span data-stu-id="6eeef-113">A Log Analytics workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="6eeef-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="6eeef-115">Windows and Linux servers are supported.</span><span class="sxs-lookup"><span data-stu-id="6eeef-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="6eeef-116">A service principal with access to the Azure subscription that is associated with the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="6eeef-116">A service principal with access to the Azure subscription that is associated with the Log Analytics workspace.</span></span> <span data-ttu-id="6eeef-117">For more information, go to [Create a service principal](#create-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="6eeef-117">For more information, go to [Create a service principal](#create-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="6eeef-118">Install the Service Map management pack</span><span class="sxs-lookup"><span data-stu-id="6eeef-118">Install the Service Map management pack</span></span>
<span data-ttu-id="6eeef-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="6eeef-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="6eeef-120">You can download the management pack bundle from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55763).</span><span class="sxs-lookup"><span data-stu-id="6eeef-120">You can download the management pack bundle from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55763).</span></span> <span data-ttu-id="6eeef-121">The bundle contains the following management packs:</span><span class="sxs-lookup"><span data-stu-id="6eeef-121">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="6eeef-122">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="6eeef-122">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="6eeef-123">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="6eeef-123">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="6eeef-124">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="6eeef-124">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="6eeef-125">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="6eeef-125">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="6eeef-126">Configure the Service Map integration</span><span class="sxs-lookup"><span data-stu-id="6eeef-126">Configure the Service Map integration</span></span>
<span data-ttu-id="6eeef-127">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span><span class="sxs-lookup"><span data-stu-id="6eeef-127">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="6eeef-128">To configure Service Map integration, do the following:</span><span class="sxs-lookup"><span data-stu-id="6eeef-128">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="6eeef-129">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span><span class="sxs-lookup"><span data-stu-id="6eeef-129">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Service Map Overview pane](media/monitoring-service-map/scom-configuration.png)

2. <span data-ttu-id="6eeef-131">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6eeef-131">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="6eeef-132">For more information, go to [Create a service principal](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="6eeef-132">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![The Connection Configuration window](media/monitoring-service-map/scom-config-spn.png)

3. <span data-ttu-id="6eeef-134">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Log Analytics workspace), and Log Analytics workspace, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6eeef-134">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Log Analytics workspace), and Log Analytics workspace, and then click **Next**.</span></span>

    ![The Operations Manager Configuration Workspace](media/monitoring-service-map/scom-config-workspace.png)

4. <span data-ttu-id="6eeef-136">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="6eeef-136">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="6eeef-137">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="6eeef-137">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="6eeef-138">When you are finished selecting groups, click **Ok** to finish.</span><span class="sxs-lookup"><span data-stu-id="6eeef-138">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![The Operations Manager Configuration Machine Groups](media/monitoring-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="6eeef-140">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-140">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="6eeef-141">Click **Add/Remove Servers**.</span><span class="sxs-lookup"><span data-stu-id="6eeef-141">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="6eeef-142">For the integration to build a distributed application diagram for a server, the server must be:</span><span class="sxs-lookup"><span data-stu-id="6eeef-142">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="6eeef-143">Managed by Operations Manager</span><span class="sxs-lookup"><span data-stu-id="6eeef-143">Managed by Operations Manager</span></span>
    * <span data-ttu-id="6eeef-144">Managed by Service Map</span><span class="sxs-lookup"><span data-stu-id="6eeef-144">Managed by Service Map</span></span>
    * <span data-ttu-id="6eeef-145">Listed in the Service Map Servers Group</span><span class="sxs-lookup"><span data-stu-id="6eeef-145">Listed in the Service Map Servers Group</span></span>

    ![The Operations Manager Configuration Group](media/monitoring-service-map/scom-config-group.png)

6. <span data-ttu-id="6eeef-147">Optional: Select the Management Server resource pool to communicate with Log Analytics, and then click **Add Workspace**.</span><span class="sxs-lookup"><span data-stu-id="6eeef-147">Optional: Select the Management Server resource pool to communicate with Log Analytics, and then click **Add Workspace**.</span></span>

    ![The Operations Manager Configuration Resource Pool](media/monitoring-service-map/scom-config-pool.png)

    <span data-ttu-id="6eeef-149">It might take a minute to configure and register the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="6eeef-149">It might take a minute to configure and register the Log Analytics workspace.</span></span> <span data-ttu-id="6eeef-150">After it is configured, Operations Manager initiates the first Service Map sync.</span><span class="sxs-lookup"><span data-stu-id="6eeef-150">After it is configured, Operations Manager initiates the first Service Map sync.</span></span>

    ![The Operations Manager Configuration Resource Pool](media/monitoring-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="6eeef-152">Monitor Service Map</span><span class="sxs-lookup"><span data-stu-id="6eeef-152">Monitor Service Map</span></span>
<span data-ttu-id="6eeef-153">After the Log Analytics workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span><span class="sxs-lookup"><span data-stu-id="6eeef-153">After the Log Analytics workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![The Operations Manager Monitoring pane](media/monitoring-service-map/scom-monitoring.png)

<span data-ttu-id="6eeef-155">The Service Map folder has four nodes:</span><span class="sxs-lookup"><span data-stu-id="6eeef-155">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="6eeef-156">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-156">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="6eeef-157">Note that these alerts are not Log Analytics alerts being synced to Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="6eeef-157">Note that these alerts are not Log Analytics alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="6eeef-158">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-158">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![The Operations Manager Monitoring Servers pane](media/monitoring-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="6eeef-160">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-160">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="6eeef-161">You can click any group to view its distributed application diagram.</span><span class="sxs-lookup"><span data-stu-id="6eeef-161">You can click any group to view its distributed application diagram.</span></span>

    ![The Operations Manager distributed application diagram](media/monitoring-service-map/scom-group-dad.png)

* <span data-ttu-id="6eeef-163">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-163">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="6eeef-164">You can click any server to view its distributed application diagram.</span><span class="sxs-lookup"><span data-stu-id="6eeef-164">You can click any server to view its distributed application diagram.</span></span>

    ![The Operations Manager distributed application diagram](media/monitoring-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="6eeef-166">Edit or delete the workspace</span><span class="sxs-lookup"><span data-stu-id="6eeef-166">Edit or delete the workspace</span></span>
<span data-ttu-id="6eeef-167">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span><span class="sxs-lookup"><span data-stu-id="6eeef-167">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="6eeef-168">You can configure only one Log Analytics workspace for now.</span><span class="sxs-lookup"><span data-stu-id="6eeef-168">You can configure only one Log Analytics workspace for now.</span></span>

![The Operations Manager Edit Workspace pane](media/monitoring-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="6eeef-170">Configure rules and overrides</span><span class="sxs-lookup"><span data-stu-id="6eeef-170">Configure rules and overrides</span></span>
<span data-ttu-id="6eeef-171">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-171">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="6eeef-172">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="6eeef-172">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![The Operations Manager Overrides properties window](media/monitoring-service-map/scom-overrides.png)

* <span data-ttu-id="6eeef-174">**Enabled**: Enable or disable automatic updates.</span><span class="sxs-lookup"><span data-stu-id="6eeef-174">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="6eeef-175">**IntervalMinutes**: Reset the time between updates.</span><span class="sxs-lookup"><span data-stu-id="6eeef-175">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="6eeef-176">The default interval is one hour.</span><span class="sxs-lookup"><span data-stu-id="6eeef-176">The default interval is one hour.</span></span> <span data-ttu-id="6eeef-177">If you want to sync server maps more frequently, you can change the value.</span><span class="sxs-lookup"><span data-stu-id="6eeef-177">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="6eeef-178">**TimeoutSeconds**: Reset the length of time before the request times out.</span><span class="sxs-lookup"><span data-stu-id="6eeef-178">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="6eeef-179">**TimeWindowMinutes**: Reset the time window for querying data.</span><span class="sxs-lookup"><span data-stu-id="6eeef-179">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="6eeef-180">Default is a 60-minute window.</span><span class="sxs-lookup"><span data-stu-id="6eeef-180">Default is a 60-minute window.</span></span> <span data-ttu-id="6eeef-181">The maximum value allowed by Service Map is 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="6eeef-181">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="6eeef-182">Known issues and limitations</span><span class="sxs-lookup"><span data-stu-id="6eeef-182">Known issues and limitations</span></span>

<span data-ttu-id="6eeef-183">The current design presents the following issues and limitations:</span><span class="sxs-lookup"><span data-stu-id="6eeef-183">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="6eeef-184">You can only connect to a single Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="6eeef-184">You can only connect to a single Log Analytics workspace.</span></span>
* <span data-ttu-id="6eeef-185">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span><span class="sxs-lookup"><span data-stu-id="6eeef-185">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="6eeef-186">They will be synced from Service Map during the next sync cycle.</span><span class="sxs-lookup"><span data-stu-id="6eeef-186">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="6eeef-187">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span><span class="sxs-lookup"><span data-stu-id="6eeef-187">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="6eeef-188">Create a service principal</span><span class="sxs-lookup"><span data-stu-id="6eeef-188">Create a service principal</span></span>
<span data-ttu-id="6eeef-189">For official Azure documentation about creating a service principal, see:</span><span class="sxs-lookup"><span data-stu-id="6eeef-189">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="6eeef-190">Create a service principal by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6eeef-190">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="6eeef-191">Create a service principal by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6eeef-191">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="6eeef-192">Create a service principal by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6eeef-192">Create a service principal by using the Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="6eeef-193">Feedback</span><span class="sxs-lookup"><span data-stu-id="6eeef-193">Feedback</span></span>
<span data-ttu-id="6eeef-194">Do you have any feedback for us about Service Map or this documentation?</span><span class="sxs-lookup"><span data-stu-id="6eeef-194">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="6eeef-195">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span><span class="sxs-lookup"><span data-stu-id="6eeef-195">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
