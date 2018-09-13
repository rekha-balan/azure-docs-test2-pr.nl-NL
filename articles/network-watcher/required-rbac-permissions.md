---
title: Permissions required to use Azure Network Watcher capabilities | Microsoft Docs
description: Learn which Azure role-based access control permissions are required to work with Network Watcher capabilities.
services: network-watcher
documentationcenter: ''
author: jimdial
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: network-watcher
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: jdial
ms.openlocfilehash: 7d0f0367a4126e7cecd34b39e6e5065e7d4fd90a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866367"
---
# <a name="role-based-access-control-permissions-required-to-use-network-watcher-capabilities"></a><span data-ttu-id="77193-103">Role-based access control permissions required to use Network Watcher capabilities</span><span class="sxs-lookup"><span data-stu-id="77193-103">Role-based access control permissions required to use Network Watcher capabilities</span></span>

<span data-ttu-id="77193-104">Azure role-based access control (RBAC) enables you to assign only the specific actions to members of your organization that they require to complete their assigned responsibilities.</span><span class="sxs-lookup"><span data-stu-id="77193-104">Azure role-based access control (RBAC) enables you to assign only the specific actions to members of your organization that they require to complete their assigned responsibilities.</span></span> <span data-ttu-id="77193-105">To use Network Watcher capabilities, the account you log into Azure with, must be assigned to the [Owner](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#owner), [Contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#contributor), or [Network contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#network-contributor) built-in roles, or assigned to a [custom role](../role-based-access-control/custom-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) that is assigned the actions listed for each Network Watcher capability in the sections that follow.</span><span class="sxs-lookup"><span data-stu-id="77193-105">To use Network Watcher capabilities, the account you log into Azure with, must be assigned to the [Owner](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#owner), [Contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#contributor), or [Network contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#network-contributor) built-in roles, or assigned to a [custom role](../role-based-access-control/custom-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) that is assigned the actions listed for each Network Watcher capability in the sections that follow.</span></span> <span data-ttu-id="77193-106">To learn more about Network Watcher's capabilities, see [What is Network Watcher?](network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77193-106">To learn more about Network Watcher's capabilities, see [What is Network Watcher?](network-watcher-monitoring-overview.md).</span></span>

## <a name="network-watcher"></a><span data-ttu-id="77193-107">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="77193-107">Network Watcher</span></span>

| <span data-ttu-id="77193-108">Action</span><span class="sxs-lookup"><span data-stu-id="77193-108">Action</span></span>                                                              | <span data-ttu-id="77193-109">Name</span><span class="sxs-lookup"><span data-stu-id="77193-109">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-110">Microsoft.Network/networkWatchers/read</span><span class="sxs-lookup"><span data-stu-id="77193-110">Microsoft.Network/networkWatchers/read</span></span>                              | <span data-ttu-id="77193-111">Get a network watcher</span><span class="sxs-lookup"><span data-stu-id="77193-111">Get a network watcher</span></span>                                          |
| <span data-ttu-id="77193-112">Microsoft.Network/networkWatchers/write</span><span class="sxs-lookup"><span data-stu-id="77193-112">Microsoft.Network/networkWatchers/write</span></span>                             | <span data-ttu-id="77193-113">Create or update a network watcher</span><span class="sxs-lookup"><span data-stu-id="77193-113">Create or update a network watcher</span></span>                             |
| <span data-ttu-id="77193-114">Microsoft.Network/networkWatchers/delete</span><span class="sxs-lookup"><span data-stu-id="77193-114">Microsoft.Network/networkWatchers/delete</span></span>                            | <span data-ttu-id="77193-115">Delete a network watcher</span><span class="sxs-lookup"><span data-stu-id="77193-115">Delete a network watcher</span></span>                                       |

## <a name="nsg-flow-logs"></a><span data-ttu-id="77193-116">NSG flow logs</span><span class="sxs-lookup"><span data-stu-id="77193-116">NSG flow logs</span></span>

| <span data-ttu-id="77193-117">Action</span><span class="sxs-lookup"><span data-stu-id="77193-117">Action</span></span>                                                              | <span data-ttu-id="77193-118">Name</span><span class="sxs-lookup"><span data-stu-id="77193-118">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-119">Microsoft.Network/networkWatchers/configureFlowLog/action</span><span class="sxs-lookup"><span data-stu-id="77193-119">Microsoft.Network/networkWatchers/configureFlowLog/action</span></span>           | <span data-ttu-id="77193-120">Configure a flow Log</span><span class="sxs-lookup"><span data-stu-id="77193-120">Configure a flow Log</span></span>                                           |
| <span data-ttu-id="77193-121">Microsoft.Network/networkWatchers/queryFlowLogStatus/action</span><span class="sxs-lookup"><span data-stu-id="77193-121">Microsoft.Network/networkWatchers/queryFlowLogStatus/action</span></span>         | <span data-ttu-id="77193-122">Query status for a flow log</span><span class="sxs-lookup"><span data-stu-id="77193-122">Query status for a flow log</span></span>                                    |

## <a name="connection-troubleshoot"></a><span data-ttu-id="77193-123">Connection troubleshoot</span><span class="sxs-lookup"><span data-stu-id="77193-123">Connection troubleshoot</span></span>

| <span data-ttu-id="77193-124">Action</span><span class="sxs-lookup"><span data-stu-id="77193-124">Action</span></span>                                                              | <span data-ttu-id="77193-125">Name</span><span class="sxs-lookup"><span data-stu-id="77193-125">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-126">Microsoft.Network/networkWatchers/queryTroubleshootResult/action</span><span class="sxs-lookup"><span data-stu-id="77193-126">Microsoft.Network/networkWatchers/queryTroubleshootResult/action</span></span>    | <span data-ttu-id="77193-127">Query results of a connection troubleshoot test</span><span class="sxs-lookup"><span data-stu-id="77193-127">Query results of a connection troubleshoot test</span></span>                |
| <span data-ttu-id="77193-128">Microsoft.Network/networkWatchers/troubleshoot/action</span><span class="sxs-lookup"><span data-stu-id="77193-128">Microsoft.Network/networkWatchers/troubleshoot/action</span></span>               | <span data-ttu-id="77193-129">Run a connection troubleshoot test</span><span class="sxs-lookup"><span data-stu-id="77193-129">Run a connection troubleshoot test</span></span>                             |

## <a name="connection-monitor"></a><span data-ttu-id="77193-130">Connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-130">Connection monitor</span></span>

| <span data-ttu-id="77193-131">Action</span><span class="sxs-lookup"><span data-stu-id="77193-131">Action</span></span>                                                              | <span data-ttu-id="77193-132">Name</span><span class="sxs-lookup"><span data-stu-id="77193-132">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-133">Microsoft.Network/networkWatchers/connectionMonitors/start/action</span><span class="sxs-lookup"><span data-stu-id="77193-133">Microsoft.Network/networkWatchers/connectionMonitors/start/action</span></span>   | <span data-ttu-id="77193-134">Start a connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-134">Start a connection monitor</span></span>                                     |
| <span data-ttu-id="77193-135">Microsoft.Network/networkWatchers/connectionMonitors/stop/action</span><span class="sxs-lookup"><span data-stu-id="77193-135">Microsoft.Network/networkWatchers/connectionMonitors/stop/action</span></span>    | <span data-ttu-id="77193-136">Stop a connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-136">Stop a connection monitor</span></span>                                      |
| <span data-ttu-id="77193-137">Microsoft.Network/networkWatchers/connectionMonitors/query/action</span><span class="sxs-lookup"><span data-stu-id="77193-137">Microsoft.Network/networkWatchers/connectionMonitors/query/action</span></span>   | <span data-ttu-id="77193-138">Query a connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-138">Query a connection monitor</span></span>                                     |
| <span data-ttu-id="77193-139">Microsoft.Network/networkWatchers/connectionMonitors/read</span><span class="sxs-lookup"><span data-stu-id="77193-139">Microsoft.Network/networkWatchers/connectionMonitors/read</span></span>           | <span data-ttu-id="77193-140">Get a connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-140">Get a connection monitor</span></span>                                       |
| <span data-ttu-id="77193-141">Microsoft.Network/networkWatchers/connectionMonitors/write</span><span class="sxs-lookup"><span data-stu-id="77193-141">Microsoft.Network/networkWatchers/connectionMonitors/write</span></span>          | <span data-ttu-id="77193-142">Create a connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-142">Create a connection monitor</span></span>                                    |
| <span data-ttu-id="77193-143">Microsoft.Network/networkWatchers/connectionMonitors/delete</span><span class="sxs-lookup"><span data-stu-id="77193-143">Microsoft.Network/networkWatchers/connectionMonitors/delete</span></span>         | <span data-ttu-id="77193-144">Delete a connection monitor</span><span class="sxs-lookup"><span data-stu-id="77193-144">Delete a connection monitor</span></span>                                    |

## <a name="packet-capture"></a><span data-ttu-id="77193-145">Packet capture</span><span class="sxs-lookup"><span data-stu-id="77193-145">Packet capture</span></span>

| <span data-ttu-id="77193-146">Action</span><span class="sxs-lookup"><span data-stu-id="77193-146">Action</span></span>                                                              | <span data-ttu-id="77193-147">Name</span><span class="sxs-lookup"><span data-stu-id="77193-147">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-148">Microsoft.Network/networkWatchers/packetCaptures/queryStatus/action</span><span class="sxs-lookup"><span data-stu-id="77193-148">Microsoft.Network/networkWatchers/packetCaptures/queryStatus/action</span></span> | <span data-ttu-id="77193-149">Query the status of a packet capture</span><span class="sxs-lookup"><span data-stu-id="77193-149">Query the status of a packet capture</span></span>                           |
| <span data-ttu-id="77193-150">Microsoft.Network/networkWatchers/packetCaptures/stop/action</span><span class="sxs-lookup"><span data-stu-id="77193-150">Microsoft.Network/networkWatchers/packetCaptures/stop/action</span></span>        | <span data-ttu-id="77193-151">Stop a packet capture</span><span class="sxs-lookup"><span data-stu-id="77193-151">Stop a packet capture</span></span>                                          |
| <span data-ttu-id="77193-152">Microsoft.Network/networkWatchers/packetCaptures/read</span><span class="sxs-lookup"><span data-stu-id="77193-152">Microsoft.Network/networkWatchers/packetCaptures/read</span></span>               | <span data-ttu-id="77193-153">Get a packet capture</span><span class="sxs-lookup"><span data-stu-id="77193-153">Get a packet capture</span></span>                                           |
| <span data-ttu-id="77193-154">Microsoft.Network/networkWatchers/packetCaptures/write</span><span class="sxs-lookup"><span data-stu-id="77193-154">Microsoft.Network/networkWatchers/packetCaptures/write</span></span>              | <span data-ttu-id="77193-155">Create a packet capture</span><span class="sxs-lookup"><span data-stu-id="77193-155">Create a packet capture</span></span>                                        |
| <span data-ttu-id="77193-156">Microsoft.Network/networkWatchers/packetCaptures/delete</span><span class="sxs-lookup"><span data-stu-id="77193-156">Microsoft.Network/networkWatchers/packetCaptures/delete</span></span>             | <span data-ttu-id="77193-157">Delete a packet capture</span><span class="sxs-lookup"><span data-stu-id="77193-157">Delete a packet capture</span></span>                                        |

## <a name="ip-flow-verify"></a><span data-ttu-id="77193-158">IP flow verify</span><span class="sxs-lookup"><span data-stu-id="77193-158">IP flow verify</span></span>

| <span data-ttu-id="77193-159">Action</span><span class="sxs-lookup"><span data-stu-id="77193-159">Action</span></span>                                                              | <span data-ttu-id="77193-160">Name</span><span class="sxs-lookup"><span data-stu-id="77193-160">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-161">Microsoft.Network/networkWatchers/ipFlowVerify/action</span><span class="sxs-lookup"><span data-stu-id="77193-161">Microsoft.Network/networkWatchers/ipFlowVerify/action</span></span>               | <span data-ttu-id="77193-162">Verify an IP flow</span><span class="sxs-lookup"><span data-stu-id="77193-162">Verify an IP flow</span></span>                                              |

## <a name="next-hop"></a><span data-ttu-id="77193-163">Next hop</span><span class="sxs-lookup"><span data-stu-id="77193-163">Next hop</span></span>

| <span data-ttu-id="77193-164">Action</span><span class="sxs-lookup"><span data-stu-id="77193-164">Action</span></span>                                                              | <span data-ttu-id="77193-165">Name</span><span class="sxs-lookup"><span data-stu-id="77193-165">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-166">Microsoft.Network/networkWatchers/nextHop/action</span><span class="sxs-lookup"><span data-stu-id="77193-166">Microsoft.Network/networkWatchers/nextHop/action</span></span>                    | <span data-ttu-id="77193-167">Get the next hop from a VM</span><span class="sxs-lookup"><span data-stu-id="77193-167">Get the next hop from a VM</span></span>                                     |

## <a name="network-security-group-view"></a><span data-ttu-id="77193-168">Network security group view</span><span class="sxs-lookup"><span data-stu-id="77193-168">Network security group view</span></span>

| <span data-ttu-id="77193-169">Action</span><span class="sxs-lookup"><span data-stu-id="77193-169">Action</span></span>                                                              | <span data-ttu-id="77193-170">Name</span><span class="sxs-lookup"><span data-stu-id="77193-170">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-171">Microsoft.Network/networkWatchers/securityGroupView/action</span><span class="sxs-lookup"><span data-stu-id="77193-171">Microsoft.Network/networkWatchers/securityGroupView/action</span></span>          | <span data-ttu-id="77193-172">View security groups</span><span class="sxs-lookup"><span data-stu-id="77193-172">View security groups</span></span>                                           |

## <a name="topology"></a><span data-ttu-id="77193-173">Topology</span><span class="sxs-lookup"><span data-stu-id="77193-173">Topology</span></span>

| <span data-ttu-id="77193-174">Action</span><span class="sxs-lookup"><span data-stu-id="77193-174">Action</span></span>                                                              | <span data-ttu-id="77193-175">Name</span><span class="sxs-lookup"><span data-stu-id="77193-175">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-176">Microsoft.Network/networkWatchers/topology/action</span><span class="sxs-lookup"><span data-stu-id="77193-176">Microsoft.Network/networkWatchers/topology/action</span></span>                   | <span data-ttu-id="77193-177">Get topology</span><span class="sxs-lookup"><span data-stu-id="77193-177">Get topology</span></span>                                                   |

## <a name="reachability-report"></a><span data-ttu-id="77193-178">Reachability report</span><span class="sxs-lookup"><span data-stu-id="77193-178">Reachability report</span></span>

| <span data-ttu-id="77193-179">Action</span><span class="sxs-lookup"><span data-stu-id="77193-179">Action</span></span>                                                              | <span data-ttu-id="77193-180">Name</span><span class="sxs-lookup"><span data-stu-id="77193-180">Name</span></span>                                                           |
| ---------                                                           | -------------                                                  |
| <span data-ttu-id="77193-181">Microsoft.Network/networkWatchers/azureReachabilityReport/action</span><span class="sxs-lookup"><span data-stu-id="77193-181">Microsoft.Network/networkWatchers/azureReachabilityReport/action</span></span>    | <span data-ttu-id="77193-182">Get an Azure reachability report</span><span class="sxs-lookup"><span data-stu-id="77193-182">Get an Azure reachability report</span></span>                               |

## <a name="additional-actions"></a><span data-ttu-id="77193-183">Additional actions</span><span class="sxs-lookup"><span data-stu-id="77193-183">Additional actions</span></span>

<span data-ttu-id="77193-184">Network Watcher capabilities also require the following actions:</span><span class="sxs-lookup"><span data-stu-id="77193-184">Network Watcher capabilities also require the following actions:</span></span>

- <span data-ttu-id="77193-185">Microsoft.Storage/Read</span><span class="sxs-lookup"><span data-stu-id="77193-185">Microsoft.Storage/Read</span></span>
- <span data-ttu-id="77193-186">Microsoft.Authorization/Read</span><span class="sxs-lookup"><span data-stu-id="77193-186">Microsoft.Authorization/Read</span></span>
- <span data-ttu-id="77193-187">Microsoft.Resources/subscriptions/resourceGroups/Read</span><span class="sxs-lookup"><span data-stu-id="77193-187">Microsoft.Resources/subscriptions/resourceGroups/Read</span></span>
- <span data-ttu-id="77193-188">Microsoft.Storage/storageAccounts/listServiceSas/Action</span><span class="sxs-lookup"><span data-stu-id="77193-188">Microsoft.Storage/storageAccounts/listServiceSas/Action</span></span>
- <span data-ttu-id="77193-189">Microsoft.Storage/storageAccounts/listAccountSas/Action</span><span class="sxs-lookup"><span data-stu-id="77193-189">Microsoft.Storage/storageAccounts/listAccountSas/Action</span></span>
- <span data-ttu-id="77193-190">Microsoft.Storage/storageAccounts/listKeys/Action</span><span class="sxs-lookup"><span data-stu-id="77193-190">Microsoft.Storage/storageAccounts/listKeys/Action</span></span>
- <span data-ttu-id="77193-191">Microsoft.Compute/virtualMachines/Read</span><span class="sxs-lookup"><span data-stu-id="77193-191">Microsoft.Compute/virtualMachines/Read</span></span>
- <span data-ttu-id="77193-192">Microsoft.Compute/virtualMachines/Write</span><span class="sxs-lookup"><span data-stu-id="77193-192">Microsoft.Compute/virtualMachines/Write</span></span>
- <span data-ttu-id="77193-193">Microsoft.Compute/virtualMachineScaleSets/Read</span><span class="sxs-lookup"><span data-stu-id="77193-193">Microsoft.Compute/virtualMachineScaleSets/Read</span></span>
- <span data-ttu-id="77193-194">Microsoft.Compute/virtualMachineScaleSets/Write</span><span class="sxs-lookup"><span data-stu-id="77193-194">Microsoft.Compute/virtualMachineScaleSets/Write</span></span>
- <span data-ttu-id="77193-195">Microsoft.Insights/alertRules/\*</span><span class="sxs-lookup"><span data-stu-id="77193-195">Microsoft.Insights/alertRules/\*</span></span>
- <span data-ttu-id="77193-196">Microsoft.Support/\*</span><span class="sxs-lookup"><span data-stu-id="77193-196">Microsoft.Support/\*</span></span>