---
title: Visualizing your cluster using Service Fabric Explorer | Microsoft Docs
description: Service Fabric Explorer is a web-based tool for inspecting and managing cloud applications and nodes in a Microsoft Azure Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: seanmck
ms.openlocfilehash: 2fdc8d305ef7a332f4958e0cb4d95196ff15b895
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563896"
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="43fe4-103">Visualize your cluster with Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="43fe4-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="43fe4-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="43fe4-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="43fe4-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span><span class="sxs-lookup"><span data-stu-id="43fe4-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="43fe4-106">Video tutorial</span><span class="sxs-lookup"><span data-stu-id="43fe4-106">Video tutorial</span></span>

<span data-ttu-id="43fe4-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span><span class="sxs-lookup"><span data-stu-id="43fe4-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="43fe4-108">Connect to Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="43fe4-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="43fe4-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="43fe4-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="43fe4-110">If you are using Internet Explorer with Service Fabric Explorer to manage a remote cluster, you need to configure some Internet Explorer settings.</span><span class="sxs-lookup"><span data-stu-id="43fe4-110">If you are using Internet Explorer with Service Fabric Explorer to manage a remote cluster, you need to configure some Internet Explorer settings.</span></span> <span data-ttu-id="43fe4-111">To ensure that all information loads correctly, go to **Tools** > **Compatibility View Settings** and uncheck **Display intranet sites in Compatibility View**.</span><span class="sxs-lookup"><span data-stu-id="43fe4-111">To ensure that all information loads correctly, go to **Tools** > **Compatibility View Settings** and uncheck **Display intranet sites in Compatibility View**.</span></span>
>
>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="43fe4-112">Understand the Service Fabric Explorer layout</span><span class="sxs-lookup"><span data-stu-id="43fe4-112">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="43fe4-113">You can navigate through Service Fabric Explorer by using the tree on the left.</span><span class="sxs-lookup"><span data-stu-id="43fe4-113">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="43fe4-114">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span><span class="sxs-lookup"><span data-stu-id="43fe4-114">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Service Fabric Explorer cluster dashboard][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="43fe4-116">View the cluster's layout</span><span class="sxs-lookup"><span data-stu-id="43fe4-116">View the cluster's layout</span></span>
<span data-ttu-id="43fe4-117">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="43fe4-117">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="43fe4-118">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span><span class="sxs-lookup"><span data-stu-id="43fe4-118">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="43fe4-119">You can view how the current cluster is laid out by using the cluster map.</span><span class="sxs-lookup"><span data-stu-id="43fe4-119">You can view how the current cluster is laid out by using the cluster map.</span></span>

![Service Fabric Explorer cluster map][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="43fe4-121">View applications and services</span><span class="sxs-lookup"><span data-stu-id="43fe4-121">View applications and services</span></span>
<span data-ttu-id="43fe4-122">The cluster contains two subtrees: one for applications and another for nodes.</span><span class="sxs-lookup"><span data-stu-id="43fe4-122">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="43fe4-123">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span><span class="sxs-lookup"><span data-stu-id="43fe4-123">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="43fe4-124">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span><span class="sxs-lookup"><span data-stu-id="43fe4-124">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="43fe4-125">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="43fe4-125">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="43fe4-126">By contrast, WebSvcService is stateless and contains a single instance.</span><span class="sxs-lookup"><span data-stu-id="43fe4-126">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Service Fabric Explorer application view][sfx-application-tree]

<span data-ttu-id="43fe4-128">At each level of the tree, the main pane shows pertinent information about the item.</span><span class="sxs-lookup"><span data-stu-id="43fe4-128">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="43fe4-129">For example, you can see the health status and version for a particular service.</span><span class="sxs-lookup"><span data-stu-id="43fe4-129">For example, you can see the health status and version for a particular service.</span></span>

![Service Fabric Explorer essentials pane][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="43fe4-131">View the cluster's nodes</span><span class="sxs-lookup"><span data-stu-id="43fe4-131">View the cluster's nodes</span></span>
<span data-ttu-id="43fe4-132">The node view shows the physical layout of the cluster.</span><span class="sxs-lookup"><span data-stu-id="43fe4-132">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="43fe4-133">For a given node, you can inspect which applications have code deployed on that node.</span><span class="sxs-lookup"><span data-stu-id="43fe4-133">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="43fe4-134">More specifically, you can see which replicas are currently running there.</span><span class="sxs-lookup"><span data-stu-id="43fe4-134">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="43fe4-135">Actions</span><span class="sxs-lookup"><span data-stu-id="43fe4-135">Actions</span></span>
<span data-ttu-id="43fe4-136">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span><span class="sxs-lookup"><span data-stu-id="43fe4-136">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="43fe4-137">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span><span class="sxs-lookup"><span data-stu-id="43fe4-137">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![Deleting an application in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="43fe4-139">You can perform the same actions by clicking the ellipsis next to each element.</span><span class="sxs-lookup"><span data-stu-id="43fe4-139">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="43fe4-140">The following table lists the actions available for each entity:</span><span class="sxs-lookup"><span data-stu-id="43fe4-140">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="43fe4-141">**Entity**</span><span class="sxs-lookup"><span data-stu-id="43fe4-141">**Entity**</span></span> | <span data-ttu-id="43fe4-142">**Action**</span><span class="sxs-lookup"><span data-stu-id="43fe4-142">**Action**</span></span> | <span data-ttu-id="43fe4-143">**Description**</span><span class="sxs-lookup"><span data-stu-id="43fe4-143">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43fe4-144">Application type</span><span class="sxs-lookup"><span data-stu-id="43fe4-144">Application type</span></span> |<span data-ttu-id="43fe4-145">Unprovision type</span><span class="sxs-lookup"><span data-stu-id="43fe4-145">Unprovision type</span></span> |<span data-ttu-id="43fe4-146">Removes the application package from the cluster's image store.</span><span class="sxs-lookup"><span data-stu-id="43fe4-146">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="43fe4-147">Requires all applications of that type to be removed first.</span><span class="sxs-lookup"><span data-stu-id="43fe4-147">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="43fe4-148">Application</span><span class="sxs-lookup"><span data-stu-id="43fe4-148">Application</span></span> |<span data-ttu-id="43fe4-149">Delete Application</span><span class="sxs-lookup"><span data-stu-id="43fe4-149">Delete Application</span></span> |<span data-ttu-id="43fe4-150">Delete the application, including all its services and their state (if any).</span><span class="sxs-lookup"><span data-stu-id="43fe4-150">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="43fe4-151">Service</span><span class="sxs-lookup"><span data-stu-id="43fe4-151">Service</span></span> |<span data-ttu-id="43fe4-152">Delete Service</span><span class="sxs-lookup"><span data-stu-id="43fe4-152">Delete Service</span></span> |<span data-ttu-id="43fe4-153">Delete the service and its state (if any).</span><span class="sxs-lookup"><span data-stu-id="43fe4-153">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="43fe4-154">Node</span><span class="sxs-lookup"><span data-stu-id="43fe4-154">Node</span></span> |<span data-ttu-id="43fe4-155">Activate</span><span class="sxs-lookup"><span data-stu-id="43fe4-155">Activate</span></span> |<span data-ttu-id="43fe4-156">Activate the node.</span><span class="sxs-lookup"><span data-stu-id="43fe4-156">Activate the node.</span></span> |
| <span data-ttu-id="43fe4-157">Node</span><span class="sxs-lookup"><span data-stu-id="43fe4-157">Node</span></span> | <span data-ttu-id="43fe4-158">Deactivate (pause)</span><span class="sxs-lookup"><span data-stu-id="43fe4-158">Deactivate (pause)</span></span> | <span data-ttu-id="43fe4-159">Pause the node in its current state.</span><span class="sxs-lookup"><span data-stu-id="43fe4-159">Pause the node in its current state.</span></span> <span data-ttu-id="43fe4-160">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span><span class="sxs-lookup"><span data-stu-id="43fe4-160">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="43fe4-161">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span><span class="sxs-lookup"><span data-stu-id="43fe4-161">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="43fe4-162">Node</span><span class="sxs-lookup"><span data-stu-id="43fe4-162">Node</span></span> | <span data-ttu-id="43fe4-163">Deactivate (restart)</span><span class="sxs-lookup"><span data-stu-id="43fe4-163">Deactivate (restart)</span></span> | <span data-ttu-id="43fe4-164">Safely move all in-memory services off a node and close persistent services.</span><span class="sxs-lookup"><span data-stu-id="43fe4-164">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="43fe4-165">Typically used when the host processes or machine need to be restarted.</span><span class="sxs-lookup"><span data-stu-id="43fe4-165">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="43fe4-166">Node</span><span class="sxs-lookup"><span data-stu-id="43fe4-166">Node</span></span> | <span data-ttu-id="43fe4-167">Deactivate (remove data)</span><span class="sxs-lookup"><span data-stu-id="43fe4-167">Deactivate (remove data)</span></span> | <span data-ttu-id="43fe4-168">Safely close all services running on the node after building sufficient spare replicas.</span><span class="sxs-lookup"><span data-stu-id="43fe4-168">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="43fe4-169">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span><span class="sxs-lookup"><span data-stu-id="43fe4-169">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="43fe4-170">Node</span><span class="sxs-lookup"><span data-stu-id="43fe4-170">Node</span></span> | <span data-ttu-id="43fe4-171">Remove node state</span><span class="sxs-lookup"><span data-stu-id="43fe4-171">Remove node state</span></span> | <span data-ttu-id="43fe4-172">Remove knowledge of a node's replicas from the cluster.</span><span class="sxs-lookup"><span data-stu-id="43fe4-172">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="43fe4-173">Typically used when an already failed node is deemed unrecoverable.</span><span class="sxs-lookup"><span data-stu-id="43fe4-173">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="43fe4-174">Node</span><span class="sxs-lookup"><span data-stu-id="43fe4-174">Node</span></span> | <span data-ttu-id="43fe4-175">Restart</span><span class="sxs-lookup"><span data-stu-id="43fe4-175">Restart</span></span> | <span data-ttu-id="43fe4-176">Simulate a node failure by restarting the node.</span><span class="sxs-lookup"><span data-stu-id="43fe4-176">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="43fe4-177">More information [here](https://docs.microsoft.com/en-us/powershell/servicefabric/vlatest/Restart-ServiceFabricNode)</span><span class="sxs-lookup"><span data-stu-id="43fe4-177">More information [here](https://docs.microsoft.com/en-us/powershell/servicefabric/vlatest/Restart-ServiceFabricNode)</span></span> | |

<span data-ttu-id="43fe4-178">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span><span class="sxs-lookup"><span data-stu-id="43fe4-178">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="43fe4-179">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span><span class="sxs-lookup"><span data-stu-id="43fe4-179">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="43fe4-180">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span><span class="sxs-lookup"><span data-stu-id="43fe4-180">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="43fe4-181">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span><span class="sxs-lookup"><span data-stu-id="43fe4-181">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![Creating an application instance in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="43fe4-183">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span><span class="sxs-lookup"><span data-stu-id="43fe4-183">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="43fe4-184">They are created using default parameter values.</span><span class="sxs-lookup"><span data-stu-id="43fe4-184">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="43fe4-185">Connect to a remote Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="43fe4-185">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="43fe4-186">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span><span class="sxs-lookup"><span data-stu-id="43fe4-186">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="43fe4-187">This is because Service Fabric Explorer is just another service that runs in the cluster.</span><span class="sxs-lookup"><span data-stu-id="43fe4-187">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="43fe4-188">Discover the Service Fabric Explorer endpoint for a remote cluster</span><span class="sxs-lookup"><span data-stu-id="43fe4-188">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="43fe4-189">To reach Service Fabric Explorer for a given cluster, point your browser to:</span><span class="sxs-lookup"><span data-stu-id="43fe4-189">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="43fe4-190">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="43fe4-190">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="43fe4-191">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43fe4-191">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="43fe4-192">Connect to a secure cluster</span><span class="sxs-lookup"><span data-stu-id="43fe4-192">Connect to a secure cluster</span></span>
<span data-ttu-id="43fe4-193">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="43fe4-193">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="43fe4-194">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span><span class="sxs-lookup"><span data-stu-id="43fe4-194">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43fe4-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="43fe4-195">Next steps</span></span>
* [<span data-ttu-id="43fe4-196">Testability overview</span><span class="sxs-lookup"><span data-stu-id="43fe4-196">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="43fe4-197">Managing your Service Fabric applications in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43fe4-197">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="43fe4-198">Service Fabric application deployment using PowerShell</span><span class="sxs-lookup"><span data-stu-id="43fe4-198">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png







