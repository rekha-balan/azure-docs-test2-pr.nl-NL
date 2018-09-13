---
title: Understand Azure AD Application Proxy connectors | Microsoft Docs
description: Covers the basics about Azure AD Application Proxy connectors.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/28/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 23bf9d5fb26ee3a0f224f7a8acc2b0539a5c1607
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865147"
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Understand Azure AD Application Proxy connectors

Connectors are what make Azure AD Application Proxy possible. They are simple, easy to deploy and maintain, and super powerful. This article discusses what connectors are, how they work, and some suggestions for how to optimize your deployment. 

## <a name="what-is-an-application-proxy-connector"></a>What is an Application Proxy connector?

Connectors are lightweight agents that sit on-premises and facilitate the outbound connection to the Application Proxy service. Connectors must be installed on a Windows Server that has access to the backend application. You can organize connectors into connector groups, with each group handling traffic to specific applications. Connectors load-balance automatically, and can help to optimize your network structure. 

## <a name="requirements-and-deployment"></a>Requirements and deployment

To deploy Application Proxy successfully, you need at least one connector, but we recommend two or more for greater resiliency. Install the connector on a Windows Server 2012 R2 or 2016 machine. The connector needs to be able to communicate with the Application Proxy service as well as the on-premises applications that you publish. 

For more information about the network requirements for the connector server, see [Get started with Application Proxy and install a connector](application-proxy-enable.md).

## <a name="maintenance"></a>Maintenance
The connectors and the service take care of all the high availability tasks. They can be added or removed dynamically. Each time a new request arrives it is routed to one of the connectors that is currently available. If a connector is temporarily not available, it doesn't respond to this traffic.

The connectors are stateless and have no configuration data on the machine. The only data they store is the settings for connecting the service and its authentication certificate. When they connect to the service, they pull all the required configuration data and refresh it every couple of minutes.

Connectors also poll the server to find out whether there is a newer version of the connector. If one is found, the connectors update themselves.

You can monitor your connectors from the machine they are running on, using either the event log and performance counters. Or you can view their status from the Application Proxy page of the Azure portal:

 ![AzureAD Application Proxy Connectors](./media/application-proxy-connectors/app-proxy-connectors.png)

You don't have to manually delete connectors that are unused. When a connector is running, it remains active as it connects to the service. Unused connectors are tagged as _inactive_ and are removed after 10 days of inactivity. If you do want to uninstall a connector, though, uninstall both the Connector service and the Updater service from the server. Restart your computer to fully remove the service.

## <a name="automatic-updates"></a>Automatic updates

Azure AD provides automatic updates for all the connectors that you deploy. As long as the Application Proxy Connector Updater service is running, your connectors update automatically. If you don’t see the Connector Updater service on your server, you need to [reinstall your connector](application-proxy-enable.md) to get any updates. 

If you don't want to wait for an automatic update to come to your connector, you can perform a manual upgrade. Go to the [connector download page](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) on the server where your connector is located and select **Download**. This process kicks off an upgrade for the local connector. 

For tenants with multiple connectors, the automatic updates target one connector at a time in each group to prevent downtime in your environment. 

You may experience downtime when your connector updates if:  
- You only have one connector. To avoid this downtime and improve high availability, we recommend you install a second connector and [create a connector group](application-proxy-connector-groups.md).  
- A connector was in the middle of a transaction when the update began. Although the initial transaction is lost, your browser should automatically retry the operation or you can refresh your page. When the request is resent, the traffic is routed to a backup connector.

## <a name="creating-connector-groups"></a>Creating connector groups

Connector groups enable you to assign specific connectors to serve specific applications. You can group a number of connectors together, and then assign each application to a group. 

Connector groups make it easier to manage large deployments. They also improve latency for tenants that have applications hosted in different regions, because you can create location-based connector groups to serve only local applications. 

To learn more about connector groups, see [Publish applications on separate networks and locations using connector groups](application-proxy-connector-groups.md).

## <a name="capacity-planning"></a>Capacity Planning 

While connectors will automatically load balance within a connector group, it is also important to make sure you have planned enough capacity between connectors to handle the expected traffic volume. In general, the more users you have, the larger a machine you will need. Below is a table giving an outline of the volume different machines can handle. Please note it is all based on expected Transactions Per Second (TPS) rather than by user since usage patterns vary and cannot be used to predict load.  Also note that there will be some differences based on the size of the responses and the backend application response time - larger response sizes and slower response times will result in a lower Max TPS.

|Cores|RAM|Expected Latency (MS)-P99|Max TPS|
| ----- | ----- | ----- | ----- |
|2|8|325|586|
|4|16|320|1150|
|8|32|270|1190|
|16|64|245|1200*|
\* This machine had a connection limit of 800. For all other machines we used the default 200 connection limit.
 
>[!NOTE]
>There is not much difference in the maximum TPS between 4, 8, and 16 core machines. The main difference between those is in the expected latency.  

## <a name="security-and-networking"></a>Security and networking

Connectors can be installed anywhere on the network that allows them to send requests to the Application Proxy service. What's important is that the computer running the connector also has access to your apps. You can install connectors inside of your corporate network or on a virtual machine that runs in the cloud. Connectors can run within a demilitarized zone (DMZ), but it's not necessary because all traffic is outbound so your network stays secure.

Connectors only send outbound requests. The outbound traffic is sent to the Application Proxy service and to the published applications. You don't have to open inbound ports because traffic flows both ways once a session is established. You don't have to set up load balancing between the connectors or configure inbound access through your firewalls. 

For more information about configuring outbound firewall rules, see [Work with existing on-premises proxy servers](application-proxy-configure-connectors-with-proxy-servers.md).


## <a name="performance-and-scalability"></a>Performance and scalability

Scale for the Application Proxy service is transparent, but scale is a factor for connectors. You need to have enough connectors to handle peak traffic. However, you don't need to configure load balancing because all connectors within a connector group automatically load balance.

Since connectors are stateless, they are not affected by the number of users or sessions. Instead, they respond to the number of requests and their payload size. With standard web traffic, an average machine can handle a couple thousand requests per second. The specific capacity depends on the exact machine characteristics. 

The connector performance is bound by CPU and networking. CPU performance is needed for SSL encryption and decryption, while networking is important to get fast connectivity to the applications and the online service in Azure.

In contrast, memory is less of an issue for connectors. The online service takes care of much of the processing and all unauthenticated traffic. Everything that can be done in the cloud is done in the cloud. 

The load balancing happens between connectors of a given connector group. We do a variation of a round-robin to determine which connector in the group serves a particular request. If for any reason that connector or machine becomes unavailable, the traffic will start going to another connector in the group. This resiliency is also why we recommend having multiple connectors.

Another factor that affects performance is the quality of the networking between the connectors, including: 

* **The online service**: Slow or high-latency connections to the Application Proxy service in Azure influence the connector performance. For the best performance, connect your organization to Azure with Express Route. Otherwise, have your networking team ensure that connections to Azure are handled as efficiently as possible. 
* **The backend applications**: In some cases, there are additional proxies between the connector and the backend applications that can slow or prevent connections. To troubleshoot this scenario, open a browser from the connector server and try to access the application. If you run the connectors in Azure but the applications are on-premises, the experience might not be what your users expect.
* **The domain controllers**: If the connectors perform SSO using Kerberos Constrained Delegation, they contact the domain controllers before sending the request to the backend. The connectors have a cache of Kerberos tickets, but in a busy environment the responsiveness of the domain controllers can affect performance. This issue is more common for connectors that run in Azure but communicate with domain controllers that are on-premises. 

For more information about optimizing your network, see [Network topology considerations when using Azure Active Directory Application Proxy](application-proxy-network-topology.md).

## <a name="domain-joining"></a>Domain joining

Connectors can run on a machine that is not domain-joined. However, if you want single sign-on (SSO) to applications that use Integrated Windows Authentication (IWA), you need a domain-joined machine. In this case, the connector machines must be joined to a domain that can perform [Kerberos](https://web.mit.edu/kerberos) Constrained Delegation on behalf of the users for the published applications.

Connectors can also be joined to domains or forests that have a partial trust, or to read-only domain controllers.

## <a name="connector-deployments-on-hardened-environments"></a>Connector deployments on hardened environments

Usually, connector deployment is straightforward and requires no special configuration. However, there are some unique conditions that should be considered:

* Organizations that limit the outbound traffic must [open required ports](application-proxy-enable.md#open-your-ports).
* FIPS-compliant machines might be required to change their configuration to allow the connector processes to generate and store a certificate.
* Organizations that lock down their environment based on the processes that issue the networking requests have to make sure that both connector services are enabled to access all required ports and IPs.
* In some cases, outbound forward proxies may break the two-way certificate authentication and cause the communication to fail.

## <a name="connector-authentication"></a>Connector authentication

To provide a secure service, connectors have to authenticate toward the service, and the service has to authenticate toward the connector. This authentication is done using client and server certificates when the connectors initiate the connection. This way the administrator’s username and password are not stored on the connector machine.

The certificates used are specific to the Application Proxy service. They get created during the initial registration and are automatically renewed by the connectors every couple of months. 

If a connector is not connected to the service for several months, its certificates may be outdated. In this case, uninstall and reinstall the connector to trigger registration. You can run the following PowerShell commands:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-the-hood"></a>Under the hood

Connectors are based on Windows Server Web Application Proxy, so they have most of the same management tools including Windows Event Logs

 ![Manage event logs with the Event Viewer](./media/application-proxy-connectors/event-view-window.png)

and Windows performance counters. 

 ![Add counters to the connector with the Performance Monitor](./media/application-proxy-connectors/performance-monitor.png)

The connectors have both admin and session logs. The admin logs include key events and their errors. The session logs include all the transactions and their processing details. 

To see the logs, go to the Event Viewer, open the **View** menu, and enable **Show analytic and debug logs**. Then, enable them to start collecting events. These logs do not appear in Web Application Proxy in Windows Server 2012 R2, as the connectors are based on a more recent version.

You can examine the state of the service in the Services window. The connector comprises two Windows Services: the actual connector, and the updater. Both of them must run all the time.

 ![AzureAD Services Local](./media/application-proxy-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Next steps


* [Publish applications on separate networks and locations using connector groups](application-proxy-connector-groups.md)
* [Work with existing on-premises proxy servers](application-proxy-configure-connectors-with-proxy-servers.md)
* [Troubleshoot Application Proxy and connector errors](application-proxy-troubleshoot.md)
* [How to silently install the Azure AD Application Proxy Connector](application-proxy-register-connector-powershell.md)
