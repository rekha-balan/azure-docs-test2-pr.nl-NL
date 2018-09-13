---
title: Secure a cluster running on Windows by using Windows security | Microsoft Docs
description: Learn how to configure node-to-node and client-to-node security on a standalone cluster running on Windows by using Windows security.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: ''
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: a94891b8a88873f91cd82632c45971524e8c8e41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818147"
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="9559c-103">Secure a standalone cluster on Windows by using Windows security</span><span class="sxs-lookup"><span data-stu-id="9559c-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="9559c-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span><span class="sxs-lookup"><span data-stu-id="9559c-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="9559c-105">Security is especially important when the cluster runs production workloads.</span><span class="sxs-lookup"><span data-stu-id="9559c-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="9559c-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span><span class="sxs-lookup"><span data-stu-id="9559c-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="9559c-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9559c-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="9559c-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="9559c-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9559c-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span><span class="sxs-lookup"><span data-stu-id="9559c-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="9559c-110">To change the security selection, you have to rebuild the full cluster.</span><span class="sxs-lookup"><span data-stu-id="9559c-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="9559c-111">Configure Windows security using gMSA</span><span class="sxs-lookup"><span data-stu-id="9559c-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="9559c-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="9559c-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "[gMSA Identity]", 
                "ClusterSPN": "[Registered SPN for the gMSA account]",
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  

| <span data-ttu-id="9559c-113">**Configuration setting**</span><span class="sxs-lookup"><span data-stu-id="9559c-113">**Configuration setting**</span></span> | <span data-ttu-id="9559c-114">**Description**</span><span class="sxs-lookup"><span data-stu-id="9559c-114">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9559c-115">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="9559c-115">ClusterCredentialType</span></span> |<span data-ttu-id="9559c-116">Set to *Windows* to enable Windows security for node-node communication.</span><span class="sxs-lookup"><span data-stu-id="9559c-116">Set to *Windows* to enable Windows security for node-node communication.</span></span>  | 
| <span data-ttu-id="9559c-117">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="9559c-117">ServerCredentialType</span></span> |<span data-ttu-id="9559c-118">Set to *Windows* to enable Windows security for client-node communication.</span><span class="sxs-lookup"><span data-stu-id="9559c-118">Set to *Windows* to enable Windows security for client-node communication.</span></span> |  
| <span data-ttu-id="9559c-119">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="9559c-119">WindowsIdentities</span></span> |<span data-ttu-id="9559c-120">Contains the cluster and client identities.</span><span class="sxs-lookup"><span data-stu-id="9559c-120">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="9559c-121">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="9559c-121">ClustergMSAIdentity</span></span> |<span data-ttu-id="9559c-122">Configures node-to-node security.</span><span class="sxs-lookup"><span data-stu-id="9559c-122">Configures node-to-node security.</span></span> <span data-ttu-id="9559c-123">A group managed service account.</span><span class="sxs-lookup"><span data-stu-id="9559c-123">A group managed service account.</span></span> |  
| <span data-ttu-id="9559c-124">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="9559c-124">ClusterSPN</span></span> |<span data-ttu-id="9559c-125">Registered SPN for gMSA account</span><span class="sxs-lookup"><span data-stu-id="9559c-125">Registered SPN for gMSA account</span></span>|  
| <span data-ttu-id="9559c-126">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="9559c-126">ClientIdentities</span></span> |<span data-ttu-id="9559c-127">Configures client-to-node security.</span><span class="sxs-lookup"><span data-stu-id="9559c-127">Configures client-to-node security.</span></span> <span data-ttu-id="9559c-128">An array of client user accounts.</span><span class="sxs-lookup"><span data-stu-id="9559c-128">An array of client user accounts.</span></span> | 
| <span data-ttu-id="9559c-129">Identity</span><span class="sxs-lookup"><span data-stu-id="9559c-129">Identity</span></span> |<span data-ttu-id="9559c-130">Add the domain user, domain\username, for the client identity.</span><span class="sxs-lookup"><span data-stu-id="9559c-130">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="9559c-131">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="9559c-131">IsAdmin</span></span> |<span data-ttu-id="9559c-132">Set to true to specify that the domain user has administrator client access or false for user client access.</span><span class="sxs-lookup"><span data-stu-id="9559c-132">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="9559c-133">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span><span class="sxs-lookup"><span data-stu-id="9559c-133">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="9559c-134">In order to build trust relationships between nodes, they must be made aware of each other.</span><span class="sxs-lookup"><span data-stu-id="9559c-134">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="9559c-135">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9559c-135">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="9559c-136">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span><span class="sxs-lookup"><span data-stu-id="9559c-136">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="9559c-137">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span><span class="sxs-lookup"><span data-stu-id="9559c-137">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="9559c-138">These accounts are also useful for automatic password management.</span><span class="sxs-lookup"><span data-stu-id="9559c-138">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="9559c-139">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="9559c-139">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="9559c-140">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="9559c-140">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="9559c-141">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span><span class="sxs-lookup"><span data-stu-id="9559c-141">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="9559c-142">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span><span class="sxs-lookup"><span data-stu-id="9559c-142">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="9559c-143">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span><span class="sxs-lookup"><span data-stu-id="9559c-143">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="9559c-144">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span><span class="sxs-lookup"><span data-stu-id="9559c-144">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="9559c-145">Administrators have full access to management capabilities (including read/write capabilities).</span><span class="sxs-lookup"><span data-stu-id="9559c-145">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="9559c-146">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span><span class="sxs-lookup"><span data-stu-id="9559c-146">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="9559c-147">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9559c-147">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="9559c-148">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span><span class="sxs-lookup"><span data-stu-id="9559c-148">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {
    "ClusterCredentialType": "Windows",            
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "http/servicefabric/clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="9559c-149">Configure Windows security using a machine group</span><span class="sxs-lookup"><span data-stu-id="9559c-149">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="9559c-150">This model is being deprecated.</span><span class="sxs-lookup"><span data-stu-id="9559c-150">This model is being deprecated.</span></span> <span data-ttu-id="9559c-151">The recommendation is to use gMSA as detailed above.</span><span class="sxs-lookup"><span data-stu-id="9559c-151">The recommendation is to use gMSA as detailed above.</span></span> <span data-ttu-id="9559c-152">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span><span class="sxs-lookup"><span data-stu-id="9559c-152">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="9559c-153">Windows security is configured in the **Properties** section:</span><span class="sxs-lookup"><span data-stu-id="9559c-153">Windows security is configured in the **Properties** section:</span></span> 

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

| <span data-ttu-id="9559c-154">**Configuration setting**</span><span class="sxs-lookup"><span data-stu-id="9559c-154">**Configuration setting**</span></span> | <span data-ttu-id="9559c-155">**Description**</span><span class="sxs-lookup"><span data-stu-id="9559c-155">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9559c-156">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="9559c-156">ClusterCredentialType</span></span> |<span data-ttu-id="9559c-157">Set to *Windows* to enable Windows security for node-node communication.</span><span class="sxs-lookup"><span data-stu-id="9559c-157">Set to *Windows* to enable Windows security for node-node communication.</span></span>  | 
| <span data-ttu-id="9559c-158">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="9559c-158">ServerCredentialType</span></span> |<span data-ttu-id="9559c-159">Set to *Windows* to enable Windows security for client-node communication.</span><span class="sxs-lookup"><span data-stu-id="9559c-159">Set to *Windows* to enable Windows security for client-node communication.</span></span> |  
| <span data-ttu-id="9559c-160">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="9559c-160">WindowsIdentities</span></span> |<span data-ttu-id="9559c-161">Contains the cluster and client identities.</span><span class="sxs-lookup"><span data-stu-id="9559c-161">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="9559c-162">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="9559c-162">ClusterIdentity</span></span> |<span data-ttu-id="9559c-163">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span><span class="sxs-lookup"><span data-stu-id="9559c-163">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="9559c-164">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="9559c-164">ClientIdentities</span></span> |<span data-ttu-id="9559c-165">Configures client-to-node security.</span><span class="sxs-lookup"><span data-stu-id="9559c-165">Configures client-to-node security.</span></span> <span data-ttu-id="9559c-166">An array of client user accounts.</span><span class="sxs-lookup"><span data-stu-id="9559c-166">An array of client user accounts.</span></span> |  
| <span data-ttu-id="9559c-167">Identity</span><span class="sxs-lookup"><span data-stu-id="9559c-167">Identity</span></span> |<span data-ttu-id="9559c-168">Add the domain user, domain\username, for the client identity.</span><span class="sxs-lookup"><span data-stu-id="9559c-168">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="9559c-169">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="9559c-169">IsAdmin</span></span> |<span data-ttu-id="9559c-170">Set to true to specify that the domain user has administrator client access or false for user client access.</span><span class="sxs-lookup"><span data-stu-id="9559c-170">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="9559c-171">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span><span class="sxs-lookup"><span data-stu-id="9559c-171">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="9559c-172">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="9559c-172">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="9559c-173">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="9559c-173">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="9559c-174">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span><span class="sxs-lookup"><span data-stu-id="9559c-174">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="9559c-175">You can establish trust in two different ways:</span><span class="sxs-lookup"><span data-stu-id="9559c-175">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="9559c-176">Specify the domain group users that can connect.</span><span class="sxs-lookup"><span data-stu-id="9559c-176">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="9559c-177">Specify the domain node users that can connect.</span><span class="sxs-lookup"><span data-stu-id="9559c-177">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="9559c-178">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span><span class="sxs-lookup"><span data-stu-id="9559c-178">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="9559c-179">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span><span class="sxs-lookup"><span data-stu-id="9559c-179">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="9559c-180">Administrators have full access to management capabilities (including read/write capabilities).</span><span class="sxs-lookup"><span data-stu-id="9559c-180">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="9559c-181">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span><span class="sxs-lookup"><span data-stu-id="9559c-181">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="9559c-182">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span><span class="sxs-lookup"><span data-stu-id="9559c-182">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

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
> <span data-ttu-id="9559c-183">Service Fabric should not be deployed on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="9559c-183">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="9559c-184">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span><span class="sxs-lookup"><span data-stu-id="9559c-184">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9559c-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="9559c-185">Next steps</span></span>
<span data-ttu-id="9559c-186">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9559c-186">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="9559c-187">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="9559c-187">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="9559c-188">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span><span class="sxs-lookup"><span data-stu-id="9559c-188">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
