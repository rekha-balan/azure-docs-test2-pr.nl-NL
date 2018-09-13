---
title: Configure the upgrade of a Service Fabric application | Microsoft Docs
description: Learn how to configure the settings for upgrading a Service Fabric application by using Microsoft Visual Studio.
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 0104f5ce97152e05cae61d631a7eeaa9db561605
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662627"
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="45a12-103">Configure the upgrade of a Service Fabric application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45a12-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="45a12-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span><span class="sxs-lookup"><span data-stu-id="45a12-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="45a12-105">There are two advantages to upgrading your application to a newer version instead of replacing the application during testing and debugging:</span><span class="sxs-lookup"><span data-stu-id="45a12-105">There are two advantages to upgrading your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="45a12-106">Application data won't be lost during the upgrade.</span><span class="sxs-lookup"><span data-stu-id="45a12-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="45a12-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="45a12-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>

<span data-ttu-id="45a12-108">Tests can be run against an application while it's being upgraded.</span><span class="sxs-lookup"><span data-stu-id="45a12-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="45a12-109">Parameters needed to upgrade</span><span class="sxs-lookup"><span data-stu-id="45a12-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="45a12-110">You can choose from two types of deployment: regular or upgrade.</span><span class="sxs-lookup"><span data-stu-id="45a12-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="45a12-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span><span class="sxs-lookup"><span data-stu-id="45a12-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="45a12-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span><span class="sxs-lookup"><span data-stu-id="45a12-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="45a12-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span><span class="sxs-lookup"><span data-stu-id="45a12-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="45a12-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="45a12-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="45a12-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="45a12-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="45a12-116">A Monitored upgrade automates the upgrade and application health check.</span><span class="sxs-lookup"><span data-stu-id="45a12-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="45a12-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span><span class="sxs-lookup"><span data-stu-id="45a12-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="45a12-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span><span class="sxs-lookup"><span data-stu-id="45a12-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="45a12-119">Each upgrade mode requires different sets of parameters.</span><span class="sxs-lookup"><span data-stu-id="45a12-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="45a12-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span><span class="sxs-lookup"><span data-stu-id="45a12-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="45a12-121">Upgrade a Service Fabric application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45a12-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="45a12-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span><span class="sxs-lookup"><span data-stu-id="45a12-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="45a12-123">To configure the upgrade parameters</span><span class="sxs-lookup"><span data-stu-id="45a12-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="45a12-124">Click the **Settings** button next to the check box.</span><span class="sxs-lookup"><span data-stu-id="45a12-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="45a12-125">The **Edit Upgrade Parameters** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="45a12-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="45a12-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span><span class="sxs-lookup"><span data-stu-id="45a12-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="45a12-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span><span class="sxs-lookup"><span data-stu-id="45a12-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="45a12-128">Each parameter has default values.</span><span class="sxs-lookup"><span data-stu-id="45a12-128">Each parameter has default values.</span></span> <span data-ttu-id="45a12-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span><span class="sxs-lookup"><span data-stu-id="45a12-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="45a12-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="45a12-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="45a12-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span><span class="sxs-lookup"><span data-stu-id="45a12-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="45a12-132">Here's a real-life example:</span><span class="sxs-lookup"><span data-stu-id="45a12-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="45a12-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span><span class="sxs-lookup"><span data-stu-id="45a12-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="45a12-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span><span class="sxs-lookup"><span data-stu-id="45a12-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="45a12-135">Upgrade an application by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="45a12-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="45a12-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="45a12-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="45a12-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="45a12-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="45a12-138">Specify a health check policy in the application manifest file</span><span class="sxs-lookup"><span data-stu-id="45a12-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="45a12-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span><span class="sxs-lookup"><span data-stu-id="45a12-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="45a12-140">You can provide these parameter values in the application manifest file.</span><span class="sxs-lookup"><span data-stu-id="45a12-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="45a12-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="45a12-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="45a12-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="45a12-142">Next steps</span></span>
<span data-ttu-id="45a12-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="45a12-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>
