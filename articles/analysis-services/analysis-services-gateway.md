---
title: On-premises data gateway | Microsoft Docs
description: An On-premises gateway is necessary if your Analysis Services server in Azure will connect to on-premises data sources.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/18/2017
ms.author: owend
ms.openlocfilehash: 3a28e80c2bf488b36d860a5645328db0c9b14db2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554687"
---
# <a name="on-premises-data-gateway"></a>On-premises data gateway
The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services server in the cloud.

A gateway is installed on a computer in your network. One gateway must be installed for each Azure Analysis Services server you have in your Azure subscription. For example, if you have two servers in your Azure subscription that connect to on-premises data sources, a gateway must be installed on two separate computers in your network.

## <a name="requirements"></a>Requirements
**Minimum Requirements:**

* .NET 4.5 Framework
* 64-bit version of Windows 7 / Windows Server 2008 R2 (or later)

**Recommended:**

* 8 Core CPU
* 8 GB Memory
* 64-bit version of Windows 2012 R2 (or later)

**Important considerations:**

* The gateway cannot be installed on a domain controller.
* Only one gateway can be installed on a single computer.
* Install the gateway on a computer that remains on and does not go to sleep. If the computer is not on, your Azure Analysis Services server cannot connect to your on-premises data sources to refresh data.
* Do not install the gateway on a computer wirelessly connected to your network. Performance can be diminished.
* To change the server name for a gateway that has already been configured, you need to reinstall and configure a new gateway.
* In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error. To learn more, see [Datasource connections](analysis-services-datasource.md).

## <a name="supported-on-premises-data-sources"></a>Supported on-premises data sources
The gateway supports connections between your Azure Analysis Services server and the following on-premises data sources:

* SQL Server
* SQL Data Warehouse
* APS
* Oracle
* Teradata

## <a name="download"></a>Download
 [Download the gateway](https://aka.ms/azureasgateway)

## <a name="install-and-configure"></a>Install and configure
1. Run setup.
2. Choose an installation location and accept the license terms.
3. Sign in to Azure.
4. Specify your Azure Analysis Server name. You can only specify one server per gateway. Click **Configure** and you're good to go.

    ![sign in to azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-gateway/aas-gateway-configure-server.png)

## <a name="how-it-works"></a>How it works
The gateway runs as a Windows service, **On-premises data gateway**, on a computer in your organization's network. The gateway you install for use with Azure Analysis Services is based on the same gateway used for other services like Power BI, but with some differences in how it's configured.

![How it works](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-gateway/aas-gateway-how-it-works.png)

Queries and data flow work like this:

1. A query is created by the cloud service with the encrypted credentials for the on-premises data source. It's then sent to a queue for the gateway to process.
2. The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. The on-premises data gateway polls the Azure Service Bus for pending requests.
4. The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.
5. The gateway sends the query to the data source for execution.
6. The results are sent from the data source, back to the gateway, and then onto the cloud service.

## <a name="windows-service-account"></a>Windows Service account
The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential. By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on. This credential is not the same account used to connect to on-premises data sources or your Azure account.  

If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.

## <a name="ports"></a>Ports
The gateway creates an outbound connection to Azure Service Bus. It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.  The gateway does not require inbound ports.

It's recommended you whitelist the IP addresses for your data region in your firewall. You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653). This list is updated weekly.

> [!NOTE]
> The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation. For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24. Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).
>
>

The following are the fully qualified domain names used by the gateway.

| Domain names | Outbound ports | Description |
| --- | --- | --- |
| *.powerbi.com |80 |HTTP used to download the installer. |
| *.powerbi.com |443 |HTTPS |
| *.analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |Advanced Message Queuing Protocol (AMQP) |
| *.servicebus.windows.net |443, 9350-9354 |Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |Used to test internet connectivity if the gateway is unreachable by the Power BI service. |
| *.microsoftonline-p.com |443 |Used for authentication depending on configuration. |

### <a name="forcing-https-communication-with-azure-service-bus"></a>Forcing HTTPS communication with Azure Service Bus
You can force the gateway to communicate with Azure Service Bus using HTTPS instead of direct TCP; however, this can greatly reduce performance. You need to modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file. Change the value from `AutoDetect` to `Https`. This file is located, by default, at *C:\Program Files\On-premises data gateway*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```


## <a name="troubleshooting"></a>Troubleshooting
Under the hood, the on-premises data gateway used for connecting Azure Analysis Services to your on-premises data sources is the same gateway used with Power BI.

If you’re having trouble when installing and configuring a gateway, be sure to see [Troubleshooting the Power BI Gateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem-tshoot/). If you think you are having an issue with your firewall, see the firewall or proxy sections.

If you think you're encountering proxy issues, with the gateway, see [Configuring proxy settings for the Power BI Gateways](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy.md).

### <a name="telemetry"></a>Telemetry
Telemetry can be used for monitoring and troubleshooting. 

**To turn on telemetry**

1.  Check the On-premises data gateway client directory on the computer. Typically, it's %systemdrive%\Program Files\On-premises data gateway. Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.
2.  In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory. Change the SendTelemetry setting to true.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Save your changes and restart the Windows service: On-premises data gateway service.




## <a name="next-steps"></a>Next steps
* [Manage Analysis Services](analysis-services-manage.md)
* [Get data from Azure Analysis Services](analysis-services-connect.md)


