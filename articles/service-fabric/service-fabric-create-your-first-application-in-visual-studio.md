---
title: Create your first Azure microservices application | Microsoft Docs
description: Create, deploy, and debug a Service Fabric application using Visual Studio
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/07/2017
ms.author: ryanwi
ms.openlocfilehash: 2258d6a57295e9a4a78ebce473217cacb77bbe1b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556317"
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="ad18b-103">Create your first Azure Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="ad18b-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
> 
> 

<span data-ttu-id="ad18b-107">The Service Fabric SDK includes an add-in for Visual Studio that provides templates and tools for creating, deploying, and debugging Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="ad18b-107">The Service Fabric SDK includes an add-in for Visual Studio that provides templates and tools for creating, deploying, and debugging Service Fabric applications.</span></span> <span data-ttu-id="ad18b-108">This topic walks you through the process of creating your first application in Visual Studio 2017 or Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ad18b-108">This topic walks you through the process of creating your first application in Visual Studio 2017 or Visual Studio 2015.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad18b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ad18b-109">Prerequisites</span></span>
<span data-ttu-id="ad18b-110">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ad18b-110">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span>

## <a name="video-walkthrough"></a><span data-ttu-id="ad18b-111">Video walkthrough</span><span class="sxs-lookup"><span data-stu-id="ad18b-111">Video walkthrough</span></span>
<span data-ttu-id="ad18b-112">The following video walks through the steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="ad18b-112">The following video walks through the steps in this tutorial:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Creating-your-first-Service-Fabric-application-in-Visual-Studio/player]
> 
> 

## <a name="create-the-application"></a><span data-ttu-id="ad18b-113">Create the application</span><span class="sxs-lookup"><span data-stu-id="ad18b-113">Create the application</span></span>
<span data-ttu-id="ad18b-114">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="ad18b-114">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="ad18b-115">Create an application project, along with your first service project, using the New Project wizard.</span><span class="sxs-lookup"><span data-stu-id="ad18b-115">Create an application project, along with your first service project, using the New Project wizard.</span></span> <span data-ttu-id="ad18b-116">You can also add more services later if you want.</span><span class="sxs-lookup"><span data-stu-id="ad18b-116">You can also add more services later if you want.</span></span>

1. <span data-ttu-id="ad18b-117">Launch Visual Studio as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ad18b-117">Launch Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="ad18b-118">Click **File > New Project > Cloud > Service Fabric Application**.</span><span class="sxs-lookup"><span data-stu-id="ad18b-118">Click **File > New Project > Cloud > Service Fabric Application**.</span></span>
3. <span data-ttu-id="ad18b-119">Name the application and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad18b-119">Name the application and click **OK**.</span></span>
   
    ![New project dialog in Visual Studio][1]
4. <span data-ttu-id="ad18b-121">On the next page, choose **Stateful** as the first service type to include in your application.</span><span class="sxs-lookup"><span data-stu-id="ad18b-121">On the next page, choose **Stateful** as the first service type to include in your application.</span></span> <span data-ttu-id="ad18b-122">Name it and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad18b-122">Name it and click **OK**.</span></span>
   
    ![New service dialog in Visual Studio][2]
   
   > [!NOTE]
   > For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).
   > 
   > 
   
    <span data-ttu-id="ad18b-125">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="ad18b-125">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>
   
    ![Solution Explorer following creation of application with stateful service][3]
   
    <span data-ttu-id="ad18b-127">The application project does not contain any code directly.</span><span class="sxs-lookup"><span data-stu-id="ad18b-127">The application project does not contain any code directly.</span></span> <span data-ttu-id="ad18b-128">Instead, it references a set of service projects.</span><span class="sxs-lookup"><span data-stu-id="ad18b-128">Instead, it references a set of service projects.</span></span> <span data-ttu-id="ad18b-129">In addition, it contains three other types of content:</span><span class="sxs-lookup"><span data-stu-id="ad18b-129">In addition, it contains three other types of content:</span></span>
   
   * <span data-ttu-id="ad18b-130">**Publish profiles**: Used to manage tooling preferences for different environments.</span><span class="sxs-lookup"><span data-stu-id="ad18b-130">**Publish profiles**: Used to manage tooling preferences for different environments.</span></span>
   * <span data-ttu-id="ad18b-131">**Scripts**: Includes a PowerShell script for deploying/upgrading your application.</span><span class="sxs-lookup"><span data-stu-id="ad18b-131">**Scripts**: Includes a PowerShell script for deploying/upgrading your application.</span></span> <span data-ttu-id="ad18b-132">Visual Studio uses the script behind-the-scenes.</span><span class="sxs-lookup"><span data-stu-id="ad18b-132">Visual Studio uses the script behind-the-scenes.</span></span> <span data-ttu-id="ad18b-133">The script can also be invoked directly at the command line.</span><span class="sxs-lookup"><span data-stu-id="ad18b-133">The script can also be invoked directly at the command line.</span></span>
   * <span data-ttu-id="ad18b-134">**Application definition**: Includes the application manifest under *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="ad18b-134">**Application definition**: Includes the application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="ad18b-135">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span><span class="sxs-lookup"><span data-stu-id="ad18b-135">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span></span>
     
     <span data-ttu-id="ad18b-136">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="ad18b-136">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="ad18b-137">Deploy and debug the application</span><span class="sxs-lookup"><span data-stu-id="ad18b-137">Deploy and debug the application</span></span>
<span data-ttu-id="ad18b-138">Now that you have an application, try running it.</span><span class="sxs-lookup"><span data-stu-id="ad18b-138">Now that you have an application, try running it.</span></span>

1. <span data-ttu-id="ad18b-139">Press F5 in Visual Studio to deploy the application for debugging.</span><span class="sxs-lookup"><span data-stu-id="ad18b-139">Press F5 in Visual Studio to deploy the application for debugging.</span></span>
   
   > [!NOTE]
   > Deploying takes a while the first time, as Visual Studio is creating a local cluster for development. A local cluster runs the same platform code that you build on in a multi-machine cluster, just on a single machine. The cluster creation status displays in the Visual Studio output window.
   > 
   > 
   
    <span data-ttu-id="ad18b-143">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span><span class="sxs-lookup"><span data-stu-id="ad18b-143">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
    ![Local cluster system tray notification][4]
2. <span data-ttu-id="ad18b-145">Once the application starts, Visual Studio automatically brings up the Diagnostics Event Viewer, where you can see trace output from the service.</span><span class="sxs-lookup"><span data-stu-id="ad18b-145">Once the application starts, Visual Studio automatically brings up the Diagnostics Event Viewer, where you can see trace output from the service.</span></span>
   
    ![Diagnostic events viewer][5]
   
    <span data-ttu-id="ad18b-147">In the case of the stateful service template, the messages simply show the counter value incrementing in the `RunAsync` method of MyStatefulService.cs.</span><span class="sxs-lookup"><span data-stu-id="ad18b-147">In the case of the stateful service template, the messages simply show the counter value incrementing in the `RunAsync` method of MyStatefulService.cs.</span></span>
3. <span data-ttu-id="ad18b-148">Expand one of the events to see more details, including the node where the code is running.</span><span class="sxs-lookup"><span data-stu-id="ad18b-148">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="ad18b-149">In this case, it is _Node_2, though it may differ on your machine.</span><span class="sxs-lookup"><span data-stu-id="ad18b-149">In this case, it is _Node_2, though it may differ on your machine.</span></span>
   
    ![Diagnostic events viewer detail][6]
   
    <span data-ttu-id="ad18b-151">The local cluster contains five nodes hosted on a single machine.</span><span class="sxs-lookup"><span data-stu-id="ad18b-151">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="ad18b-152">It mimics a five-node cluster, where nodes are on distinct machines.</span><span class="sxs-lookup"><span data-stu-id="ad18b-152">It mimics a five-node cluster, where nodes are on distinct machines.</span></span> <span data-ttu-id="ad18b-153">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span><span class="sxs-lookup"><span data-stu-id="ad18b-153">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>
   
   > [!NOTE]
   > The application diagnostic events emitted by the project template use the included `ServiceEventSource` class. For more information, see [How to monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
   > 
   > 
4. <span data-ttu-id="ad18b-156">Find the class in your service project that derives from StatefulService (for example, MyStatefulService) and set a breakpoint on the first line of the `RunAsync` method.</span><span class="sxs-lookup"><span data-stu-id="ad18b-156">Find the class in your service project that derives from StatefulService (for example, MyStatefulService) and set a breakpoint on the first line of the `RunAsync` method.</span></span>
   
    ![Breakpoint in stateful service RunAsync method][7]
5. <span data-ttu-id="ad18b-158">To launch Service Fabric Explorer, right-click the Local Cluster Manager system tray app and choose **Manage Local Cluster**.</span><span class="sxs-lookup"><span data-stu-id="ad18b-158">To launch Service Fabric Explorer, right-click the Local Cluster Manager system tray app and choose **Manage Local Cluster**.</span></span>
   
    ![Launch Service Fabric Explorer from the Local Cluster Manager][systray-launch-sfx]
   
    <span data-ttu-id="ad18b-160">Service Fabric Explorer offers a visual representation of a cluster--including the set of applications deployed to it and the set of physical nodes that make it up.</span><span class="sxs-lookup"><span data-stu-id="ad18b-160">Service Fabric Explorer offers a visual representation of a cluster--including the set of applications deployed to it and the set of physical nodes that make it up.</span></span> <span data-ttu-id="ad18b-161">To learn more about Service Fabric Explorer, see [Visualizing your cluster](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ad18b-161">To learn more about Service Fabric Explorer, see [Visualizing your cluster](service-fabric-visualizing-your-cluster.md).</span></span>
6. <span data-ttu-id="ad18b-162">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span><span class="sxs-lookup"><span data-stu-id="ad18b-162">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>
7. <span data-ttu-id="ad18b-163">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span><span class="sxs-lookup"><span data-stu-id="ad18b-163">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span> <span data-ttu-id="ad18b-164">Or, deactivate the node from the node list view in the left pane.)</span><span class="sxs-lookup"><span data-stu-id="ad18b-164">Or, deactivate the node from the node list view in the left pane.)</span></span>
   
    ![Stop a node in Service Fabric Explorer][sfx-stop-node]
   
    <span data-ttu-id="ad18b-166">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span><span class="sxs-lookup"><span data-stu-id="ad18b-166">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>
8. <span data-ttu-id="ad18b-167">Return to the Diagnostic Events Viewer and observe the messages.</span><span class="sxs-lookup"><span data-stu-id="ad18b-167">Return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="ad18b-168">The counter has continued incrementing, even though the events are actually coming from a different node.</span><span class="sxs-lookup"><span data-stu-id="ad18b-168">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>
   
    ![Diagnostic events viewer after failover][diagnostic-events-viewer-detail-post-failover]

## <a name="switch-cluster-mode"></a><span data-ttu-id="ad18b-170">Switch cluster mode</span><span class="sxs-lookup"><span data-stu-id="ad18b-170">Switch cluster mode</span></span>
<span data-ttu-id="ad18b-171">By default, the local development cluster is configured to run as a five-node cluster, which is useful for debugging services deployed across multiple nodes.</span><span class="sxs-lookup"><span data-stu-id="ad18b-171">By default, the local development cluster is configured to run as a five-node cluster, which is useful for debugging services deployed across multiple nodes.</span></span> <span data-ttu-id="ad18b-172">Deploying an application to the five-node development cluster can take some time, however.</span><span class="sxs-lookup"><span data-stu-id="ad18b-172">Deploying an application to the five-node development cluster can take some time, however.</span></span> <span data-ttu-id="ad18b-173">If you want to iterate code changes quickly, without running your app on five nodes, switch the development cluster to one-node mode.</span><span class="sxs-lookup"><span data-stu-id="ad18b-173">If you want to iterate code changes quickly, without running your app on five nodes, switch the development cluster to one-node mode.</span></span> <span data-ttu-id="ad18b-174">To run your code on a cluster with one node, right-click on the Local Cluster Manager in the system tray and select **Switch Cluster Mode -> 1 Node**.</span><span class="sxs-lookup"><span data-stu-id="ad18b-174">To run your code on a cluster with one node, right-click on the Local Cluster Manager in the system tray and select **Switch Cluster Mode -> 1 Node**.</span></span>  

![Switch cluster mode][switch-cluster-mode]

<span data-ttu-id="ad18b-176">The development cluster resets when you change cluster mode and all applications provisioned or running on the cluster are removed.</span><span class="sxs-lookup"><span data-stu-id="ad18b-176">The development cluster resets when you change cluster mode and all applications provisioned or running on the cluster are removed.</span></span>

<span data-ttu-id="ad18b-177">You can also change the cluster mode using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ad18b-177">You can also change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="ad18b-178">Launch a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ad18b-178">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="ad18b-179">Run the cluster setup script from the SDK folder:</span><span class="sxs-lookup"><span data-stu-id="ad18b-179">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="ad18b-180">Cluster setup takes a few moments.</span><span class="sxs-lookup"><span data-stu-id="ad18b-180">Cluster setup takes a few moments.</span></span> <span data-ttu-id="ad18b-181">After setup is finished, you should see output similar to:</span><span class="sxs-lookup"><span data-stu-id="ad18b-181">After setup is finished, you should see output similar to:</span></span>
   
    ![Cluster setup output][cluster-setup-success-1-node]

## <a name="cleaning-up"></a><span data-ttu-id="ad18b-183">Cleaning up</span><span class="sxs-lookup"><span data-stu-id="ad18b-183">Cleaning up</span></span>
<span data-ttu-id="ad18b-184">Before wrapping up, it's important to remember that the local cluster is real.</span><span class="sxs-lookup"><span data-stu-id="ad18b-184">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="ad18b-185">Stopping the debugger removes your application instance and unregisters the application type.</span><span class="sxs-lookup"><span data-stu-id="ad18b-185">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="ad18b-186">The cluster continues to run in the background, however.</span><span class="sxs-lookup"><span data-stu-id="ad18b-186">The cluster continues to run in the background, however.</span></span> <span data-ttu-id="ad18b-187">You have several options to manage the cluster:</span><span class="sxs-lookup"><span data-stu-id="ad18b-187">You have several options to manage the cluster:</span></span>

1. <span data-ttu-id="ad18b-188">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span><span class="sxs-lookup"><span data-stu-id="ad18b-188">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
2. <span data-ttu-id="ad18b-189">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span><span class="sxs-lookup"><span data-stu-id="ad18b-189">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="ad18b-190">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad18b-190">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="ad18b-191">Delete the cluster only if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span><span class="sxs-lookup"><span data-stu-id="ad18b-191">Delete the cluster only if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad18b-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad18b-192">Next steps</span></span>
* <span data-ttu-id="ad18b-193">Learn how to create a [cluster in Azure](service-fabric-cluster-creation-via-portal.md) or a [standalone cluster on Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ad18b-193">Learn how to create a [cluster in Azure](service-fabric-cluster-creation-via-portal.md) or a [standalone cluster on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>
* <span data-ttu-id="ad18b-194">Try creating a service using the [Reliable Services](service-fabric-reliable-services-quick-start.md) or [Reliable Actors](service-fabric-reliable-actors-get-started.md) programming models.</span><span class="sxs-lookup"><span data-stu-id="ad18b-194">Try creating a service using the [Reliable Services](service-fabric-reliable-services-quick-start.md) or [Reliable Actors](service-fabric-reliable-actors-get-started.md) programming models.</span></span>
* <span data-ttu-id="ad18b-195">Try deploying a [Windows container](service-fabric-deploy-container.md) or an existing app as a [guest executable](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="ad18b-195">Try deploying a [Windows container](service-fabric-deploy-container.md) or an existing app as a [guest executable](service-fabric-deploy-existing-app.md).</span></span>
* <span data-ttu-id="ad18b-196">Learn how to expose your services to the Internet with a [web service front end](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="ad18b-196">Learn how to expose your services to the Internet with a [web service front end](service-fabric-add-a-web-frontend.md).</span></span>
* <span data-ttu-id="ad18b-197">Walk through a [hands-on-lab](https://msdnshared.blob.core.windows.net/media/2016/07/SF-Lab-Part-I.docx) and create a stateless service, configure monitoring and health reports, and perform an application upgrade.</span><span class="sxs-lookup"><span data-stu-id="ad18b-197">Walk through a [hands-on-lab](https://msdnshared.blob.core.windows.net/media/2016/07/SF-Lab-Part-I.docx) and create a stateless service, configure monitoring and health reports, and perform an application upgrade.</span></span>
* <span data-ttu-id="ad18b-198">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="ad18b-198">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<!-- Image References -->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png













