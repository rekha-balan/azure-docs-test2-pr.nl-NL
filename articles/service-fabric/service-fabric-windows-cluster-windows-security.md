---
title: Secure a cluster running on Windows by using Windows security | Microsoft Docs
description: Learn how to configure node-to-node and client-to-node security on a standalone cluster running on Windows by using Windows security.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/17/2017
ms.author: ryanwi
ms.openlocfilehash: b8842047351da6fdb547e0b09492b89fad962bee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555076"
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="84970-103">Secure a standalone cluster on Windows by using Windows security</span><span class="sxs-lookup"><span data-stu-id="84970-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="84970-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span><span class="sxs-lookup"><span data-stu-id="84970-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="84970-105">Security is especially important when the cluster runs production workloads.</span><span class="sxs-lookup"><span data-stu-id="84970-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="84970-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span><span class="sxs-lookup"><span data-stu-id="84970-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="84970-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="84970-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="84970-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="84970-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="84970-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span><span class="sxs-lookup"><span data-stu-id="84970-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="84970-110">To change the security selection, you have to rebuild the full cluster.</span><span class="sxs-lookup"><span data-stu-id="84970-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="84970-111">Configure Windows security using gMSA</span><span class="sxs-lookup"><span data-stu-id="84970-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="84970-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="84970-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "ServerCredentialType": "Windows",  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="84970-113">**Configuration Setting**</span><span class="sxs-lookup"><span data-stu-id="84970-113">**Configuration Setting**</span></span> | <span data-ttu-id="84970-114">**Description**</span><span class="sxs-lookup"><span data-stu-id="84970-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="84970-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="84970-115">WindowsIdentities</span></span> |<span data-ttu-id="84970-116">Contains the cluster and client identities.</span><span class="sxs-lookup"><span data-stu-id="84970-116">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="84970-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="84970-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="84970-118">Configures node-to-node security.</span><span class="sxs-lookup"><span data-stu-id="84970-118">Configures node-to-node security.</span></span> <span data-ttu-id="84970-119">A group managed service account.</span><span class="sxs-lookup"><span data-stu-id="84970-119">A group managed service account.</span></span> |  
| <span data-ttu-id="84970-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="84970-120">ClusterSPN</span></span> |<span data-ttu-id="84970-121">Fully qualified domain SPN for gMSA account</span><span class="sxs-lookup"><span data-stu-id="84970-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="84970-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="84970-122">ClientIdentities</span></span> |<span data-ttu-id="84970-123">Configures client-to-node security.</span><span class="sxs-lookup"><span data-stu-id="84970-123">Configures client-to-node security.</span></span> <span data-ttu-id="84970-124">An array of client user accounts.</span><span class="sxs-lookup"><span data-stu-id="84970-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="84970-125">Identity</span><span class="sxs-lookup"><span data-stu-id="84970-125">Identity</span></span> |<span data-ttu-id="84970-126">The client identity, a domain user.</span><span class="sxs-lookup"><span data-stu-id="84970-126">The client identity, a domain user.</span></span> |  
| <span data-ttu-id="84970-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="84970-127">IsAdmin</span></span> |<span data-ttu-id="84970-128">True specifies that the domain user has administrator client access, false for user client access.</span><span class="sxs-lookup"><span data-stu-id="84970-128">True specifies that the domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="84970-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span><span class="sxs-lookup"><span data-stu-id="84970-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="84970-130">In order to build trust relationships between nodes, they must be made aware of each other.</span><span class="sxs-lookup"><span data-stu-id="84970-130">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="84970-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="84970-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="84970-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span><span class="sxs-lookup"><span data-stu-id="84970-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="84970-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span><span class="sxs-lookup"><span data-stu-id="84970-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="84970-134">These accounts are also useful for automatic password management.</span><span class="sxs-lookup"><span data-stu-id="84970-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="84970-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="84970-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="84970-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="84970-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="84970-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span><span class="sxs-lookup"><span data-stu-id="84970-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="84970-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span><span class="sxs-lookup"><span data-stu-id="84970-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="84970-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span><span class="sxs-lookup"><span data-stu-id="84970-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="84970-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span><span class="sxs-lookup"><span data-stu-id="84970-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="84970-141">Administrators have full access to management capabilities (including read/write capabilities).</span><span class="sxs-lookup"><span data-stu-id="84970-141">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="84970-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span><span class="sxs-lookup"><span data-stu-id="84970-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="84970-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="84970-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="84970-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span><span class="sxs-lookup"><span data-stu-id="84970-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="84970-145">Configure Windows security using a machine group</span><span class="sxs-lookup"><span data-stu-id="84970-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="84970-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span><span class="sxs-lookup"><span data-stu-id="84970-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="84970-147">Windows security is configured in the **Properties** section:</span><span class="sxs-lookup"><span data-stu-id="84970-147">Windows security is configured in the **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="84970-148">**Configuration setting**</span><span class="sxs-lookup"><span data-stu-id="84970-148">**Configuration setting**</span></span> | <span data-ttu-id="84970-149">**Description**</span><span class="sxs-lookup"><span data-stu-id="84970-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="84970-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="84970-150">ClusterCredentialType</span></span> |<span data-ttu-id="84970-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span><span class="sxs-lookup"><span data-stu-id="84970-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="84970-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="84970-152">ServerCredentialType</span></span> |<span data-ttu-id="84970-153">Set to *Windows* to enable Windows security for clients.</span><span class="sxs-lookup"><span data-stu-id="84970-153">Set to *Windows* to enable Windows security for clients.</span></span><br /><br /><span data-ttu-id="84970-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="84970-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="84970-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="84970-155">WindowsIdentities</span></span> |<span data-ttu-id="84970-156">Contains the cluster and client identities.</span><span class="sxs-lookup"><span data-stu-id="84970-156">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="84970-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="84970-157">ClusterIdentity</span></span> |<span data-ttu-id="84970-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span><span class="sxs-lookup"><span data-stu-id="84970-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="84970-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="84970-159">ClientIdentities</span></span> |<span data-ttu-id="84970-160">Configures client-to-node security.</span><span class="sxs-lookup"><span data-stu-id="84970-160">Configures client-to-node security.</span></span> <span data-ttu-id="84970-161">An array of client user accounts.</span><span class="sxs-lookup"><span data-stu-id="84970-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="84970-162">Identity</span><span class="sxs-lookup"><span data-stu-id="84970-162">Identity</span></span> |<span data-ttu-id="84970-163">Add the domain user, domain\username, for the client identity.</span><span class="sxs-lookup"><span data-stu-id="84970-163">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="84970-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="84970-164">IsAdmin</span></span> |<span data-ttu-id="84970-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span><span class="sxs-lookup"><span data-stu-id="84970-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="84970-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span><span class="sxs-lookup"><span data-stu-id="84970-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="84970-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="84970-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="84970-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="84970-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="84970-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span><span class="sxs-lookup"><span data-stu-id="84970-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="84970-170">You can establish trust in two different ways:</span><span class="sxs-lookup"><span data-stu-id="84970-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="84970-171">Specify the domain group users that can connect.</span><span class="sxs-lookup"><span data-stu-id="84970-171">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="84970-172">Specify the domain node users that can connect.</span><span class="sxs-lookup"><span data-stu-id="84970-172">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="84970-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span><span class="sxs-lookup"><span data-stu-id="84970-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="84970-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span><span class="sxs-lookup"><span data-stu-id="84970-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="84970-175">Administrators have full access to management capabilities (including read/write capabilities).</span><span class="sxs-lookup"><span data-stu-id="84970-175">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="84970-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span><span class="sxs-lookup"><span data-stu-id="84970-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="84970-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span><span class="sxs-lookup"><span data-stu-id="84970-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="84970-178">Service Fabric should not be deployed on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="84970-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="84970-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span><span class="sxs-lookup"><span data-stu-id="84970-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="84970-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="84970-180">Next steps</span></span>
<span data-ttu-id="84970-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="84970-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="84970-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="84970-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="84970-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span><span class="sxs-lookup"><span data-stu-id="84970-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
