---
title: Report and check health with Azure Service Fabric | Microsoft Docs
description: Learn how to send health reports from your service code and how to check the health of your service by using the health monitoring tools that Azure Service Fabric provides.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: ''
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: dekapur
ms.openlocfilehash: d34e42e307eda9fd0ae114c5f7e08e893fe48e2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562769"
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="7b0ea-103">Report and check service health</span><span class="sxs-lookup"><span data-stu-id="7b0ea-103">Report and check service health</span></span>
<span data-ttu-id="7b0ea-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="7b0ea-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="7b0ea-106">There are three ways that you can report health from the service:</span><span class="sxs-lookup"><span data-stu-id="7b0ea-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="7b0ea-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="7b0ea-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="7b0ea-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="7b0ea-110">Use `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="7b0ea-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="7b0ea-112">This won't be true in most real-world scenarios.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-112">This won't be true in most real-world scenarios.</span></span> <span data-ttu-id="7b0ea-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="7b0ea-114">Ideally, however, service code should only send reports that are related to its own health.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="7b0ea-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica or node levels.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica or node levels.</span></span> <span data-ttu-id="7b0ea-116">This can be used to report health from within a container.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="7b0ea-117">This article walks you through an example that reports health from the service code.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="7b0ea-118">The example also shows how the tools that Service Fabric provides can be used to check the health status.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-118">The example also shows how the tools that Service Fabric provides can be used to check the health status.</span></span> <span data-ttu-id="7b0ea-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="7b0ea-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b0ea-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7b0ea-121">Prerequisites</span></span>
<span data-ttu-id="7b0ea-122">You must have the following installed:</span><span class="sxs-lookup"><span data-stu-id="7b0ea-122">You must have the following installed:</span></span>

* <span data-ttu-id="7b0ea-123">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7b0ea-123">Visual Studio 2015</span></span>
* <span data-ttu-id="7b0ea-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="7b0ea-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="7b0ea-125">To create a local secure dev cluster</span><span class="sxs-lookup"><span data-stu-id="7b0ea-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="7b0ea-126">Open PowerShell with admin privileges, and run the following commands.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-126">Open PowerShell with admin privileges, and run the following commands.</span></span>

![Commands that show how to create a secure dev cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="7b0ea-128">To deploy an application and check its health</span><span class="sxs-lookup"><span data-stu-id="7b0ea-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="7b0ea-129">Open Visual Studio as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="7b0ea-130">Create a project by using the **Stateful Service** template.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Create a Service Fabric application with Stateful Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="7b0ea-132">Press **F5** to run the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="7b0ea-133">The application will be deployed to the local cluster.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-133">The application will be deployed to the local cluster.</span></span>
4. <span data-ttu-id="7b0ea-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Open Service Fabric Explorer from notification area](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="7b0ea-136">The application health should be displayed as in this image.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="7b0ea-137">At this time, the application should be healthy with no errors.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Healthy application in Service Fabric Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="7b0ea-139">You can also check the health by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="7b0ea-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="7b0ea-141">The health report for the same application in PowerShell is in this image.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Healthy application in PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="7b0ea-143">To add custom health events to your service code</span><span class="sxs-lookup"><span data-stu-id="7b0ea-143">To add custom health events to your service code</span></span>
<span data-ttu-id="7b0ea-144">The Service Fabric project templates in Visual Studio contain sample code.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="7b0ea-145">The following steps show how you can report custom health events from your service code.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="7b0ea-146">Such reports will automatically show up in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-146">Such reports will automatically show up in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="7b0ea-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="7b0ea-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="7b0ea-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="7b0ea-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="7b0ea-151">To report a health event when the lack of result represents a failure, add the following steps.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="7b0ea-152">a.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-152">a.</span></span> <span data-ttu-id="7b0ea-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="7b0ea-154">b.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-154">b.</span></span> <span data-ttu-id="7b0ea-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span><span class="sxs-lookup"><span data-stu-id="7b0ea-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="7b0ea-156">We report replica health because it's being reported from a stateful service.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="7b0ea-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="7b0ea-158">If you had created a stateless service, use the following code</span><span class="sxs-lookup"><span data-stu-id="7b0ea-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="7b0ea-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="7b0ea-160">a.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-160">a.</span></span> <span data-ttu-id="7b0ea-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="7b0ea-162">b.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-162">b.</span></span> <span data-ttu-id="7b0ea-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="7b0ea-164">Let's simulate this failure and see it show up in the health monitoring tools.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="7b0ea-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="7b0ea-166">After you comment out the first line, the code will look like the following example.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="7b0ea-167">This code will now fire this health report each time `RunAsync` executes.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-167">This code will now fire this health report each time `RunAsync` executes.</span></span> <span data-ttu-id="7b0ea-168">After you make the change, press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="7b0ea-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="7b0ea-170">This time, Service Fabric Explorer will show that the application is unhealthy.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-170">This time, Service Fabric Explorer will show that the application is unhealthy.</span></span> <span data-ttu-id="7b0ea-171">This is because of the error that was reported from the code that we added previously.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Unhealthy application in Service Fabric Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="7b0ea-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="7b0ea-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="7b0ea-175">You can see the same health reports in PowerShell and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Replica health in Service Fabric Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="7b0ea-177">This report will remain in the health manager until it is replaced by another report or until this replica is deleted.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-177">This report will remain in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="7b0ea-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report will never expire.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report will never expire.</span></span>

<span data-ttu-id="7b0ea-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="7b0ea-180">You can also report health on `Partition`.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="7b0ea-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="7b0ea-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="7b0ea-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b0ea-182">Next steps</span></span>
* [<span data-ttu-id="7b0ea-183">Deep dive on Service Fabric health</span><span class="sxs-lookup"><span data-stu-id="7b0ea-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="7b0ea-184">REST API for reporting service health</span><span class="sxs-lookup"><span data-stu-id="7b0ea-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="7b0ea-185">REST API for reporting application health</span><span class="sxs-lookup"><span data-stu-id="7b0ea-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)








