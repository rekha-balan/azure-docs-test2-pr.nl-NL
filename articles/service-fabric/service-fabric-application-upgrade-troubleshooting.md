---
title: Troubleshooting application upgrades | Microsoft Docs
description: This article covers some common issues around upgrading a Service Fabric application and how to resolve them.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/23/2018
ms.author: subramar
ms.openlocfilehash: c6ba61354bf7466819e34a0d619a5a1820dd7b90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828958"
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="becae-103">Troubleshoot application upgrades</span><span class="sxs-lookup"><span data-stu-id="becae-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="becae-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="becae-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="becae-105">Troubleshoot a failed application upgrade</span><span class="sxs-lookup"><span data-stu-id="becae-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="becae-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span><span class="sxs-lookup"><span data-stu-id="becae-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="becae-107">The following list specifies how the additional information can be used:</span><span class="sxs-lookup"><span data-stu-id="becae-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="becae-108">Identify the failure type.</span><span class="sxs-lookup"><span data-stu-id="becae-108">Identify the failure type.</span></span>
2. <span data-ttu-id="becae-109">Identify the failure reason.</span><span class="sxs-lookup"><span data-stu-id="becae-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="becae-110">Isolate one or more failing components for further investigation.</span><span class="sxs-lookup"><span data-stu-id="becae-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="becae-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span><span class="sxs-lookup"><span data-stu-id="becae-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="becae-112">Identify the failure type</span><span class="sxs-lookup"><span data-stu-id="becae-112">Identify the failure type</span></span>
<span data-ttu-id="becae-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span><span class="sxs-lookup"><span data-stu-id="becae-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="becae-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span><span class="sxs-lookup"><span data-stu-id="becae-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="becae-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span><span class="sxs-lookup"><span data-stu-id="becae-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="becae-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span><span class="sxs-lookup"><span data-stu-id="becae-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="becae-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span><span class="sxs-lookup"><span data-stu-id="becae-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="becae-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span><span class="sxs-lookup"><span data-stu-id="becae-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="becae-119">Further information is displayed depending on the type of the failure.</span><span class="sxs-lookup"><span data-stu-id="becae-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="becae-120">Investigate upgrade timeouts</span><span class="sxs-lookup"><span data-stu-id="becae-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="becae-121">Upgrade timeout failures are most commonly caused by service availability issues.</span><span class="sxs-lookup"><span data-stu-id="becae-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="becae-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span><span class="sxs-lookup"><span data-stu-id="becae-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="becae-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span><span class="sxs-lookup"><span data-stu-id="becae-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="becae-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span><span class="sxs-lookup"><span data-stu-id="becae-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="becae-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span><span class="sxs-lookup"><span data-stu-id="becae-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="becae-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="becae-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="becae-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span><span class="sxs-lookup"><span data-stu-id="becae-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="becae-128">All this information points to a potential issue with the new version of the application code.</span><span class="sxs-lookup"><span data-stu-id="becae-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="becae-129">The most common issues are service errors in the open or promotion to primary code paths.</span><span class="sxs-lookup"><span data-stu-id="becae-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="becae-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span><span class="sxs-lookup"><span data-stu-id="becae-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="becae-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span><span class="sxs-lookup"><span data-stu-id="becae-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="becae-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span><span class="sxs-lookup"><span data-stu-id="becae-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="becae-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span><span class="sxs-lookup"><span data-stu-id="becae-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

<span data-ttu-id="becae-134">In rare cases, the **UpgradeDomainProgressAtFailure** field may be empty if the overall upgrade times out just as the system completes all work for the current upgrade domain.</span><span class="sxs-lookup"><span data-stu-id="becae-134">In rare cases, the **UpgradeDomainProgressAtFailure** field may be empty if the overall upgrade times out just as the system completes all work for the current upgrade domain.</span></span> <span data-ttu-id="becae-135">If this happens, try increasing the **UpgradeTimeout** and **UpgradeDomainTimeout** upgrade parameter values and retry the upgrade.</span><span class="sxs-lookup"><span data-stu-id="becae-135">If this happens, try increasing the **UpgradeTimeout** and **UpgradeDomainTimeout** upgrade parameter values and retry the upgrade.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="becae-136">Investigate health check failures</span><span class="sxs-lookup"><span data-stu-id="becae-136">Investigate health check failures</span></span>
<span data-ttu-id="becae-137">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span><span class="sxs-lookup"><span data-stu-id="becae-137">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="becae-138">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span><span class="sxs-lookup"><span data-stu-id="becae-138">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="becae-139">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="becae-139">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="becae-140">Investigating health check failures first requires an understanding of the Service Fabric health model.</span><span class="sxs-lookup"><span data-stu-id="becae-140">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="becae-141">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span><span class="sxs-lookup"><span data-stu-id="becae-141">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="becae-142">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="becae-142">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="becae-143">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span><span class="sxs-lookup"><span data-stu-id="becae-143">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="becae-144">This mode allows us to investigate the live system in the failed state before taking any further action.</span><span class="sxs-lookup"><span data-stu-id="becae-144">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="becae-145">Recover from a suspended upgrade</span><span class="sxs-lookup"><span data-stu-id="becae-145">Recover from a suspended upgrade</span></span>
<span data-ttu-id="becae-146">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span><span class="sxs-lookup"><span data-stu-id="becae-146">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="becae-147">With a manual **FailureAction**, there are several recovery options:</span><span class="sxs-lookup"><span data-stu-id="becae-147">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="becae-148">trigger a rollback</span><span class="sxs-lookup"><span data-stu-id="becae-148">trigger a rollback</span></span>
2. <span data-ttu-id="becae-149">Proceed through the remainder of the upgrade manually</span><span class="sxs-lookup"><span data-stu-id="becae-149">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="becae-150">Resume the monitored upgrade</span><span class="sxs-lookup"><span data-stu-id="becae-150">Resume the monitored upgrade</span></span>

<span data-ttu-id="becae-151">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span><span class="sxs-lookup"><span data-stu-id="becae-151">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="becae-152">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span><span class="sxs-lookup"><span data-stu-id="becae-152">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="becae-153">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span><span class="sxs-lookup"><span data-stu-id="becae-153">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="becae-154">In this mode, only safety checks are performed by the system.</span><span class="sxs-lookup"><span data-stu-id="becae-154">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="becae-155">No more health checks are performed.</span><span class="sxs-lookup"><span data-stu-id="becae-155">No more health checks are performed.</span></span> <span data-ttu-id="becae-156">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span><span class="sxs-lookup"><span data-stu-id="becae-156">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="becae-157">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span><span class="sxs-lookup"><span data-stu-id="becae-157">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="becae-158">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span><span class="sxs-lookup"><span data-stu-id="becae-158">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="becae-159">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span><span class="sxs-lookup"><span data-stu-id="becae-159">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="becae-160">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span><span class="sxs-lookup"><span data-stu-id="becae-160">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="becae-161">Further troubleshooting</span><span class="sxs-lookup"><span data-stu-id="becae-161">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="becae-162">Service Fabric is not following the specified health policies</span><span class="sxs-lookup"><span data-stu-id="becae-162">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="becae-163">Possible Cause 1:</span><span class="sxs-lookup"><span data-stu-id="becae-163">Possible Cause 1:</span></span>

<span data-ttu-id="becae-164">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span><span class="sxs-lookup"><span data-stu-id="becae-164">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="becae-165">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="becae-165">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="becae-166">Thus, health policies should be set accordingly.</span><span class="sxs-lookup"><span data-stu-id="becae-166">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="becae-167">Possible Cause 2:</span><span class="sxs-lookup"><span data-stu-id="becae-167">Possible Cause 2:</span></span>

<span data-ttu-id="becae-168">Health policies are specified in terms of percentages of total services and not specific service instances.</span><span class="sxs-lookup"><span data-stu-id="becae-168">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="becae-169">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span><span class="sxs-lookup"><span data-stu-id="becae-169">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="becae-170">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span><span class="sxs-lookup"><span data-stu-id="becae-170">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="becae-171">However, during the upgrade, D may become healthy while C becomes unhealthy.</span><span class="sxs-lookup"><span data-stu-id="becae-171">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="becae-172">The upgrade would still succeed because only 25% of the services are unhealthy.</span><span class="sxs-lookup"><span data-stu-id="becae-172">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="becae-173">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span><span class="sxs-lookup"><span data-stu-id="becae-173">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="becae-174">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span><span class="sxs-lookup"><span data-stu-id="becae-174">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="becae-175">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span><span class="sxs-lookup"><span data-stu-id="becae-175">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="becae-176">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span><span class="sxs-lookup"><span data-stu-id="becae-176">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="becae-177">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span><span class="sxs-lookup"><span data-stu-id="becae-177">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="becae-178">The policies specified as part of the API call only apply during the upgrade.</span><span class="sxs-lookup"><span data-stu-id="becae-178">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="becae-179">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span><span class="sxs-lookup"><span data-stu-id="becae-179">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="becae-180">Incorrect time-outs are specified</span><span class="sxs-lookup"><span data-stu-id="becae-180">Incorrect time-outs are specified</span></span>
<span data-ttu-id="becae-181">You may have wondered about what happens when time-outs are set inconsistently.</span><span class="sxs-lookup"><span data-stu-id="becae-181">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="becae-182">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="becae-182">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="becae-183">The answer is that an error is returned.</span><span class="sxs-lookup"><span data-stu-id="becae-183">The answer is that an error is returned.</span></span> <span data-ttu-id="becae-184">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="becae-184">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="becae-185">My upgrades are taking too long</span><span class="sxs-lookup"><span data-stu-id="becae-185">My upgrades are taking too long</span></span>
<span data-ttu-id="becae-186">The time for an upgrade to complete depends on the health checks and time-outs specified.</span><span class="sxs-lookup"><span data-stu-id="becae-186">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="becae-187">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span><span class="sxs-lookup"><span data-stu-id="becae-187">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="becae-188">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span><span class="sxs-lookup"><span data-stu-id="becae-188">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="becae-189">Here's a quick refresher on how the time-outs interact with the upgrade times:</span><span class="sxs-lookup"><span data-stu-id="becae-189">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="becae-190">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="becae-190">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="becae-191">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="becae-191">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="becae-192">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="becae-192">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="becae-193">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="becae-193">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="becae-194">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span><span class="sxs-lookup"><span data-stu-id="becae-194">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="becae-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="becae-195">Next steps</span></span>
<span data-ttu-id="becae-196">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="becae-196">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="becae-197">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="becae-197">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="becae-198">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="becae-198">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="becae-199">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="becae-199">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="becae-200">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="becae-200">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
