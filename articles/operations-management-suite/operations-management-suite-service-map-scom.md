---
title: Service Map integration with System Center Operations Manager | Microsoft Docs
description: Service Map is an Operations Management Suite (OMS) solution that automatically discovers application components on Windows and Linux systems and maps the communication between services.  This article provides details for using Service Map to automatically create Distributed Application Diagrams in SCOM.
services: operations-management-suite
documentationcenter: ''
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: 5a8b2b77dfddf9a17a3675817948f426b43012ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555821"
---
# <a name="service-map-integration-with-system-center-operations-manager-integration"></a><span data-ttu-id="d09f3-104">Service Map integration with System Center Operations Manager Integration</span><span class="sxs-lookup"><span data-stu-id="d09f3-104">Service Map integration with System Center Operations Manager Integration</span></span>
  > [!NOTE]
  > <span data-ttu-id="d09f3-105">This feature is in private preview, so it should not be used on production systems.</span><span class="sxs-lookup"><span data-stu-id="d09f3-105">This feature is in private preview, so it should not be used on production systems.</span></span>
  > 
  
<span data-ttu-id="d09f3-106">Operations Management Suite (OMS) Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span><span class="sxs-lookup"><span data-stu-id="d09f3-106">Operations Management Suite (OMS) Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="d09f3-107">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span><span class="sxs-lookup"><span data-stu-id="d09f3-107">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="d09f3-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span><span class="sxs-lookup"><span data-stu-id="d09f3-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span>  <span data-ttu-id="d09f3-109">For more details, see the [Service Map Documentation](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="d09f3-109">For more details, see the [Service Map Documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="d09f3-110">With this integration between Service Map and System Center Operations Manager (SCOM), you can automatically create Distributed Application Diagrams in SCOM based on dynamic dependency maps in Service Map.</span><span class="sxs-lookup"><span data-stu-id="d09f3-110">With this integration between Service Map and System Center Operations Manager (SCOM), you can automatically create Distributed Application Diagrams in SCOM based on dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d09f3-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d09f3-111">Prerequisites</span></span>
1.  <span data-ttu-id="d09f3-112">A SCOM management group managing a set of servers.</span><span class="sxs-lookup"><span data-stu-id="d09f3-112">A SCOM management group managing a set of servers.</span></span>
2.  <span data-ttu-id="d09f3-113">An OMS Workspace with the Service Map solution enabled.</span><span class="sxs-lookup"><span data-stu-id="d09f3-113">An OMS Workspace with the Service Map solution enabled.</span></span>
3.  <span data-ttu-id="d09f3-114">A set of servers (at least one) that are both being managed by SCOM and sending data to Service Map.</span><span class="sxs-lookup"><span data-stu-id="d09f3-114">A set of servers (at least one) that are both being managed by SCOM and sending data to Service Map.</span></span>  <span data-ttu-id="d09f3-115">Windows and Linux servers are supported.</span><span class="sxs-lookup"><span data-stu-id="d09f3-115">Windows and Linux servers are supported.</span></span>
4.  <span data-ttu-id="d09f3-116">A Service Principal with access to the Azure Subscription that is associated with the OMS Workspace.</span><span class="sxs-lookup"><span data-stu-id="d09f3-116">A Service Principal with access to the Azure Subscription that is associated with the OMS Workspace.</span></span>  <span data-ttu-id="d09f3-117">[More information on creating a Service Principal](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="d09f3-117">[More information on creating a Service Principal](#creating-a-service-principal).</span></span>

## <a name="installing-service-map-management-pack"></a><span data-ttu-id="d09f3-118">Installing Service Map Management Pack</span><span class="sxs-lookup"><span data-stu-id="d09f3-118">Installing Service Map Management Pack</span></span>
<span data-ttu-id="d09f3-119">The integration between SCOM and Service Map is enabled by importing the Microsoft.SystemCenter.ServiceMap Management Pack Bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="d09f3-119">The integration between SCOM and Service Map is enabled by importing the Microsoft.SystemCenter.ServiceMap Management Pack Bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span>  <span data-ttu-id="d09f3-120">The bundle contains the following Management Packs:</span><span class="sxs-lookup"><span data-stu-id="d09f3-120">The bundle contains the following Management Packs:</span></span>
* <span data-ttu-id="d09f3-121">Microsoft ServiceMap Application Views</span><span class="sxs-lookup"><span data-stu-id="d09f3-121">Microsoft ServiceMap Application Views</span></span>
* <span data-ttu-id="d09f3-122">Microsoft System Center ServiceMap Internal</span><span class="sxs-lookup"><span data-stu-id="d09f3-122">Microsoft System Center ServiceMap Internal</span></span>
* <span data-ttu-id="d09f3-123">Microsoft System Center ServiceMap Overrides</span><span class="sxs-lookup"><span data-stu-id="d09f3-123">Microsoft System Center ServiceMap Overrides</span></span>
* <span data-ttu-id="d09f3-124">Microsoft System Center ServiceMap</span><span class="sxs-lookup"><span data-stu-id="d09f3-124">Microsoft System Center ServiceMap</span></span>

## <a name="configuring-the-service-map-integration"></a><span data-ttu-id="d09f3-125">Configuring the Service Map Integration</span><span class="sxs-lookup"><span data-stu-id="d09f3-125">Configuring the Service Map Integration</span></span>
1. <span data-ttu-id="d09f3-126">After installing the ServiceMap management pack, there will be a new node, Service Map, under the Operations Management Suite in the Administration pane.</span><span class="sxs-lookup"><span data-stu-id="d09f3-126">After installing the ServiceMap management pack, there will be a new node, Service Map, under the Operations Management Suite in the Administration pane.</span></span>
2. <span data-ttu-id="d09f3-127">Click “Add workspace” in the Service Map Overview pane to open the configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="d09f3-127">Click “Add workspace” in the Service Map Overview pane to open the configuration wizard.</span></span>

    ![SCOM Configuration Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-configuration.png)

3. <span data-ttu-id="d09f3-129">The first step in the wizard is Connection Configuration where you enter the information for your Azure Service Principal.</span><span class="sxs-lookup"><span data-stu-id="d09f3-129">The first step in the wizard is Connection Configuration where you enter the information for your Azure Service Principal.</span></span> <span data-ttu-id="d09f3-130">Enter the Tenant name or ID, Application ID (also known as Username or ClientID), and Password of the Service Principal.</span><span class="sxs-lookup"><span data-stu-id="d09f3-130">Enter the Tenant name or ID, Application ID (also known as Username or ClientID), and Password of the Service Principal.</span></span>  <span data-ttu-id="d09f3-131">[More information on creating a Service Principal](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="d09f3-131">[More information on creating a Service Principal](#creating-a-service-principal).</span></span>

    ![SCOM Config SPN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-config-spn.png)

4. <span data-ttu-id="d09f3-133">The next step is to select the Azure Subscription, Azure Resource Group (the one containing the OMS Workspace), and OMS Workspace.</span><span class="sxs-lookup"><span data-stu-id="d09f3-133">The next step is to select the Azure Subscription, Azure Resource Group (the one containing the OMS Workspace), and OMS Workspace.</span></span>

    ![SCOM Config Workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-config-workspace.png)

5. <span data-ttu-id="d09f3-135">The next step is to configure the Service Map Servers Group with the servers you would like to sync between SCOM and Service Map.</span><span class="sxs-lookup"><span data-stu-id="d09f3-135">The next step is to configure the Service Map Servers Group with the servers you would like to sync between SCOM and Service Map.</span></span>  <span data-ttu-id="d09f3-136">Click the Add/Remove Servers…</span><span class="sxs-lookup"><span data-stu-id="d09f3-136">Click the Add/Remove Servers…</span></span> <span data-ttu-id="d09f3-137">button.</span><span class="sxs-lookup"><span data-stu-id="d09f3-137">button.</span></span> <span data-ttu-id="d09f3-138">Note that for the integration to build a Distributed Application Diagram for a server, the server must: 1) be managed by SCOM, 2) be managed by Service Map, and 3) be listed in the Service Map Servers Group.</span><span class="sxs-lookup"><span data-stu-id="d09f3-138">Note that for the integration to build a Distributed Application Diagram for a server, the server must: 1) be managed by SCOM, 2) be managed by Service Map, and 3) be listed in the Service Map Servers Group.</span></span>

    ![SCOM Config Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="d09f3-140">Optional - Select the Management Server resource pool to communicate with OMS and click “Add Workspace”.</span><span class="sxs-lookup"><span data-stu-id="d09f3-140">Optional - Select the Management Server resource pool to communicate with OMS and click “Add Workspace”.</span></span>

    ![SCOM Config Resource Pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-config-pool.png)

7. <span data-ttu-id="d09f3-142">Please note that it will take a minute to configure and register the OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="d09f3-142">Please note that it will take a minute to configure and register the OMS workspace.</span></span> <span data-ttu-id="d09f3-143">Once this is configured, SCOM will initiate the first Service Map sync from OMS.</span><span class="sxs-lookup"><span data-stu-id="d09f3-143">Once this is configured, SCOM will initiate the first Service Map sync from OMS.</span></span>

    ![SCOM Config Resource Pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-config-success.png)

<span data-ttu-id="d09f3-145">**Note:** The default sync interval is set to 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="d09f3-145">**Note:** The default sync interval is set to 60 minutes.</span></span> <span data-ttu-id="d09f3-146">Users can configure overrides to change the sync interval.</span><span class="sxs-lookup"><span data-stu-id="d09f3-146">Users can configure overrides to change the sync interval.</span></span> <span data-ttu-id="d09f3-147">Users can also add servers to the Service Map Servers Group manually through the Authoring pane (Authoring pane --> Groups, then search for "Service Map Servers Group").</span><span class="sxs-lookup"><span data-stu-id="d09f3-147">Users can also add servers to the Service Map Servers Group manually through the Authoring pane (Authoring pane --> Groups, then search for "Service Map Servers Group").</span></span> <span data-ttu-id="d09f3-148">The server maps for those servers will be synced with the next sync (based on the sync interval configured).</span><span class="sxs-lookup"><span data-stu-id="d09f3-148">The server maps for those servers will be synced with the next sync (based on the sync interval configured).</span></span>

## <a name="monitoring-service-map"></a><span data-ttu-id="d09f3-149">Monitoring Service Map</span><span class="sxs-lookup"><span data-stu-id="d09f3-149">Monitoring Service Map</span></span>
<span data-ttu-id="d09f3-150">Once the OMS workspace is connected, a new folder Service Map will show up in the Monitoring pane of the SCOM console.</span><span class="sxs-lookup"><span data-stu-id="d09f3-150">Once the OMS workspace is connected, a new folder Service Map will show up in the Monitoring pane of the SCOM console.</span></span>
<span data-ttu-id="d09f3-151">![SCOM Monitoring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-monitoring.png)</span><span class="sxs-lookup"><span data-stu-id="d09f3-151">![SCOM Monitoring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-monitoring.png)</span></span>

<span data-ttu-id="d09f3-152">The Service Map folder has three nodes:</span><span class="sxs-lookup"><span data-stu-id="d09f3-152">The Service Map folder has three nodes:</span></span>
### <a name="active-alerts"></a><span data-ttu-id="d09f3-153">Active Alerts:</span><span class="sxs-lookup"><span data-stu-id="d09f3-153">Active Alerts:</span></span>
<span data-ttu-id="d09f3-154">This shows all the active alerts about the communication between SCOM and Service Map solution in OMS.</span><span class="sxs-lookup"><span data-stu-id="d09f3-154">This shows all the active alerts about the communication between SCOM and Service Map solution in OMS.</span></span>

<span data-ttu-id="d09f3-155">**Note:** These are not OMS alerts being surfaced in SCOM.</span><span class="sxs-lookup"><span data-stu-id="d09f3-155">**Note:** These are not OMS alerts being surfaced in SCOM.</span></span>
### <a name="servers"></a><span data-ttu-id="d09f3-156">Servers:</span><span class="sxs-lookup"><span data-stu-id="d09f3-156">Servers:</span></span>
<span data-ttu-id="d09f3-157">This will have the list of monitored servers configured to sync from Service Map.</span><span class="sxs-lookup"><span data-stu-id="d09f3-157">This will have the list of monitored servers configured to sync from Service Map.</span></span>

![SCOM Monitoring Servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-monitoring-servers.png)

### <a name="server-dependency-views"></a><span data-ttu-id="d09f3-159">Server Dependency Views:</span><span class="sxs-lookup"><span data-stu-id="d09f3-159">Server Dependency Views:</span></span>
<span data-ttu-id="d09f3-160">This view will have the list of all servers synced from Service Map.</span><span class="sxs-lookup"><span data-stu-id="d09f3-160">This view will have the list of all servers synced from Service Map.</span></span> <span data-ttu-id="d09f3-161">Users can click on any server to view its Distributed Application Diagram.</span><span class="sxs-lookup"><span data-stu-id="d09f3-161">Users can click on any server to view its Distributed Application Diagram.</span></span>

![SCOM Distributed Application Diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-dad.png)

## <a name="editdelete-workspace"></a><span data-ttu-id="d09f3-163">Edit/Delete Workspace:</span><span class="sxs-lookup"><span data-stu-id="d09f3-163">Edit/Delete Workspace:</span></span>
<span data-ttu-id="d09f3-164">Users can Edit or delete the configured workspace through the Service Map Overview pane (Administration pane --> Operations Management Suite --> Service Map).</span><span class="sxs-lookup"><span data-stu-id="d09f3-164">Users can Edit or delete the configured workspace through the Service Map Overview pane (Administration pane --> Operations Management Suite --> Service Map).</span></span>  <span data-ttu-id="d09f3-165">Note that you can configure only one OMS Workspace for now.</span><span class="sxs-lookup"><span data-stu-id="d09f3-165">Note that you can configure only one OMS Workspace for now.</span></span>

![SCOM Edit Workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-edit-workspace.png)

## <a name="configuring-rules-and-overrides"></a><span data-ttu-id="d09f3-167">Configuring Rules and Overrides:</span><span class="sxs-lookup"><span data-stu-id="d09f3-167">Configuring Rules and Overrides:</span></span>
<span data-ttu-id="d09f3-168">A Rule **_Microsoft.SystemCenter.ServiceMapImport.Rule**_ is created to periodically fetch information from Service Map.</span><span class="sxs-lookup"><span data-stu-id="d09f3-168">A Rule **_Microsoft.SystemCenter.ServiceMapImport.Rule**_ is created to periodically fetch information from Service Map.</span></span>  <span data-ttu-id="d09f3-169">Users can configure Overrides of this rule to change sync timings.</span><span class="sxs-lookup"><span data-stu-id="d09f3-169">Users can configure Overrides of this rule to change sync timings.</span></span>
<span data-ttu-id="d09f3-170">Authoring pane --> Rules --> Microsoft.SystemCenter.ServiceMapImport.Rule</span><span class="sxs-lookup"><span data-stu-id="d09f3-170">Authoring pane --> Rules --> Microsoft.SystemCenter.ServiceMapImport.Rule</span></span>

![SCOM Overrides](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/scom-overrides.png)
* <span data-ttu-id="d09f3-172">**Enabled** – enable/disable automatic updates</span><span class="sxs-lookup"><span data-stu-id="d09f3-172">**Enabled** – enable/disable automatic updates</span></span> 
* <span data-ttu-id="d09f3-173">**IntervalSeconds** – the time between updates.</span><span class="sxs-lookup"><span data-stu-id="d09f3-173">**IntervalSeconds** – the time between updates.</span></span>  <span data-ttu-id="d09f3-174">Default is 1 hour.</span><span class="sxs-lookup"><span data-stu-id="d09f3-174">Default is 1 hour.</span></span> <span data-ttu-id="d09f3-175">Users can change the value here if they want to sync server maps more frequently.</span><span class="sxs-lookup"><span data-stu-id="d09f3-175">Users can change the value here if they want to sync server maps more frequently.</span></span>
* <span data-ttu-id="d09f3-176">**TimeoutSeconds** – how long before the request times out</span><span class="sxs-lookup"><span data-stu-id="d09f3-176">**TimeoutSeconds** – how long before the request times out</span></span> 
* <span data-ttu-id="d09f3-177">**TimeWindowMinutes** – how wide is the query for data.</span><span class="sxs-lookup"><span data-stu-id="d09f3-177">**TimeWindowMinutes** – how wide is the query for data.</span></span>  <span data-ttu-id="d09f3-178">Default is a 60-minute wide window.</span><span class="sxs-lookup"><span data-stu-id="d09f3-178">Default is a 60-minute wide window.</span></span> <span data-ttu-id="d09f3-179">The maximum value is 1 hour (the maximum that Service Map allows).</span><span class="sxs-lookup"><span data-stu-id="d09f3-179">The maximum value is 1 hour (the maximum that Service Map allows).</span></span>

## <a name="known-issueslimitations"></a><span data-ttu-id="d09f3-180">Known Issues/Limitations:</span><span class="sxs-lookup"><span data-stu-id="d09f3-180">Known Issues/Limitations:</span></span>
<span data-ttu-id="d09f3-181">In the current design:</span><span class="sxs-lookup"><span data-stu-id="d09f3-181">In the current design:</span></span>
1. <span data-ttu-id="d09f3-182">While users can add servers to “Service Map Servers Group” manually through the authoring pane, the maps for those servers will be synced from Service Map only during the next sync cycle (60 minutes by default.</span><span class="sxs-lookup"><span data-stu-id="d09f3-182">While users can add servers to “Service Map Servers Group” manually through the authoring pane, the maps for those servers will be synced from Service Map only during the next sync cycle (60 minutes by default.</span></span> <span data-ttu-id="d09f3-183">Users can override the sync timing.).</span><span class="sxs-lookup"><span data-stu-id="d09f3-183">Users can override the sync timing.).</span></span> 
2. <span data-ttu-id="d09f3-184">Users can connect to a single OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="d09f3-184">Users can connect to a single OMS workspace.</span></span>

## <a name="creating-a-service-principal"></a><span data-ttu-id="d09f3-185">Creating A Service Principal</span><span class="sxs-lookup"><span data-stu-id="d09f3-185">Creating A Service Principal</span></span>
<span data-ttu-id="d09f3-186">The following links will take you to official Azure documentation about three different ways to create a Service Principal.</span><span class="sxs-lookup"><span data-stu-id="d09f3-186">The following links will take you to official Azure documentation about three different ways to create a Service Principal.</span></span>
* [<span data-ttu-id="d09f3-187">Create Service Principal with PowerShell</span><span class="sxs-lookup"><span data-stu-id="d09f3-187">Create Service Principal with PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="d09f3-188">Create Service Principal with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d09f3-188">Create Service Principal with Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="d09f3-189">Create Service Principal with Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d09f3-189">Create Service Principal with Azure Portal</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="d09f3-190">Feedback</span><span class="sxs-lookup"><span data-stu-id="d09f3-190">Feedback</span></span>
<span data-ttu-id="d09f3-191">Do you have any feedback for us about Service Map or this documentation?</span><span class="sxs-lookup"><span data-stu-id="d09f3-191">Do you have any feedback for us about Service Map or this documentation?</span></span>  <span data-ttu-id="d09f3-192">Please visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote up existing suggestions.</span><span class="sxs-lookup"><span data-stu-id="d09f3-192">Please visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote up existing suggestions.</span></span>











