---
title: Diagnose On-Premises connectivity via VPN gateway with Azure Network Watcher | Microsoft Docs
description: This article describes how to diagnose on-premises connectivity via VPN gateway with Azure Network Watcher resource troubleshooting.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: f262d586605701e5af9681a2491a176a1ebd819e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662571"
---
# <a name="diagnose-on-premise-connectivity-via-vpn-gateways"></a>Diagnose on-premise connectivity via VPN gateways

Azure VPN Gateway enables you to create hybrid solution that address the need for a secure connection between your on-premises network and your Azure virtual network. As your requirements are unique, so is the choice of on-premises VPN device. Azure currently supports [several VPN devices](../vpn-gateway/vpn-gateway-about-vpn-devices.md#a-namedevicetableavalidated-vpn-devices-and-device-configuration-guides) that are constantly validated in partnership with the device vendors. Review the device-specific configuration settings before configuring your on-premises VPN device. Similarly, Azure VPN Gateway is configured with a set of [supported IPsec parameters](../vpn-gateway/vpn-gateway-about-vpn-devices.md#a-nameipsecaipsecike-parameters) that are used for establishing connections. Currently there is no way for you to specify or select a specific combination of IPsec parameters from the Azure VPN Gateway. For establishing a successful connection between on-premises and Azure, the on-premises VPN device settings must be in accordance with the IPsec parameters prescribed by Azure VPN Gateway. Failure to do so results in loss of connectivity and until now troubleshooting these issues was not trivial and usually took hours to identify and fix the issue.

With the Azure Network Watcher troubleshoot feature, you are able to diagnose any issues with your Gateway and Connections and within minutes have enough information to make an informed decision to rectify the issue.

## <a name="scenario"></a>Scenario

You want to configure a site-to-site connection between Azure and on-premises using Cisco ASA as the on-premises VPN Gateway. To achieve this scenario, you would require the following setup:

1. Virtual Network Gateway - The VPN Gateway on Azure
1. Local Network Gateway - The [on-premises (CISCO ASA) VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) representation in Azure cloud
1. Site-to-site connection (policy based) - [Connection between the VPN Gateway and the on-premises CISCO ASA](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#a-namecreateconnectiona8-create-a-site-to-site-vpn-connection)
1. [Configuring CISCO ASA](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA)

Detailed step by step guidance for configuring a Site-to-Site configuration can be found by visiting: [Create a VNet with a Site-to-Site connection using the Azure portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

One of the critical configuration steps is configuring the IPsec communication parameters, any misconfiguration leads to loss of connectivity between the on-premises network and Azure. Currently Azure VPN Gateways are configured to support the following IPsec parameters for Phase 1. Note, as mentioned earlier these settings cannot be modified.  As you can see in the table below, the encryption algorithms supported by Azure VPN Gateway are AES256, AES128, and 3DES.

### <a name="ike-phase-1-setup"></a>IKE phase 1 setup

| **Property** | **PolicyBased** | **RouteBased and Standard or High-Performance VPN gateway** |
| --- | --- | --- |
| IKE Version |IKEv1 |IKEv2 |
| Diffie-Hellman Group |Group 2 (1024 bit) |Group 2 (1024 bit) |
| Authentication Method |Pre-Shared Key |Pre-Shared Key |
| Encryption Algorithms |AES256 AES128 3DES |AES256 3DES |
| Hashing Algorithm |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Phase 1 Security Association (SA) Lifetime (Time) |28,800 seconds |10,800 seconds |

As a user, you would be required to configure your Cisco ASA, a sample configuration can be found on [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Cisco/Current/ASA/ASA_9.1_and_above_Show_running-config.txt). Among other configurations, you would also need to specify the hashing algorithm. Cisco ASA supports more [encryption and hashing algorithms](http://www.cisco.com/c/en/us/about/security-center/next-generation-cryptography.html) than Azure VPN Gateway. Unknowingly you configured your Cisco ASA to use SHA-512 as the hashing algorithm. As this algorithm is not a supported algorithm for policy-based connections, your VPN connection does work.

These issues are hard to troubleshoot and root causes are often non-intuitive. In this case you can open a support ticket to get help on resolving the issue. But with Azure Network Watcher troubleshoot API, you can identify these issues on your own.

## <a name="troubleshooting-using-azure-network-watcher"></a>Troubleshooting using Azure Network Watcher

To diagnose your connection, connect to Azure PowerShell and initiate the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. You can find the details on using this cmdlet at [Troubleshoot Virtual Network Gateway and connections - PowerShell](network-watcher-troubleshoot-manage-powershell.md). This cmdlet may take up to few minutes to complete.

Once the cmdlet completes, you can navigate to the storage location specified in the cmdlet to get detailed information on about the issue and logs. Azure Network Watcher creates a zip folder that contains the following log files:

![1][1]

Open the file called IKEErrors.txt and it displays the following error, indicating an issue with on-premises IKE setting misconfiguration.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

You can get detailed information from the Scrubbed-wfpdiag.txt about the error, as in this case it mentions that there was `ERROR_IPSEC_IKE_POLICY_MATCH` that lead to connection not working properly.

Another common misconfiguration is the specifying incorrect shared keys. If in the preceding example you had specified different shared keys, the IKEErrors.txt shows the following error: `Error: Authentication failed. Check shared key`.

Azure Network Watcher troubleshoot feature enables you to diagnose and troubleshoot your VPN Gateway and Connection with the ease of a simple PowerShell cmdlet. Currently we support diagnosing the following conditions and are working towards adding more condition.

### <a name="gateway"></a>Gateway

| Fault Type | Reason | Log|
|---|---|---|
| NoFault | When no error is detected. |Yes|
| GatewayNotFound | Cannot find Gateway or Gateway is not provisioned. |No|
| PlannedMaintenance |  Gateway instance is under maintenance.  |No|
| UserDrivenUpdate | When a user update is in progress. This could be a resize operation. | No |
| VipUnResponsive | Cannot reach the primary instance of the Gateway. This happens when the health probe fails. | No |
| PlatformInActive | There is an issue with the platform. | No|
| ServiceNotRunning | The underlying service is not running. | No|
| NoConnectionsFoundForGateway | No Connections exists on the gateway. This is only a warning.| No|
| ConnectionsNotConnected | None of the Connections are not connected. This is only a warning.| Yes|
| GatewayCPUUsageExceeded | The current Gateway usage CPU usage is > 95%. | Yes |

### <a name="connection"></a>Connection

| Fault Type | Reason | Log|
|---|---|---|
| NoFault | When no error is detected. |Yes|
| GatewayNotFound | Cannot find Gateway or Gateway is not provisioned. |No|
| PlannedMaintenance | Gateway instance is under maintenance.  |No|
| UserDrivenUpdate | When a user update is in progress. This could be a resize operation.  | No |
| VipUnResponsive | Cannot reach the primary instance of the Gateway. It happens when the health probe fails. | No |
| ConnectionEntityNotFound | Connection configuration is missing. | No |
| ConnectionIsMarkedDisconnected | The Connection is marked "disconnected". |No|
| ConnectionNotConfiguredOnGateway | The underlying service does not have the Connection configured. | Yes |
| ConnectionMarkedStandy | The underlying service is marked as standby.| Yes|
| Authentication | Preshared Key mismatch. | Yes|
| PeerReachability | The peer gateway is not reachable. | Yes|
| IkePolicyMismatch | The peer gateway has IKE policies that are not supported by Azure. | Yes|
| WfpParse Error | An error occurred parsing the WFP log. |Yes|

## <a name="next-steps"></a>Next steps

Learn to check VPN Gateway connectivity with PowerShell and Azure Automation by visiting [Monitor VPN gateways with Azure Network Watcher troubleshooting](network-watcher-monitor-with-azure-automation.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-diagnose-on-premises-connectivity/figure1.png
