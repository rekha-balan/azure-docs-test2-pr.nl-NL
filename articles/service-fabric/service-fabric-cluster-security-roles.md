---
title: 'Service Fabric cluster security: client roles | Microsoft Docs'
description: This article describes the two client roles and the permissions provided to the roles.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: ''
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
ms.openlocfilehash: 09ddabf97028525e04f930f935f6ddf7ae132567
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552528"
---
# <a name="role-based-access-control-for-service-fabric-clients"></a><span data-ttu-id="6f6d1-103">Role-based access control for Service Fabric clients</span><span class="sxs-lookup"><span data-stu-id="6f6d1-103">Role-based access control for Service Fabric clients</span></span>
<span data-ttu-id="6f6d1-104">Azure Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-104">Azure Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="6f6d1-105">Access control allows the cluster administrator to limit access to certain cluster operations for different groups of users, making the cluster more secure.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-105">Access control allows the cluster administrator to limit access to certain cluster operations for different groups of users, making the cluster more secure.</span></span>  

<span data-ttu-id="6f6d1-106">**Administrators** have full access to management capabilities (including read/write capabilities).</span><span class="sxs-lookup"><span data-stu-id="6f6d1-106">**Administrators** have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="6f6d1-107">By default, **users** only have read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-107">By default, **users** only have read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>

<span data-ttu-id="6f6d1-108">You specify the two client roles (administrator and client) at the time of cluster creation by providing separate certificates for each.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-108">You specify the two client roles (administrator and client) at the time of cluster creation by providing separate certificates for each.</span></span> <span data-ttu-id="6f6d1-109">See [Service Fabric cluster security](service-fabric-cluster-security.md) for details on setting up a secure Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-109">See [Service Fabric cluster security](service-fabric-cluster-security.md) for details on setting up a secure Service Fabric cluster.</span></span>

## <a name="default-access-control-settings"></a><span data-ttu-id="6f6d1-110">Default access control settings</span><span class="sxs-lookup"><span data-stu-id="6f6d1-110">Default access control settings</span></span>
<span data-ttu-id="6f6d1-111">The administrator access control type has full access to all the FabricClient APIs.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-111">The administrator access control type has full access to all the FabricClient APIs.</span></span> <span data-ttu-id="6f6d1-112">It can perform any reads and writes on the Service Fabric cluster, including the following operations:</span><span class="sxs-lookup"><span data-stu-id="6f6d1-112">It can perform any reads and writes on the Service Fabric cluster, including the following operations:</span></span>

### <a name="application-and-service-operations"></a><span data-ttu-id="6f6d1-113">Application and service operations</span><span class="sxs-lookup"><span data-stu-id="6f6d1-113">Application and service operations</span></span>
* <span data-ttu-id="6f6d1-114">**CreateService**: service creation</span><span class="sxs-lookup"><span data-stu-id="6f6d1-114">**CreateService**: service creation</span></span>                             
* <span data-ttu-id="6f6d1-115">**CreateServiceFromTemplate**: service creation from template</span><span class="sxs-lookup"><span data-stu-id="6f6d1-115">**CreateServiceFromTemplate**: service creation from template</span></span>                             
* <span data-ttu-id="6f6d1-116">**UpdateService**: service updates</span><span class="sxs-lookup"><span data-stu-id="6f6d1-116">**UpdateService**: service updates</span></span>                             
* <span data-ttu-id="6f6d1-117">**DeleteService**: service deletion</span><span class="sxs-lookup"><span data-stu-id="6f6d1-117">**DeleteService**: service deletion</span></span>                             
* <span data-ttu-id="6f6d1-118">**ProvisionApplicationType**: application type provisioning</span><span class="sxs-lookup"><span data-stu-id="6f6d1-118">**ProvisionApplicationType**: application type provisioning</span></span>                             
* <span data-ttu-id="6f6d1-119">**CreateApplication**: application creation</span><span class="sxs-lookup"><span data-stu-id="6f6d1-119">**CreateApplication**: application creation</span></span>                               
* <span data-ttu-id="6f6d1-120">**DeleteApplication**: application deletion</span><span class="sxs-lookup"><span data-stu-id="6f6d1-120">**DeleteApplication**: application deletion</span></span>                             
* <span data-ttu-id="6f6d1-121">**UpgradeApplication**: starting or interrupting application upgrades</span><span class="sxs-lookup"><span data-stu-id="6f6d1-121">**UpgradeApplication**: starting or interrupting application upgrades</span></span>                             
* <span data-ttu-id="6f6d1-122">**UnprovisionApplicationType**: application type unprovisioning</span><span class="sxs-lookup"><span data-stu-id="6f6d1-122">**UnprovisionApplicationType**: application type unprovisioning</span></span>                             
* <span data-ttu-id="6f6d1-123">**MoveNextUpgradeDomain**: resuming application upgrades with an explicit update domain</span><span class="sxs-lookup"><span data-stu-id="6f6d1-123">**MoveNextUpgradeDomain**: resuming application upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="6f6d1-124">**ReportUpgradeHealth**: resuming application upgrades with the current upgrade progress</span><span class="sxs-lookup"><span data-stu-id="6f6d1-124">**ReportUpgradeHealth**: resuming application upgrades with the current upgrade progress</span></span>                             
* <span data-ttu-id="6f6d1-125">**ReportHealth**: reporting health</span><span class="sxs-lookup"><span data-stu-id="6f6d1-125">**ReportHealth**: reporting health</span></span>                             
* <span data-ttu-id="6f6d1-126">**PredeployPackageToNode**: predeployment API</span><span class="sxs-lookup"><span data-stu-id="6f6d1-126">**PredeployPackageToNode**: predeployment API</span></span>                            
* <span data-ttu-id="6f6d1-127">**CodePackageControl**: restarting code packages</span><span class="sxs-lookup"><span data-stu-id="6f6d1-127">**CodePackageControl**: restarting code packages</span></span>                             
* <span data-ttu-id="6f6d1-128">**RecoverPartition**: recovering a partition</span><span class="sxs-lookup"><span data-stu-id="6f6d1-128">**RecoverPartition**: recovering a partition</span></span>                             
* <span data-ttu-id="6f6d1-129">**RecoverPartitions**: recovering partitions</span><span class="sxs-lookup"><span data-stu-id="6f6d1-129">**RecoverPartitions**: recovering partitions</span></span>                             
* <span data-ttu-id="6f6d1-130">**RecoverServicePartitions**: recovering service partitions</span><span class="sxs-lookup"><span data-stu-id="6f6d1-130">**RecoverServicePartitions**: recovering service partitions</span></span>                             
* <span data-ttu-id="6f6d1-131">**RecoverSystemPartitions**: recovering system service partitions</span><span class="sxs-lookup"><span data-stu-id="6f6d1-131">**RecoverSystemPartitions**: recovering system service partitions</span></span>                             

### <a name="cluster-operations"></a><span data-ttu-id="6f6d1-132">Cluster operations</span><span class="sxs-lookup"><span data-stu-id="6f6d1-132">Cluster operations</span></span>
* <span data-ttu-id="6f6d1-133">**ProvisionFabric**: MSI and/or cluster manifest provisioning</span><span class="sxs-lookup"><span data-stu-id="6f6d1-133">**ProvisionFabric**: MSI and/or cluster manifest provisioning</span></span>                             
* <span data-ttu-id="6f6d1-134">**UpgradeFabric**: starting cluster upgrades</span><span class="sxs-lookup"><span data-stu-id="6f6d1-134">**UpgradeFabric**: starting cluster upgrades</span></span>                             
* <span data-ttu-id="6f6d1-135">**UnprovisionFabric**: MSI and/or cluster manifest unprovisioning</span><span class="sxs-lookup"><span data-stu-id="6f6d1-135">**UnprovisionFabric**: MSI and/or cluster manifest unprovisioning</span></span>                         
* <span data-ttu-id="6f6d1-136">**MoveNextFabricUpgradeDomain**: resuming cluster upgrades with an explicit update domain</span><span class="sxs-lookup"><span data-stu-id="6f6d1-136">**MoveNextFabricUpgradeDomain**: resuming cluster upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="6f6d1-137">**ReportFabricUpgradeHealth**: resuming cluster upgrades with the current upgrade progress</span><span class="sxs-lookup"><span data-stu-id="6f6d1-137">**ReportFabricUpgradeHealth**: resuming cluster upgrades with the current upgrade progress</span></span>                             
* <span data-ttu-id="6f6d1-138">**StartInfrastructureTask**: starting infrastructure tasks</span><span class="sxs-lookup"><span data-stu-id="6f6d1-138">**StartInfrastructureTask**: starting infrastructure tasks</span></span>                             
* <span data-ttu-id="6f6d1-139">**FinishInfrastructureTask**: finishing infrastructure tasks</span><span class="sxs-lookup"><span data-stu-id="6f6d1-139">**FinishInfrastructureTask**: finishing infrastructure tasks</span></span>                             
* <span data-ttu-id="6f6d1-140">**InvokeInfrastructureCommand**: infrastructure task management commands</span><span class="sxs-lookup"><span data-stu-id="6f6d1-140">**InvokeInfrastructureCommand**: infrastructure task management commands</span></span>                              
* <span data-ttu-id="6f6d1-141">**ActivateNode**: activating a node</span><span class="sxs-lookup"><span data-stu-id="6f6d1-141">**ActivateNode**: activating a node</span></span>                             
* <span data-ttu-id="6f6d1-142">**DeactivateNode**: deactivating a node</span><span class="sxs-lookup"><span data-stu-id="6f6d1-142">**DeactivateNode**: deactivating a node</span></span>                             
* <span data-ttu-id="6f6d1-143">**DeactivateNodesBatch**: deactivating multiple nodes</span><span class="sxs-lookup"><span data-stu-id="6f6d1-143">**DeactivateNodesBatch**: deactivating multiple nodes</span></span>                             
* <span data-ttu-id="6f6d1-144">**RemoveNodeDeactivations**: reverting deactivation on multiple nodes</span><span class="sxs-lookup"><span data-stu-id="6f6d1-144">**RemoveNodeDeactivations**: reverting deactivation on multiple nodes</span></span>                             
* <span data-ttu-id="6f6d1-145">**GetNodeDeactivationStatus**: checking deactivation status</span><span class="sxs-lookup"><span data-stu-id="6f6d1-145">**GetNodeDeactivationStatus**: checking deactivation status</span></span>                             
* <span data-ttu-id="6f6d1-146">**NodeStateRemoved**: reporting node state removed</span><span class="sxs-lookup"><span data-stu-id="6f6d1-146">**NodeStateRemoved**: reporting node state removed</span></span>                             
* <span data-ttu-id="6f6d1-147">**ReportFault**: reporting fault</span><span class="sxs-lookup"><span data-stu-id="6f6d1-147">**ReportFault**: reporting fault</span></span>                             
* <span data-ttu-id="6f6d1-148">**FileContent**: image store client file transfer (external to cluster)</span><span class="sxs-lookup"><span data-stu-id="6f6d1-148">**FileContent**: image store client file transfer (external to cluster)</span></span>                             
* <span data-ttu-id="6f6d1-149">**FileDownload**: image store client file download initiation (external to cluster)</span><span class="sxs-lookup"><span data-stu-id="6f6d1-149">**FileDownload**: image store client file download initiation (external to cluster)</span></span>                             
* <span data-ttu-id="6f6d1-150">**InternalList**: image store client file list operation (internal)</span><span class="sxs-lookup"><span data-stu-id="6f6d1-150">**InternalList**: image store client file list operation (internal)</span></span>                             
* <span data-ttu-id="6f6d1-151">**Delete**: image store client delete operation</span><span class="sxs-lookup"><span data-stu-id="6f6d1-151">**Delete**: image store client delete operation</span></span>                              
* <span data-ttu-id="6f6d1-152">**Upload**: image store client upload operation</span><span class="sxs-lookup"><span data-stu-id="6f6d1-152">**Upload**: image store client upload operation</span></span>                             
* <span data-ttu-id="6f6d1-153">**NodeControl**: starting, stopping, and restarting nodes</span><span class="sxs-lookup"><span data-stu-id="6f6d1-153">**NodeControl**: starting, stopping, and restarting nodes</span></span>                             
* <span data-ttu-id="6f6d1-154">**MoveReplicaControl**: moving replicas from one node to another</span><span class="sxs-lookup"><span data-stu-id="6f6d1-154">**MoveReplicaControl**: moving replicas from one node to another</span></span>                             

### <a name="miscellaneous-operations"></a><span data-ttu-id="6f6d1-155">Miscellaneous operations</span><span class="sxs-lookup"><span data-stu-id="6f6d1-155">Miscellaneous operations</span></span>
* <span data-ttu-id="6f6d1-156">**Ping**: client pings</span><span class="sxs-lookup"><span data-stu-id="6f6d1-156">**Ping**: client pings</span></span>                             
* <span data-ttu-id="6f6d1-157">**Query**: all queries allowed</span><span class="sxs-lookup"><span data-stu-id="6f6d1-157">**Query**: all queries allowed</span></span>
* <span data-ttu-id="6f6d1-158">**NameExists**: naming URI existence checks</span><span class="sxs-lookup"><span data-stu-id="6f6d1-158">**NameExists**: naming URI existence checks</span></span>                             

<span data-ttu-id="6f6d1-159">The user access control type is, by default, limited to the following operations:</span><span class="sxs-lookup"><span data-stu-id="6f6d1-159">The user access control type is, by default, limited to the following operations:</span></span> 

* <span data-ttu-id="6f6d1-160">**EnumerateSubnames**: naming URI enumeration</span><span class="sxs-lookup"><span data-stu-id="6f6d1-160">**EnumerateSubnames**: naming URI enumeration</span></span>                             
* <span data-ttu-id="6f6d1-161">**EnumerateProperties**: naming property enumeration</span><span class="sxs-lookup"><span data-stu-id="6f6d1-161">**EnumerateProperties**: naming property enumeration</span></span>                             
* <span data-ttu-id="6f6d1-162">**PropertyReadBatch**: naming property read operations</span><span class="sxs-lookup"><span data-stu-id="6f6d1-162">**PropertyReadBatch**: naming property read operations</span></span>                             
* <span data-ttu-id="6f6d1-163">**GetServiceDescription**: long-poll service notifications and reading service descriptions</span><span class="sxs-lookup"><span data-stu-id="6f6d1-163">**GetServiceDescription**: long-poll service notifications and reading service descriptions</span></span>                             
* <span data-ttu-id="6f6d1-164">**ResolveService**: complaint-based service resolution</span><span class="sxs-lookup"><span data-stu-id="6f6d1-164">**ResolveService**: complaint-based service resolution</span></span>                             
* <span data-ttu-id="6f6d1-165">**ResolveNameOwner**: resolving naming URI owner</span><span class="sxs-lookup"><span data-stu-id="6f6d1-165">**ResolveNameOwner**: resolving naming URI owner</span></span>                             
* <span data-ttu-id="6f6d1-166">**ResolvePartition**: resolving system services</span><span class="sxs-lookup"><span data-stu-id="6f6d1-166">**ResolvePartition**: resolving system services</span></span>                             
* <span data-ttu-id="6f6d1-167">**ServiceNotifications**: event-based service notifications</span><span class="sxs-lookup"><span data-stu-id="6f6d1-167">**ServiceNotifications**: event-based service notifications</span></span>                             
* <span data-ttu-id="6f6d1-168">**GetUpgradeStatus**: polling application upgrade status</span><span class="sxs-lookup"><span data-stu-id="6f6d1-168">**GetUpgradeStatus**: polling application upgrade status</span></span>                             
* <span data-ttu-id="6f6d1-169">**GetFabricUpgradeStatus**: polling cluster upgrade status</span><span class="sxs-lookup"><span data-stu-id="6f6d1-169">**GetFabricUpgradeStatus**: polling cluster upgrade status</span></span>                             
* <span data-ttu-id="6f6d1-170">**InvokeInfrastructureQuery**: querying infrastructure tasks</span><span class="sxs-lookup"><span data-stu-id="6f6d1-170">**InvokeInfrastructureQuery**: querying infrastructure tasks</span></span>                             
* <span data-ttu-id="6f6d1-171">**List**: image store client file list operation</span><span class="sxs-lookup"><span data-stu-id="6f6d1-171">**List**: image store client file list operation</span></span>                             
* <span data-ttu-id="6f6d1-172">**ResetPartitionLoad**: resetting load for a failover unit</span><span class="sxs-lookup"><span data-stu-id="6f6d1-172">**ResetPartitionLoad**: resetting load for a failover unit</span></span>                             
* <span data-ttu-id="6f6d1-173">**ToggleVerboseServicePlacementHealthReporting**: toggling verbose service placement health reporting</span><span class="sxs-lookup"><span data-stu-id="6f6d1-173">**ToggleVerboseServicePlacementHealthReporting**: toggling verbose service placement health reporting</span></span>                             

<span data-ttu-id="6f6d1-174">The admin access control also has access to the preceding operations.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-174">The admin access control also has access to the preceding operations.</span></span>

## <a name="changing-default-settings-for-client-roles"></a><span data-ttu-id="6f6d1-175">Changing default settings for client roles</span><span class="sxs-lookup"><span data-stu-id="6f6d1-175">Changing default settings for client roles</span></span>
<span data-ttu-id="6f6d1-176">In the cluster manifest file, you can provide admin capabilities to the client if needed.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-176">In the cluster manifest file, you can provide admin capabilities to the client if needed.</span></span> <span data-ttu-id="6f6d1-177">You can change the defaults by going to the **Fabric Settings** option during [cluster creation](service-fabric-cluster-creation-via-portal.md), and providing the preceding settings in the **name**, **admin**, **user**, and **value** fields.</span><span class="sxs-lookup"><span data-stu-id="6f6d1-177">You can change the defaults by going to the **Fabric Settings** option during [cluster creation](service-fabric-cluster-creation-via-portal.md), and providing the preceding settings in the **name**, **admin**, **user**, and **value** fields.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f6d1-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f6d1-178">Next steps</span></span>
[<span data-ttu-id="6f6d1-179">Service Fabric cluster security</span><span class="sxs-lookup"><span data-stu-id="6f6d1-179">Service Fabric cluster security</span></span>](service-fabric-cluster-security.md)

[<span data-ttu-id="6f6d1-180">Service Fabric cluster creation</span><span class="sxs-lookup"><span data-stu-id="6f6d1-180">Service Fabric cluster creation</span></span>](service-fabric-cluster-creation-via-portal.md)

