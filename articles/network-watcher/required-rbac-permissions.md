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
# <a name="role-based-access-control-permissions-required-to-use-network-watcher-capabilities"></a>Role-based access control permissions required to use Network Watcher capabilities

Azure role-based access control (RBAC) enables you to assign only the specific actions to members of your organization that they require to complete their assigned responsibilities. To use Network Watcher capabilities, the account you log into Azure with, must be assigned to the [Owner](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#owner), [Contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#contributor), or [Network contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#network-contributor) built-in roles, or assigned to a [custom role](../role-based-access-control/custom-roles.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) that is assigned the actions listed for each Network Watcher capability in the sections that follow. To learn more about Network Watcher's capabilities, see [What is Network Watcher?](network-watcher-monitoring-overview.md).

## <a name="network-watcher"></a>Network Watcher

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/read                              | Get a network watcher                                          |
| Microsoft.Network/networkWatchers/write                             | Create or update a network watcher                             |
| Microsoft.Network/networkWatchers/delete                            | Delete a network watcher                                       |

## <a name="nsg-flow-logs"></a>NSG flow logs

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/configureFlowLog/action           | Configure a flow Log                                           |
| Microsoft.Network/networkWatchers/queryFlowLogStatus/action         | Query status for a flow log                                    |

## <a name="connection-troubleshoot"></a>Connection troubleshoot

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/queryTroubleshootResult/action    | Query results of a connection troubleshoot test                |
| Microsoft.Network/networkWatchers/troubleshoot/action               | Run a connection troubleshoot test                             |

## <a name="connection-monitor"></a>Connection monitor

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/connectionMonitors/start/action   | Start a connection monitor                                     |
| Microsoft.Network/networkWatchers/connectionMonitors/stop/action    | Stop a connection monitor                                      |
| Microsoft.Network/networkWatchers/connectionMonitors/query/action   | Query a connection monitor                                     |
| Microsoft.Network/networkWatchers/connectionMonitors/read           | Get a connection monitor                                       |
| Microsoft.Network/networkWatchers/connectionMonitors/write          | Create a connection monitor                                    |
| Microsoft.Network/networkWatchers/connectionMonitors/delete         | Delete a connection monitor                                    |

## <a name="packet-capture"></a>Packet capture

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/packetCaptures/queryStatus/action | Query the status of a packet capture                           |
| Microsoft.Network/networkWatchers/packetCaptures/stop/action        | Stop a packet capture                                          |
| Microsoft.Network/networkWatchers/packetCaptures/read               | Get a packet capture                                           |
| Microsoft.Network/networkWatchers/packetCaptures/write              | Create a packet capture                                        |
| Microsoft.Network/networkWatchers/packetCaptures/delete             | Delete a packet capture                                        |

## <a name="ip-flow-verify"></a>IP flow verify

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/ipFlowVerify/action               | Verify an IP flow                                              |

## <a name="next-hop"></a>Next hop

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/nextHop/action                    | Get the next hop from a VM                                     |

## <a name="network-security-group-view"></a>Network security group view

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/securityGroupView/action          | View security groups                                           |

## <a name="topology"></a>Topology

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/topology/action                   | Get topology                                                   |

## <a name="reachability-report"></a>Reachability report

| Action                                                              | Name                                                           |
| ---------                                                           | -------------                                                  |
| Microsoft.Network/networkWatchers/azureReachabilityReport/action    | Get an Azure reachability report                               |

## <a name="additional-actions"></a>Additional actions

Network Watcher capabilities also require the following actions:

- Microsoft.Storage/Read
- Microsoft.Authorization/Read
- Microsoft.Resources/subscriptions/resourceGroups/Read
- Microsoft.Storage/storageAccounts/listServiceSas/Action
- Microsoft.Storage/storageAccounts/listAccountSas/Action
- Microsoft.Storage/storageAccounts/listKeys/Action
- Microsoft.Compute/virtualMachines/Read
- Microsoft.Compute/virtualMachines/Write
- Microsoft.Compute/virtualMachineScaleSets/Read
- Microsoft.Compute/virtualMachineScaleSets/Write
- Microsoft.Insights/alertRules/*
- Microsoft.Support/*