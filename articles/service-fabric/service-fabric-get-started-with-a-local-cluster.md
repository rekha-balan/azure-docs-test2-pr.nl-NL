---
title: Deploy and upgrade Azure microservices locally | Microsoft Docs
description: Learn how to set up a local Service Fabric cluster, deploy an existing application to it, and then upgrade that application.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: 5af00cdc8ff79b21f73884d0cb76c560e7878193
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555904"
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="478b1-103">Get started with deploying and upgrading applications on your local cluster</span><span class="sxs-lookup"><span data-stu-id="478b1-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="478b1-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span><span class="sxs-lookup"><span data-stu-id="478b1-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="478b1-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="478b1-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="478b1-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="478b1-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="478b1-107">Create a local cluster</span><span class="sxs-lookup"><span data-stu-id="478b1-107">Create a local cluster</span></span>
<span data-ttu-id="478b1-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span><span class="sxs-lookup"><span data-stu-id="478b1-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="478b1-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span><span class="sxs-lookup"><span data-stu-id="478b1-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span></span> <span data-ttu-id="478b1-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span><span class="sxs-lookup"><span data-stu-id="478b1-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="478b1-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span><span class="sxs-lookup"><span data-stu-id="478b1-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="478b1-112">It runs the same platform code that is found on multi-machine clusters.</span><span class="sxs-lookup"><span data-stu-id="478b1-112">It runs the same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="478b1-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span><span class="sxs-lookup"><span data-stu-id="478b1-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="478b1-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span><span class="sxs-lookup"><span data-stu-id="478b1-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span></span> <span data-ttu-id="478b1-115">In this tutorial, we use the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="478b1-115">In this tutorial, we use the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="478b1-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="478b1-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="478b1-117">Launch a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="478b1-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="478b1-118">Run the cluster setup script from the SDK folder:</span><span class="sxs-lookup"><span data-stu-id="478b1-118">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="478b1-119">Cluster setup takes a few moments.</span><span class="sxs-lookup"><span data-stu-id="478b1-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="478b1-120">After setup is finished, you should see output similar to:</span><span class="sxs-lookup"><span data-stu-id="478b1-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Cluster setup output][cluster-setup-success]
   
    <span data-ttu-id="478b1-122">You are now ready to try deploying an application to your cluster.</span><span class="sxs-lookup"><span data-stu-id="478b1-122">You are now ready to try deploying an application to your cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="478b1-123">Deploy an application</span><span class="sxs-lookup"><span data-stu-id="478b1-123">Deploy an application</span></span>
<span data-ttu-id="478b1-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span><span class="sxs-lookup"><span data-stu-id="478b1-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="478b1-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="478b1-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="478b1-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span><span class="sxs-lookup"><span data-stu-id="478b1-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="478b1-127">Launch a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="478b1-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="478b1-128">Import the Service Fabric SDK PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="478b1-128">Import the Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="478b1-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="478b1-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="478b1-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span><span class="sxs-lookup"><span data-stu-id="478b1-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span></span>  <span data-ttu-id="478b1-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span><span class="sxs-lookup"><span data-stu-id="478b1-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span></span>  <span data-ttu-id="478b1-132">Change the file extension to *.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="478b1-132">Change the file extension to *.sfpkg*.</span></span>
5. <span data-ttu-id="478b1-133">Connect to the local cluster:</span><span class="sxs-lookup"><span data-stu-id="478b1-133">Connect to the local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="478b1-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span><span class="sxs-lookup"><span data-stu-id="478b1-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="478b1-135">If all goes well, you should see the following output:</span><span class="sxs-lookup"><span data-stu-id="478b1-135">If all goes well, you should see the following output:</span></span>
   
    ![Deploy an application to the local cluster][deploy-app-to-local-cluster]
7. <span data-ttu-id="478b1-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="478b1-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="478b1-138">You should see:</span><span class="sxs-lookup"><span data-stu-id="478b1-138">You should see:</span></span>
   
    ![Deployed application UI][deployed-app-ui]
   
    <span data-ttu-id="478b1-140">The WordCount application is simple.</span><span class="sxs-lookup"><span data-stu-id="478b1-140">The WordCount application is simple.</span></span> <span data-ttu-id="478b1-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="478b1-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span></span> <span data-ttu-id="478b1-142">A stateful service tracks the number of words counted.</span><span class="sxs-lookup"><span data-stu-id="478b1-142">A stateful service tracks the number of words counted.</span></span> <span data-ttu-id="478b1-143">They are partitioned based on the first character of the word.</span><span class="sxs-lookup"><span data-stu-id="478b1-143">They are partitioned based on the first character of the word.</span></span> <span data-ttu-id="478b1-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="478b1-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="478b1-145">The application that we deployed contains four partitions.</span><span class="sxs-lookup"><span data-stu-id="478b1-145">The application that we deployed contains four partitions.</span></span> <span data-ttu-id="478b1-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span><span class="sxs-lookup"><span data-stu-id="478b1-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="478b1-147">View application details and status</span><span class="sxs-lookup"><span data-stu-id="478b1-147">View application details and status</span></span>
<span data-ttu-id="478b1-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="478b1-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span></span>

1. <span data-ttu-id="478b1-149">Query all deployed applications on the cluster:</span><span class="sxs-lookup"><span data-stu-id="478b1-149">Query all deployed applications on the cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="478b1-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span><span class="sxs-lookup"><span data-stu-id="478b1-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span></span>
   
    ![Query all deployed applications in PowerShell][ps-getsfapp]
2. <span data-ttu-id="478b1-152">Go to the next level by querying the set of services that are included in the WordCount application.</span><span class="sxs-lookup"><span data-stu-id="478b1-152">Go to the next level by querying the set of services that are included in the WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![List services for the application in PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="478b1-154">The application is made up of two services--the web front end and the stateful service that manages the words.</span><span class="sxs-lookup"><span data-stu-id="478b1-154">The application is made up of two services--the web front end and the stateful service that manages the words.</span></span>
3. <span data-ttu-id="478b1-155">Finally, look at the list of partitions for WordCountService:</span><span class="sxs-lookup"><span data-stu-id="478b1-155">Finally, look at the list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![View the service partitions in PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="478b1-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span><span class="sxs-lookup"><span data-stu-id="478b1-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="478b1-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span><span class="sxs-lookup"><span data-stu-id="478b1-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span></span>
   
    ![View application details in Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="478b1-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="478b1-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="478b1-161">Upgrade an application</span><span class="sxs-lookup"><span data-stu-id="478b1-161">Upgrade an application</span></span>
<span data-ttu-id="478b1-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span><span class="sxs-lookup"><span data-stu-id="478b1-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span></span> <span data-ttu-id="478b1-163">Perform an upgrade of the WordCount application.</span><span class="sxs-lookup"><span data-stu-id="478b1-163">Perform an upgrade of the WordCount application.</span></span>

<span data-ttu-id="478b1-164">The new version of the application now counts only words that begin with a vowel.</span><span class="sxs-lookup"><span data-stu-id="478b1-164">The new version of the application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="478b1-165">As the upgrade rolls out, we see two changes in the application's behavior.</span><span class="sxs-lookup"><span data-stu-id="478b1-165">As the upgrade rolls out, we see two changes in the application's behavior.</span></span> <span data-ttu-id="478b1-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span><span class="sxs-lookup"><span data-stu-id="478b1-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="478b1-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span><span class="sxs-lookup"><span data-stu-id="478b1-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span></span>

1. <span data-ttu-id="478b1-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span><span class="sxs-lookup"><span data-stu-id="478b1-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span></span>
2. <span data-ttu-id="478b1-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span><span class="sxs-lookup"><span data-stu-id="478b1-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span></span> <span data-ttu-id="478b1-170">Then begin upgrading the fabric:/WordCount application.</span><span class="sxs-lookup"><span data-stu-id="478b1-170">Then begin upgrading the fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="478b1-171">You should see the following output in PowerShell as the upgrade begins.</span><span class="sxs-lookup"><span data-stu-id="478b1-171">You should see the following output in PowerShell as the upgrade begins.</span></span>
   
    ![Upgrade progress in PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="478b1-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="478b1-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="478b1-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="478b1-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="478b1-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span><span class="sxs-lookup"><span data-stu-id="478b1-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="478b1-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="478b1-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span></span>
   
    ![Upgrade progress in Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="478b1-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span><span class="sxs-lookup"><span data-stu-id="478b1-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span></span>
4. <span data-ttu-id="478b1-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span><span class="sxs-lookup"><span data-stu-id="478b1-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Query application services after upgrade][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="478b1-181">This example highlights how Service Fabric manages application upgrades.</span><span class="sxs-lookup"><span data-stu-id="478b1-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="478b1-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span><span class="sxs-lookup"><span data-stu-id="478b1-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="478b1-183">Finally, return to the browser to observe the behavior of the new application version.</span><span class="sxs-lookup"><span data-stu-id="478b1-183">Finally, return to the browser to observe the behavior of the new application version.</span></span> <span data-ttu-id="478b1-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span><span class="sxs-lookup"><span data-stu-id="478b1-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span></span>
   
    ![View the new version of the application in the browser][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="478b1-186">Cleaning up</span><span class="sxs-lookup"><span data-stu-id="478b1-186">Cleaning up</span></span>
<span data-ttu-id="478b1-187">Before wrapping up, it's important to remember that the local cluster is real.</span><span class="sxs-lookup"><span data-stu-id="478b1-187">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="478b1-188">Applications continue to run in the background until you remove them.</span><span class="sxs-lookup"><span data-stu-id="478b1-188">Applications continue to run in the background until you remove them.</span></span>  <span data-ttu-id="478b1-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span><span class="sxs-lookup"><span data-stu-id="478b1-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="478b1-190">You have several options to manage applications and the cluster:</span><span class="sxs-lookup"><span data-stu-id="478b1-190">You have several options to manage applications and the cluster:</span></span>

1. <span data-ttu-id="478b1-191">To remove an individual application and all it's data, run the following command:</span><span class="sxs-lookup"><span data-stu-id="478b1-191">To remove an individual application and all it's data, run the following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="478b1-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span><span class="sxs-lookup"><span data-stu-id="478b1-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span></span>
   
    ![Delete an application is Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="478b1-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span><span class="sxs-lookup"><span data-stu-id="478b1-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span></span> <span data-ttu-id="478b1-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span><span class="sxs-lookup"><span data-stu-id="478b1-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="478b1-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span><span class="sxs-lookup"><span data-stu-id="478b1-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span></span>
3. <span data-ttu-id="478b1-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span><span class="sxs-lookup"><span data-stu-id="478b1-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
4. <span data-ttu-id="478b1-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span><span class="sxs-lookup"><span data-stu-id="478b1-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="478b1-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="478b1-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="478b1-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span><span class="sxs-lookup"><span data-stu-id="478b1-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="478b1-201">One-node and five-node cluster mode</span><span class="sxs-lookup"><span data-stu-id="478b1-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="478b1-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span><span class="sxs-lookup"><span data-stu-id="478b1-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="478b1-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span><span class="sxs-lookup"><span data-stu-id="478b1-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="478b1-204">Both cluster modes have their benefits.</span><span class="sxs-lookup"><span data-stu-id="478b1-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="478b1-205">Five-node cluster mode enables you to work with a real cluster.</span><span class="sxs-lookup"><span data-stu-id="478b1-205">Five-node cluster mode enables you to work with a real cluster.</span></span> <span data-ttu-id="478b1-206">You can test failover scenarios, work with more instances and replicas of your services.</span><span class="sxs-lookup"><span data-stu-id="478b1-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="478b1-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="478b1-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span></span>

<span data-ttu-id="478b1-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span><span class="sxs-lookup"><span data-stu-id="478b1-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="478b1-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span><span class="sxs-lookup"><span data-stu-id="478b1-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="478b1-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span><span class="sxs-lookup"><span data-stu-id="478b1-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="478b1-211">The data stored in the cluster is deleted when you change cluster mode.</span><span class="sxs-lookup"><span data-stu-id="478b1-211">The data stored in the cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="478b1-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="478b1-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span></span>

![Switch cluster mode][switch-cluster-mode]

<span data-ttu-id="478b1-214">Or, change the cluster mode using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="478b1-214">Or, change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="478b1-215">Launch a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="478b1-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="478b1-216">Run the cluster setup script from the SDK folder:</span><span class="sxs-lookup"><span data-stu-id="478b1-216">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="478b1-217">Cluster setup takes a few moments.</span><span class="sxs-lookup"><span data-stu-id="478b1-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="478b1-218">After setup is finished, you should see output similar to:</span><span class="sxs-lookup"><span data-stu-id="478b1-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Cluster setup output][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="478b1-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="478b1-220">Next steps</span></span>
* <span data-ttu-id="478b1-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="478b1-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="478b1-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span><span class="sxs-lookup"><span data-stu-id="478b1-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="478b1-223">The upgrade that we performed in this article was basic.</span><span class="sxs-lookup"><span data-stu-id="478b1-223">The upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="478b1-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span><span class="sxs-lookup"><span data-stu-id="478b1-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
















