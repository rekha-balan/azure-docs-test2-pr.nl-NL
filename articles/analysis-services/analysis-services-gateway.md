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
# <a name="on-premises-data-gateway"></a><span data-ttu-id="a013a-103">On-premises data gateway</span><span class="sxs-lookup"><span data-stu-id="a013a-103">On-premises data gateway</span></span>
<span data-ttu-id="a013a-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services server in the cloud.</span><span class="sxs-lookup"><span data-stu-id="a013a-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services server in the cloud.</span></span>

<span data-ttu-id="a013a-105">A gateway is installed on a computer in your network.</span><span class="sxs-lookup"><span data-stu-id="a013a-105">A gateway is installed on a computer in your network.</span></span> <span data-ttu-id="a013a-106">One gateway must be installed for each Azure Analysis Services server you have in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a013a-106">One gateway must be installed for each Azure Analysis Services server you have in your Azure subscription.</span></span> <span data-ttu-id="a013a-107">For example, if you have two servers in your Azure subscription that connect to on-premises data sources, a gateway must be installed on two separate computers in your network.</span><span class="sxs-lookup"><span data-stu-id="a013a-107">For example, if you have two servers in your Azure subscription that connect to on-premises data sources, a gateway must be installed on two separate computers in your network.</span></span>

## <a name="requirements"></a><span data-ttu-id="a013a-108">Requirements</span><span class="sxs-lookup"><span data-stu-id="a013a-108">Requirements</span></span>
<span data-ttu-id="a013a-109">**Minimum Requirements:**</span><span class="sxs-lookup"><span data-stu-id="a013a-109">**Minimum Requirements:**</span></span>

* <span data-ttu-id="a013a-110">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="a013a-110">.NET 4.5 Framework</span></span>
* <span data-ttu-id="a013a-111">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span><span class="sxs-lookup"><span data-stu-id="a013a-111">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="a013a-112">**Recommended:**</span><span class="sxs-lookup"><span data-stu-id="a013a-112">**Recommended:**</span></span>

* <span data-ttu-id="a013a-113">8 Core CPU</span><span class="sxs-lookup"><span data-stu-id="a013a-113">8 Core CPU</span></span>
* <span data-ttu-id="a013a-114">8 GB Memory</span><span class="sxs-lookup"><span data-stu-id="a013a-114">8 GB Memory</span></span>
* <span data-ttu-id="a013a-115">64-bit version of Windows 2012 R2 (or later)</span><span class="sxs-lookup"><span data-stu-id="a013a-115">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="a013a-116">**Important considerations:**</span><span class="sxs-lookup"><span data-stu-id="a013a-116">**Important considerations:**</span></span>

* <span data-ttu-id="a013a-117">The gateway cannot be installed on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="a013a-117">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="a013a-118">Only one gateway can be installed on a single computer.</span><span class="sxs-lookup"><span data-stu-id="a013a-118">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="a013a-119">Install the gateway on a computer that remains on and does not go to sleep.</span><span class="sxs-lookup"><span data-stu-id="a013a-119">Install the gateway on a computer that remains on and does not go to sleep.</span></span> <span data-ttu-id="a013a-120">If the computer is not on, your Azure Analysis Services server cannot connect to your on-premises data sources to refresh data.</span><span class="sxs-lookup"><span data-stu-id="a013a-120">If the computer is not on, your Azure Analysis Services server cannot connect to your on-premises data sources to refresh data.</span></span>
* <span data-ttu-id="a013a-121">Do not install the gateway on a computer wirelessly connected to your network.</span><span class="sxs-lookup"><span data-stu-id="a013a-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="a013a-122">Performance can be diminished.</span><span class="sxs-lookup"><span data-stu-id="a013a-122">Performance can be diminished.</span></span>
* <span data-ttu-id="a013a-123">To change the server name for a gateway that has already been configured, you need to reinstall and configure a new gateway.</span><span class="sxs-lookup"><span data-stu-id="a013a-123">To change the server name for a gateway that has already been configured, you need to reinstall and configure a new gateway.</span></span>
* <span data-ttu-id="a013a-124">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span><span class="sxs-lookup"><span data-stu-id="a013a-124">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span> <span data-ttu-id="a013a-125">To learn more, see [Datasource connections](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="a013a-125">To learn more, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="supported-on-premises-data-sources"></a><span data-ttu-id="a013a-126">Supported on-premises data sources</span><span class="sxs-lookup"><span data-stu-id="a013a-126">Supported on-premises data sources</span></span>
<span data-ttu-id="a013a-127">The gateway supports connections between your Azure Analysis Services server and the following on-premises data sources:</span><span class="sxs-lookup"><span data-stu-id="a013a-127">The gateway supports connections between your Azure Analysis Services server and the following on-premises data sources:</span></span>

* <span data-ttu-id="a013a-128">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a013a-128">SQL Server</span></span>
* <span data-ttu-id="a013a-129">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a013a-129">SQL Data Warehouse</span></span>
* <span data-ttu-id="a013a-130">APS</span><span class="sxs-lookup"><span data-stu-id="a013a-130">APS</span></span>
* <span data-ttu-id="a013a-131">Oracle</span><span class="sxs-lookup"><span data-stu-id="a013a-131">Oracle</span></span>
* <span data-ttu-id="a013a-132">Teradata</span><span class="sxs-lookup"><span data-stu-id="a013a-132">Teradata</span></span>

## <a name="download"></a><span data-ttu-id="a013a-133">Download</span><span class="sxs-lookup"><span data-stu-id="a013a-133">Download</span></span>
 [<span data-ttu-id="a013a-134">Download the gateway</span><span class="sxs-lookup"><span data-stu-id="a013a-134">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <a name="install-and-configure"></a><span data-ttu-id="a013a-135">Install and configure</span><span class="sxs-lookup"><span data-stu-id="a013a-135">Install and configure</span></span>
1. <span data-ttu-id="a013a-136">Run setup.</span><span class="sxs-lookup"><span data-stu-id="a013a-136">Run setup.</span></span>
2. <span data-ttu-id="a013a-137">Choose an installation location and accept the license terms.</span><span class="sxs-lookup"><span data-stu-id="a013a-137">Choose an installation location and accept the license terms.</span></span>
3. <span data-ttu-id="a013a-138">Sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="a013a-138">Sign in to Azure.</span></span>
4. <span data-ttu-id="a013a-139">Specify your Azure Analysis Server name.</span><span class="sxs-lookup"><span data-stu-id="a013a-139">Specify your Azure Analysis Server name.</span></span> <span data-ttu-id="a013a-140">You can only specify one server per gateway.</span><span class="sxs-lookup"><span data-stu-id="a013a-140">You can only specify one server per gateway.</span></span> <span data-ttu-id="a013a-141">Click **Configure** and you're good to go.</span><span class="sxs-lookup"><span data-stu-id="a013a-141">Click **Configure** and you're good to go.</span></span>

    ![sign in to azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-gateway/aas-gateway-configure-server.png)

## <a name="how-it-works"></a><span data-ttu-id="a013a-143">How it works</span><span class="sxs-lookup"><span data-stu-id="a013a-143">How it works</span></span>
<span data-ttu-id="a013a-144">The gateway runs as a Windows service, **On-premises data gateway**, on a computer in your organization's network.</span><span class="sxs-lookup"><span data-stu-id="a013a-144">The gateway runs as a Windows service, **On-premises data gateway**, on a computer in your organization's network.</span></span> <span data-ttu-id="a013a-145">The gateway you install for use with Azure Analysis Services is based on the same gateway used for other services like Power BI, but with some differences in how it's configured.</span><span class="sxs-lookup"><span data-stu-id="a013a-145">The gateway you install for use with Azure Analysis Services is based on the same gateway used for other services like Power BI, but with some differences in how it's configured.</span></span>

![How it works](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="a013a-147">Queries and data flow work like this:</span><span class="sxs-lookup"><span data-stu-id="a013a-147">Queries and data flow work like this:</span></span>

1. <span data-ttu-id="a013a-148">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span><span class="sxs-lookup"><span data-stu-id="a013a-148">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="a013a-149">It's then sent to a queue for the gateway to process.</span><span class="sxs-lookup"><span data-stu-id="a013a-149">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="a013a-150">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="a013a-150">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="a013a-151">The on-premises data gateway polls the Azure Service Bus for pending requests.</span><span class="sxs-lookup"><span data-stu-id="a013a-151">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="a013a-152">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span><span class="sxs-lookup"><span data-stu-id="a013a-152">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="a013a-153">The gateway sends the query to the data source for execution.</span><span class="sxs-lookup"><span data-stu-id="a013a-153">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="a013a-154">The results are sent from the data source, back to the gateway, and then onto the cloud service.</span><span class="sxs-lookup"><span data-stu-id="a013a-154">The results are sent from the data source, back to the gateway, and then onto the cloud service.</span></span>

## <a name="windows-service-account"></a><span data-ttu-id="a013a-155">Windows Service account</span><span class="sxs-lookup"><span data-stu-id="a013a-155">Windows Service account</span></span>
<span data-ttu-id="a013a-156">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span><span class="sxs-lookup"><span data-stu-id="a013a-156">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="a013a-157">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span><span class="sxs-lookup"><span data-stu-id="a013a-157">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="a013a-158">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a013a-158">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="a013a-159">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span><span class="sxs-lookup"><span data-stu-id="a013a-159">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <a name="ports"></a><span data-ttu-id="a013a-160">Ports</span><span class="sxs-lookup"><span data-stu-id="a013a-160">Ports</span></span>
<span data-ttu-id="a013a-161">The gateway creates an outbound connection to Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a013a-161">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="a013a-162">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span><span class="sxs-lookup"><span data-stu-id="a013a-162">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="a013a-163">The gateway does not require inbound ports.</span><span class="sxs-lookup"><span data-stu-id="a013a-163">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="a013a-164">It's recommended you whitelist the IP addresses for your data region in your firewall.</span><span class="sxs-lookup"><span data-stu-id="a013a-164">It's recommended you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="a013a-165">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="a013a-165">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="a013a-166">This list is updated weekly.</span><span class="sxs-lookup"><span data-stu-id="a013a-166">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="a013a-167">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="a013a-167">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="a013a-168">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="a013a-168">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="a013a-169">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="a013a-169">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="a013a-170">The following are the fully qualified domain names used by the gateway.</span><span class="sxs-lookup"><span data-stu-id="a013a-170">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="a013a-171">Domain names</span><span class="sxs-lookup"><span data-stu-id="a013a-171">Domain names</span></span> | <span data-ttu-id="a013a-172">Outbound ports</span><span class="sxs-lookup"><span data-stu-id="a013a-172">Outbound ports</span></span> | <span data-ttu-id="a013a-173">Description</span><span class="sxs-lookup"><span data-stu-id="a013a-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a013a-174">\*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="a013a-174">\*.powerbi.com</span></span> |<span data-ttu-id="a013a-175">80</span><span class="sxs-lookup"><span data-stu-id="a013a-175">80</span></span> |<span data-ttu-id="a013a-176">HTTP used to download the installer.</span><span class="sxs-lookup"><span data-stu-id="a013a-176">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="a013a-177">\*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="a013a-177">\*.powerbi.com</span></span> |<span data-ttu-id="a013a-178">443</span><span class="sxs-lookup"><span data-stu-id="a013a-178">443</span></span> |<span data-ttu-id="a013a-179">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a013a-179">HTTPS</span></span> |
| <span data-ttu-id="a013a-180">\*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="a013a-180">\*.analysis.windows.net</span></span> |<span data-ttu-id="a013a-181">443</span><span class="sxs-lookup"><span data-stu-id="a013a-181">443</span></span> |<span data-ttu-id="a013a-182">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a013a-182">HTTPS</span></span> |
| <span data-ttu-id="a013a-183">\*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="a013a-183">\*.login.windows.net</span></span> |<span data-ttu-id="a013a-184">443</span><span class="sxs-lookup"><span data-stu-id="a013a-184">443</span></span> |<span data-ttu-id="a013a-185">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a013a-185">HTTPS</span></span> |
| <span data-ttu-id="a013a-186">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="a013a-186">\*.servicebus.windows.net</span></span> |<span data-ttu-id="a013a-187">5671-5672</span><span class="sxs-lookup"><span data-stu-id="a013a-187">5671-5672</span></span> |<span data-ttu-id="a013a-188">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="a013a-188">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="a013a-189">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="a013a-189">\*.servicebus.windows.net</span></span> |<span data-ttu-id="a013a-190">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="a013a-190">443, 9350-9354</span></span> |<span data-ttu-id="a013a-191">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span><span class="sxs-lookup"><span data-stu-id="a013a-191">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="a013a-192">\*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="a013a-192">\*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="a013a-193">443</span><span class="sxs-lookup"><span data-stu-id="a013a-193">443</span></span> |<span data-ttu-id="a013a-194">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a013a-194">HTTPS</span></span> |
| <span data-ttu-id="a013a-195">\*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="a013a-195">\*.core.windows.net</span></span> |<span data-ttu-id="a013a-196">443</span><span class="sxs-lookup"><span data-stu-id="a013a-196">443</span></span> |<span data-ttu-id="a013a-197">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a013a-197">HTTPS</span></span> |
| <span data-ttu-id="a013a-198">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a013a-198">login.microsoftonline.com</span></span> |<span data-ttu-id="a013a-199">443</span><span class="sxs-lookup"><span data-stu-id="a013a-199">443</span></span> |<span data-ttu-id="a013a-200">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a013a-200">HTTPS</span></span> |
| <span data-ttu-id="a013a-201">\*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="a013a-201">\*.msftncsi.com</span></span> |<span data-ttu-id="a013a-202">443</span><span class="sxs-lookup"><span data-stu-id="a013a-202">443</span></span> |<span data-ttu-id="a013a-203">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span><span class="sxs-lookup"><span data-stu-id="a013a-203">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="a013a-204">\*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="a013a-204">\*.microsoftonline-p.com</span></span> |<span data-ttu-id="a013a-205">443</span><span class="sxs-lookup"><span data-stu-id="a013a-205">443</span></span> |<span data-ttu-id="a013a-206">Used for authentication depending on configuration.</span><span class="sxs-lookup"><span data-stu-id="a013a-206">Used for authentication depending on configuration.</span></span> |

### <a name="forcing-https-communication-with-azure-service-bus"></a><span data-ttu-id="a013a-207">Forcing HTTPS communication with Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="a013a-207">Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="a013a-208">You can force the gateway to communicate with Azure Service Bus using HTTPS instead of direct TCP; however, this can greatly reduce performance.</span><span class="sxs-lookup"><span data-stu-id="a013a-208">You can force the gateway to communicate with Azure Service Bus using HTTPS instead of direct TCP; however, this can greatly reduce performance.</span></span> <span data-ttu-id="a013a-209">You need to modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file.</span><span class="sxs-lookup"><span data-stu-id="a013a-209">You need to modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file.</span></span> <span data-ttu-id="a013a-210">Change the value from `AutoDetect` to `Https`.</span><span class="sxs-lookup"><span data-stu-id="a013a-210">Change the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="a013a-211">This file is located, by default, at *C:\Program Files\On-premises data gateway*.</span><span class="sxs-lookup"><span data-stu-id="a013a-211">This file is located, by default, at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```


## <a name="troubleshooting"></a><span data-ttu-id="a013a-212">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a013a-212">Troubleshooting</span></span>
<span data-ttu-id="a013a-213">Under the hood, the on-premises data gateway used for connecting Azure Analysis Services to your on-premises data sources is the same gateway used with Power BI.</span><span class="sxs-lookup"><span data-stu-id="a013a-213">Under the hood, the on-premises data gateway used for connecting Azure Analysis Services to your on-premises data sources is the same gateway used with Power BI.</span></span>

<span data-ttu-id="a013a-214">If you’re having trouble when installing and configuring a gateway, be sure to see [Troubleshooting the Power BI Gateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem-tshoot/).</span><span class="sxs-lookup"><span data-stu-id="a013a-214">If you’re having trouble when installing and configuring a gateway, be sure to see [Troubleshooting the Power BI Gateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem-tshoot/).</span></span> <span data-ttu-id="a013a-215">If you think you are having an issue with your firewall, see the firewall or proxy sections.</span><span class="sxs-lookup"><span data-stu-id="a013a-215">If you think you are having an issue with your firewall, see the firewall or proxy sections.</span></span>

<span data-ttu-id="a013a-216">If you think you're encountering proxy issues, with the gateway, see [Configuring proxy settings for the Power BI Gateways](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="a013a-216">If you think you're encountering proxy issues, with the gateway, see [Configuring proxy settings for the Power BI Gateways](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy.md).</span></span>

### <a name="telemetry"></a><span data-ttu-id="a013a-217">Telemetry</span><span class="sxs-lookup"><span data-stu-id="a013a-217">Telemetry</span></span>
<span data-ttu-id="a013a-218">Telemetry can be used for monitoring and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a013a-218">Telemetry can be used for monitoring and troubleshooting.</span></span> 

<span data-ttu-id="a013a-219">**To turn on telemetry**</span><span class="sxs-lookup"><span data-stu-id="a013a-219">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="a013a-220">Check the On-premises data gateway client directory on the computer.</span><span class="sxs-lookup"><span data-stu-id="a013a-220">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="a013a-221">Typically, it's %systemdrive%\Program Files\On-premises data gateway.</span><span class="sxs-lookup"><span data-stu-id="a013a-221">Typically, it's %systemdrive%\Program Files\On-premises data gateway.</span></span> <span data-ttu-id="a013a-222">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span><span class="sxs-lookup"><span data-stu-id="a013a-222">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="a013a-223">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span><span class="sxs-lookup"><span data-stu-id="a013a-223">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="a013a-224">Change the SendTelemetry setting to true.</span><span class="sxs-lookup"><span data-stu-id="a013a-224">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="a013a-225">Save your changes and restart the Windows service: On-premises data gateway service.</span><span class="sxs-lookup"><span data-stu-id="a013a-225">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="a013a-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="a013a-226">Next steps</span></span>
* [<span data-ttu-id="a013a-227">Manage Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a013a-227">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="a013a-228">Get data from Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a013a-228">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)


