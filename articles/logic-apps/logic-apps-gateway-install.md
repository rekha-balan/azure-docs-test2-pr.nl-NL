---
title: Install on-premises data gateway - Azure Logic Apps | Microsoft Docs
description: Access on-premises data from logic apps by installing an on-premises data gateway
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/05/2016
ms.author: jehollan
ms.openlocfilehash: b9971117d5f61669a5161a28c96b11b2fd600b61
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548720"
---
# <a name="install-an-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="082a7-103">Install an on-premises data gateway for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="082a7-103">Install an on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="082a7-104">The on-premises data gateway supports these connections:</span><span class="sxs-lookup"><span data-stu-id="082a7-104">The on-premises data gateway supports these connections:</span></span>

*   <span data-ttu-id="082a7-105">BizTalk Server</span><span class="sxs-lookup"><span data-stu-id="082a7-105">BizTalk Server</span></span>
*   <span data-ttu-id="082a7-106">DB2</span><span class="sxs-lookup"><span data-stu-id="082a7-106">DB2</span></span>  
*   <span data-ttu-id="082a7-107">File System</span><span class="sxs-lookup"><span data-stu-id="082a7-107">File System</span></span>
*   <span data-ttu-id="082a7-108">Informix</span><span class="sxs-lookup"><span data-stu-id="082a7-108">Informix</span></span>
*   <span data-ttu-id="082a7-109">MQ</span><span class="sxs-lookup"><span data-stu-id="082a7-109">MQ</span></span>
*   <span data-ttu-id="082a7-110">MySQL</span><span class="sxs-lookup"><span data-stu-id="082a7-110">MySQL</span></span>
*   <span data-ttu-id="082a7-111">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="082a7-111">Oracle Database</span></span> 
*   <span data-ttu-id="082a7-112">SAP Application Server</span><span class="sxs-lookup"><span data-stu-id="082a7-112">SAP Application Server</span></span> 
*   <span data-ttu-id="082a7-113">SAP Message Server</span><span class="sxs-lookup"><span data-stu-id="082a7-113">SAP Message Server</span></span>
*   <span data-ttu-id="082a7-114">SharePoint for HTTP only, not HTTPS</span><span class="sxs-lookup"><span data-stu-id="082a7-114">SharePoint for HTTP only, not HTTPS</span></span>
*   <span data-ttu-id="082a7-115">SQL Server</span><span class="sxs-lookup"><span data-stu-id="082a7-115">SQL Server</span></span>
*   <span data-ttu-id="082a7-116">Teradata</span><span class="sxs-lookup"><span data-stu-id="082a7-116">Teradata</span></span>

<span data-ttu-id="082a7-117">For more information about these connections, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="082a7-117">For more information about these connections, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span>

## <a name="installation-and-configuration"></a><span data-ttu-id="082a7-118">Installation and configuration</span><span class="sxs-lookup"><span data-stu-id="082a7-118">Installation and configuration</span></span>

### <a name="requirements"></a><span data-ttu-id="082a7-119">Requirements</span><span class="sxs-lookup"><span data-stu-id="082a7-119">Requirements</span></span>

<span data-ttu-id="082a7-120">Minimum:</span><span class="sxs-lookup"><span data-stu-id="082a7-120">Minimum:</span></span>

* <span data-ttu-id="082a7-121">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="082a7-121">.NET 4.5 Framework</span></span>
* <span data-ttu-id="082a7-122">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span><span class="sxs-lookup"><span data-stu-id="082a7-122">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="082a7-123">Recommended:</span><span class="sxs-lookup"><span data-stu-id="082a7-123">Recommended:</span></span>

* <span data-ttu-id="082a7-124">8 Core CPU</span><span class="sxs-lookup"><span data-stu-id="082a7-124">8 Core CPU</span></span>
* <span data-ttu-id="082a7-125">8 GB Memory</span><span class="sxs-lookup"><span data-stu-id="082a7-125">8 GB Memory</span></span>
* <span data-ttu-id="082a7-126">64-bit version of Windows 2012 R2 (or later)</span><span class="sxs-lookup"><span data-stu-id="082a7-126">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="082a7-127">Related considerations:</span><span class="sxs-lookup"><span data-stu-id="082a7-127">Related considerations:</span></span>

* <span data-ttu-id="082a7-128">Only install the on-premises data gateway on a local machine.</span><span class="sxs-lookup"><span data-stu-id="082a7-128">Only install the on-premises data gateway on a local machine.</span></span>
<span data-ttu-id="082a7-129">You can't install the gateway on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="082a7-129">You can't install the gateway on a domain controller.</span></span>

* <span data-ttu-id="082a7-130">Don't install the gateway on a computer that might turn off, go to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span><span class="sxs-lookup"><span data-stu-id="082a7-130">Don't install the gateway on a computer that might turn off, go to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="082a7-131">Also, gateway performance might suffer over a wireless network.</span><span class="sxs-lookup"><span data-stu-id="082a7-131">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="082a7-132">You can only use a work or school email address in Azure, so that you can associate the on-premises data gateway with your Azure Active Directory-based account.</span><span class="sxs-lookup"><span data-stu-id="082a7-132">You can only use a work or school email address in Azure, so that you can associate the on-premises data gateway with your Azure Active Directory-based account.</span></span>

    <span data-ttu-id="082a7-133">If you are using a Microsoft account, like @outlook.com,   you can use your Azure account to   [create a work or school email address](../virtual-machines/windows/create-aad-work-id.md#locate-your-default-directory-in-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="082a7-133">If you are using a Microsoft account, like @outlook.com,   you can use your Azure account to   [create a work or school email address](../virtual-machines/windows/create-aad-work-id.md#locate-your-default-directory-in-the-azure-classic-portal).</span></span>

### <a name="install-the-gateway"></a><span data-ttu-id="082a7-134">Install the gateway</span><span class="sxs-lookup"><span data-stu-id="082a7-134">Install the gateway</span></span>

1.  <span data-ttu-id="082a7-135">[Download installer for the on-premises data gateway here](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="082a7-135">[Download installer for the on-premises data gateway here](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2.  <span data-ttu-id="082a7-136">Specify **On-premises data gateway** as the mode.</span><span class="sxs-lookup"><span data-stu-id="082a7-136">Specify **On-premises data gateway** as the mode.</span></span>

3. <span data-ttu-id="082a7-137">Sign in with your Azure work or school account.</span><span class="sxs-lookup"><span data-stu-id="082a7-137">Sign in with your Azure work or school account.</span></span> 

4. <span data-ttu-id="082a7-138">Set up a new gateway, or you can migrate, restore, or take over an existing gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-138">Set up a new gateway, or you can migrate, restore, or take over an existing gateway.</span></span>

    <span data-ttu-id="082a7-139">To configure a gateway, provide a name for your gateway and a recovery key,  then choose **Configure**.</span><span class="sxs-lookup"><span data-stu-id="082a7-139">To configure a gateway, provide a name for your gateway and a recovery key,  then choose **Configure**.</span></span>
  
    <span data-ttu-id="082a7-140">Specify a recovery key that contains at least eight characters, and keep the key in a safe place.</span><span class="sxs-lookup"><span data-stu-id="082a7-140">Specify a recovery key that contains at least eight characters, and keep the key in a safe place.</span></span> <span data-ttu-id="082a7-141">You need this key if you want to migrate, restore, or take over the gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-141">You need this key if you want to migrate, restore, or take over the gateway.</span></span>

    <span data-ttu-id="082a7-142">To migrate, restore, or take over an existing gateway,  provide the recovery key that was specified when the gateway was created.</span><span class="sxs-lookup"><span data-stu-id="082a7-142">To migrate, restore, or take over an existing gateway,  provide the recovery key that was specified when the gateway was created.</span></span>

### <a name="restart-the-gateway"></a><span data-ttu-id="082a7-143">Restart the gateway</span><span class="sxs-lookup"><span data-stu-id="082a7-143">Restart the gateway</span></span>

<span data-ttu-id="082a7-144">The gateway runs as a Windows service, so like any other Windows service, you can start and stop the service in multiple ways.</span><span class="sxs-lookup"><span data-stu-id="082a7-144">The gateway runs as a Windows service, so like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="082a7-145">For example, you can open a command prompt with elevated permissions on the machine where the gateway is running, and run either these commands:</span><span class="sxs-lookup"><span data-stu-id="082a7-145">For example, you can open a command prompt with elevated permissions on the machine where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="082a7-146">To stop the service, run this command:</span><span class="sxs-lookup"><span data-stu-id="082a7-146">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="082a7-147">To start the service, run this command:</span><span class="sxs-lookup"><span data-stu-id="082a7-147">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="082a7-148">Configure a firewall or proxy</span><span class="sxs-lookup"><span data-stu-id="082a7-148">Configure a firewall or proxy</span></span>

<span data-ttu-id="082a7-149">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="082a7-149">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="082a7-150">You can verify whether your firewall, or proxy, might block connections by running the following command from a PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="082a7-150">You can verify whether your firewall, or proxy, might block connections by running the following command from a PowerShell prompt.</span></span> <span data-ttu-id="082a7-151">This command tests connectivity to the Azure Service Bus and only network connectivity, so the command doesn't have anything to do with the cloud server service or the gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-151">This command tests connectivity to the Azure Service Bus and only network connectivity, so the command doesn't have anything to do with the cloud server service or the gateway.</span></span> <span data-ttu-id="082a7-152">This test helps determine whether your machine can actually connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="082a7-152">This test helps determine whether your machine can actually connect to the internet.</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

<span data-ttu-id="082a7-153">The results should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="082a7-153">The results should look similar to this example.</span></span> <span data-ttu-id="082a7-154">If **TcpTestSucceeded** is not true, you might be blocked by a firewall.</span><span class="sxs-lookup"><span data-stu-id="082a7-154">If **TcpTestSucceeded** is not true, you might be blocked by a firewall.</span></span>

```
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="082a7-155">If you want to be exhaustive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span><span class="sxs-lookup"><span data-stu-id="082a7-155">If you want to be exhaustive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="082a7-156">The firewall might also block connections that the Azure Service Bus makes to the Azure data centers.</span><span class="sxs-lookup"><span data-stu-id="082a7-156">The firewall might also block connections that the Azure Service Bus makes to the Azure data centers.</span></span> <span data-ttu-id="082a7-157">If so, approve (unblock) all the IP addresses for those data centers in your region.</span><span class="sxs-lookup"><span data-stu-id="082a7-157">If so, approve (unblock) all the IP addresses for those data centers in your region.</span></span>
<span data-ttu-id="082a7-158">You can get a list of [Azure IP addresses here](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="082a7-158">You can get a list of [Azure IP addresses here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="configure-ports"></a><span data-ttu-id="082a7-159">Configure ports</span><span class="sxs-lookup"><span data-stu-id="082a7-159">Configure ports</span></span>
<span data-ttu-id="082a7-160">The gateway creates an outbound connection to Azure Service Bus and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span><span class="sxs-lookup"><span data-stu-id="082a7-160">The gateway creates an outbound connection to Azure Service Bus and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="082a7-161">The gateway doesn't require inbound ports.</span><span class="sxs-lookup"><span data-stu-id="082a7-161">The gateway doesn't require inbound ports.</span></span>

<span data-ttu-id="082a7-162">Learn more about [hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="082a7-162">Learn more about [hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="082a7-163">DOMAIN NAMES</span><span class="sxs-lookup"><span data-stu-id="082a7-163">DOMAIN NAMES</span></span> | <span data-ttu-id="082a7-164">OUTBOUND PORTS</span><span class="sxs-lookup"><span data-stu-id="082a7-164">OUTBOUND PORTS</span></span> | <span data-ttu-id="082a7-165">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="082a7-165">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="082a7-166">\*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="082a7-166">\*.analysis.windows.net</span></span> | <span data-ttu-id="082a7-167">443</span><span class="sxs-lookup"><span data-stu-id="082a7-167">443</span></span> | <span data-ttu-id="082a7-168">HTTPS</span><span class="sxs-lookup"><span data-stu-id="082a7-168">HTTPS</span></span> | 
| <span data-ttu-id="082a7-169">\*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="082a7-169">\*.login.windows.net</span></span> | <span data-ttu-id="082a7-170">443</span><span class="sxs-lookup"><span data-stu-id="082a7-170">443</span></span> | <span data-ttu-id="082a7-171">HTTPS</span><span class="sxs-lookup"><span data-stu-id="082a7-171">HTTPS</span></span> | 
| <span data-ttu-id="082a7-172">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="082a7-172">\*.servicebus.windows.net</span></span> | <span data-ttu-id="082a7-173">5671-5672</span><span class="sxs-lookup"><span data-stu-id="082a7-173">5671-5672</span></span> | <span data-ttu-id="082a7-174">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="082a7-174">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="082a7-175">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="082a7-175">\*.servicebus.windows.net</span></span> | <span data-ttu-id="082a7-176">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="082a7-176">443, 9350-9354</span></span> | <span data-ttu-id="082a7-177">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span><span class="sxs-lookup"><span data-stu-id="082a7-177">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="082a7-178">\*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="082a7-178">\*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="082a7-179">443</span><span class="sxs-lookup"><span data-stu-id="082a7-179">443</span></span> | <span data-ttu-id="082a7-180">HTTPS</span><span class="sxs-lookup"><span data-stu-id="082a7-180">HTTPS</span></span> | 
| <span data-ttu-id="082a7-181">\*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="082a7-181">\*.core.windows.net</span></span> | <span data-ttu-id="082a7-182">443</span><span class="sxs-lookup"><span data-stu-id="082a7-182">443</span></span> | <span data-ttu-id="082a7-183">HTTPS</span><span class="sxs-lookup"><span data-stu-id="082a7-183">HTTPS</span></span> | 
| <span data-ttu-id="082a7-184">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="082a7-184">login.microsoftonline.com</span></span> | <span data-ttu-id="082a7-185">443</span><span class="sxs-lookup"><span data-stu-id="082a7-185">443</span></span> | <span data-ttu-id="082a7-186">HTTPS</span><span class="sxs-lookup"><span data-stu-id="082a7-186">HTTPS</span></span> | 
| <span data-ttu-id="082a7-187">\*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="082a7-187">\*.msftncsi.com</span></span> | <span data-ttu-id="082a7-188">443</span><span class="sxs-lookup"><span data-stu-id="082a7-188">443</span></span> | <span data-ttu-id="082a7-189">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span><span class="sxs-lookup"><span data-stu-id="082a7-189">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="082a7-190">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="082a7-190">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="082a7-191">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span><span class="sxs-lookup"><span data-stu-id="082a7-191">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

### <a name="sign-in-accounts"></a><span data-ttu-id="082a7-192">Sign-in accounts</span><span class="sxs-lookup"><span data-stu-id="082a7-192">Sign-in accounts</span></span>

<span data-ttu-id="082a7-193">You can sign in with either a work or school account, which is your organization account.</span><span class="sxs-lookup"><span data-stu-id="082a7-193">You can sign in with either a work or school account, which is your organization account.</span></span> <span data-ttu-id="082a7-194">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="082a7-194">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="082a7-195">Your account, within a cloud service, is stored within a tenant in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="082a7-195">Your account, within a cloud service, is stored within a tenant in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="082a7-196">Usually, your Azure AD account's UPN matches the email address.</span><span class="sxs-lookup"><span data-stu-id="082a7-196">Usually, your Azure AD account's UPN matches the email address.</span></span>

### <a name="windows-service-account"></a><span data-ttu-id="082a7-197">Windows service account</span><span class="sxs-lookup"><span data-stu-id="082a7-197">Windows service account</span></span>

<span data-ttu-id="082a7-198">For the Windows service logon credential, the on-premises data gateway is set up to use NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="082a7-198">For the Windows service logon credential, the on-premises data gateway is set up to use NT SERVICE\PBIEgwService.</span></span> <span data-ttu-id="082a7-199">By default, the gateway has the right for "Log on as a service", within the context of the machine where you installing the gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-199">By default, the gateway has the right for "Log on as a service", within the context of the machine where you installing the gateway.</span></span>

<span data-ttu-id="082a7-200">This service account isn't same account used for connecting to on-premises data sources, nor the work or school account that you use to sign in to cloud services.</span><span class="sxs-lookup"><span data-stu-id="082a7-200">This service account isn't same account used for connecting to on-premises data sources, nor the work or school account that you use to sign in to cloud services.</span></span>

## <a name="how-the-gateway-works"></a><span data-ttu-id="082a7-201">How the gateway works</span><span class="sxs-lookup"><span data-stu-id="082a7-201">How the gateway works</span></span>
<span data-ttu-id="082a7-202">When others interact with an element that's connected to an on-premises data source:</span><span class="sxs-lookup"><span data-stu-id="082a7-202">When others interact with an element that's connected to an on-premises data source:</span></span>

1. <span data-ttu-id="082a7-203">The cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span><span class="sxs-lookup"><span data-stu-id="082a7-203">The cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>
2. <span data-ttu-id="082a7-204">The service analyzes the query and pushes the request to the Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="082a7-204">The service analyzes the query and pushes the request to the Azure Service Bus.</span></span>
3. <span data-ttu-id="082a7-205">The on-premises data gateway polls the Azure Service Bus for pending requests.</span><span class="sxs-lookup"><span data-stu-id="082a7-205">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="082a7-206">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span><span class="sxs-lookup"><span data-stu-id="082a7-206">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>
5. <span data-ttu-id="082a7-207">The gateway sends the query to the data source for execution.</span><span class="sxs-lookup"><span data-stu-id="082a7-207">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="082a7-208">The results are sent from the data source, back to the gateway, and then to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="082a7-208">The results are sent from the data source, back to the gateway, and then to the cloud service.</span></span> <span data-ttu-id="082a7-209">The service then uses the results.</span><span class="sxs-lookup"><span data-stu-id="082a7-209">The service then uses the results.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="082a7-210">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="082a7-210">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="082a7-211">General</span><span class="sxs-lookup"><span data-stu-id="082a7-211">General</span></span>

<span data-ttu-id="082a7-212">**Question**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="082a7-212">**Question**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/>
<span data-ttu-id="082a7-213">**Answer**: No.</span><span class="sxs-lookup"><span data-stu-id="082a7-213">**Answer**: No.</span></span> <span data-ttu-id="082a7-214">A gateway connects to on-premises data sources only.</span><span class="sxs-lookup"><span data-stu-id="082a7-214">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="082a7-215">**Question**: What is the actual Windows service called?</span><span class="sxs-lookup"><span data-stu-id="082a7-215">**Question**: What is the actual Windows service called?</span></span><br/>
<span data-ttu-id="082a7-216">**Answer**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span><span class="sxs-lookup"><span data-stu-id="082a7-216">**Answer**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="082a7-217">**Question**: Are there any inbound connections to the gateway from the cloud?</span><span class="sxs-lookup"><span data-stu-id="082a7-217">**Question**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/>
<span data-ttu-id="082a7-218">**Answer**: No.</span><span class="sxs-lookup"><span data-stu-id="082a7-218">**Answer**: No.</span></span> <span data-ttu-id="082a7-219">The gateway uses outbound connections to Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="082a7-219">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="082a7-220">**Question**: What if I block outbound connections?</span><span class="sxs-lookup"><span data-stu-id="082a7-220">**Question**: What if I block outbound connections?</span></span> <span data-ttu-id="082a7-221">What do I need to open?</span><span class="sxs-lookup"><span data-stu-id="082a7-221">What do I need to open?</span></span> <br/>
<span data-ttu-id="082a7-222">**Answer**: See the ports and hosts that the gateway uses.</span><span class="sxs-lookup"><span data-stu-id="082a7-222">**Answer**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="082a7-223">**Question**: Does the gateway have to be installed on the same machine as the data source?</span><span class="sxs-lookup"><span data-stu-id="082a7-223">**Question**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/>
<span data-ttu-id="082a7-224">**Answer**: No.</span><span class="sxs-lookup"><span data-stu-id="082a7-224">**Answer**: No.</span></span> <span data-ttu-id="082a7-225">The gateway connects to the data source using the connection information that was provided.</span><span class="sxs-lookup"><span data-stu-id="082a7-225">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="082a7-226">Consider the gateway as a client application in this sense.</span><span class="sxs-lookup"><span data-stu-id="082a7-226">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="082a7-227">The gateway just needs the capability to connect to the server name that was provided.</span><span class="sxs-lookup"><span data-stu-id="082a7-227">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<span data-ttu-id="082a7-228">**Question**: What is the latency for running queries to a data source from the gateway?</span><span class="sxs-lookup"><span data-stu-id="082a7-228">**Question**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="082a7-229">What is the best architecture?</span><span class="sxs-lookup"><span data-stu-id="082a7-229">What is the best architecture?</span></span> <br/>
<span data-ttu-id="082a7-230">**Answer**: To reduce network latency, install the gateway as close to the data source as possible.</span><span class="sxs-lookup"><span data-stu-id="082a7-230">**Answer**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="082a7-231">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span><span class="sxs-lookup"><span data-stu-id="082a7-231">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="082a7-232">Consider the data centers too.</span><span class="sxs-lookup"><span data-stu-id="082a7-232">Consider the data centers too.</span></span> <span data-ttu-id="082a7-233">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span><span class="sxs-lookup"><span data-stu-id="082a7-233">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="082a7-234">This proximity minimizes latency and avoids egress charges on the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="082a7-234">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="082a7-235">**Question**: Are there any requirements for network bandwidth?</span><span class="sxs-lookup"><span data-stu-id="082a7-235">**Question**: Are there any requirements for network bandwidth?</span></span> <br/>
<span data-ttu-id="082a7-236">**Answer**: We recommend that your network connection has good throughput.</span><span class="sxs-lookup"><span data-stu-id="082a7-236">**Answer**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="082a7-237">Every environment is different, and the amount of data being sent affects the results.</span><span class="sxs-lookup"><span data-stu-id="082a7-237">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="082a7-238">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure data centers.</span><span class="sxs-lookup"><span data-stu-id="082a7-238">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure data centers.</span></span>

<span data-ttu-id="082a7-239">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span><span class="sxs-lookup"><span data-stu-id="082a7-239">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="082a7-240">**Question**: Can the gateway Windows service run with an Azure Active Directory account?</span><span class="sxs-lookup"><span data-stu-id="082a7-240">**Question**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/>
<span data-ttu-id="082a7-241">**Answer**: No.</span><span class="sxs-lookup"><span data-stu-id="082a7-241">**Answer**: No.</span></span> <span data-ttu-id="082a7-242">The Windows service must have a valid Windows account.</span><span class="sxs-lookup"><span data-stu-id="082a7-242">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="082a7-243">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="082a7-243">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

<span data-ttu-id="082a7-244">**Question**: How are results sent back to the cloud?</span><span class="sxs-lookup"><span data-stu-id="082a7-244">**Question**: How are results sent back to the cloud?</span></span> <br/>
<span data-ttu-id="082a7-245">**Answer**: Results are sent through the Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="082a7-245">**Answer**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="082a7-246">**Question**: Where are my credentials stored?</span><span class="sxs-lookup"><span data-stu-id="082a7-246">**Question**: Where are my credentials stored?</span></span> <br/>
<span data-ttu-id="082a7-247">**Answer**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span><span class="sxs-lookup"><span data-stu-id="082a7-247">**Answer**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="082a7-248">The credentials are decrypted at the on-premises gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-248">The credentials are decrypted at the on-premises gateway.</span></span>

### <a name="high-availabilitydisaster-recovery"></a><span data-ttu-id="082a7-249">High availability/disaster recovery</span><span class="sxs-lookup"><span data-stu-id="082a7-249">High availability/disaster recovery</span></span>
<span data-ttu-id="082a7-250">**Question**: Are there any plans for enabling high availability scenarios with the gateway?</span><span class="sxs-lookup"><span data-stu-id="082a7-250">**Question**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/>
<span data-ttu-id="082a7-251">**Answer**: These scenarios are on the roadmap, but we don't have a timeline yet.</span><span class="sxs-lookup"><span data-stu-id="082a7-251">**Answer**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

<span data-ttu-id="082a7-252">**Question**: What options are available for disaster recovery?</span><span class="sxs-lookup"><span data-stu-id="082a7-252">**Question**: What options are available for disaster recovery?</span></span> <br/>
<span data-ttu-id="082a7-253">**Answer**: You can use the recovery key to restore or move a gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-253">**Answer**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="082a7-254">When you install the gateway, specify the recovery key.</span><span class="sxs-lookup"><span data-stu-id="082a7-254">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="082a7-255">**Question**: What is the benefit of the recovery key?</span><span class="sxs-lookup"><span data-stu-id="082a7-255">**Question**: What is the benefit of the recovery key?</span></span> <br/>
<span data-ttu-id="082a7-256">**Answer**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span><span class="sxs-lookup"><span data-stu-id="082a7-256">**Answer**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="082a7-257">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="082a7-257">Troubleshooting</span></span>

<span data-ttu-id="082a7-258">**Question**: Where are the gateway logs?</span><span class="sxs-lookup"><span data-stu-id="082a7-258">**Question**: Where are the gateway logs?</span></span> <br/>
<span data-ttu-id="082a7-259">**Answer**: See Tools later in this topic.</span><span class="sxs-lookup"><span data-stu-id="082a7-259">**Answer**: See Tools later in this topic.</span></span>

<span data-ttu-id="082a7-260">**Question**: How can I see what queries are being sent to the on-premises data source?</span><span class="sxs-lookup"><span data-stu-id="082a7-260">**Question**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/>
<span data-ttu-id="082a7-261">**Answer**: You can enable query tracing, which includes the queries that are sent.</span><span class="sxs-lookup"><span data-stu-id="082a7-261">**Answer**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="082a7-262">Remember to change query tracing back to the original value when done troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="082a7-262">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="082a7-263">Leaving query tracing turned on creates larger logs.</span><span class="sxs-lookup"><span data-stu-id="082a7-263">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="082a7-264">You can also look at tools that your data source has for tracing queries.</span><span class="sxs-lookup"><span data-stu-id="082a7-264">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="082a7-265">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="082a7-265">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="082a7-266">Update to the latest version</span><span class="sxs-lookup"><span data-stu-id="082a7-266">Update to the latest version</span></span>

<span data-ttu-id="082a7-267">Many issues can surface when the gateway version becomes outdated.</span><span class="sxs-lookup"><span data-stu-id="082a7-267">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="082a7-268">As good general practice, make sure that you use the latest version.</span><span class="sxs-lookup"><span data-stu-id="082a7-268">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="082a7-269">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span><span class="sxs-lookup"><span data-stu-id="082a7-269">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="082a7-270">Error: Failed to add user to group.</span><span class="sxs-lookup"><span data-stu-id="082a7-270">Error: Failed to add user to group.</span></span> <span data-ttu-id="082a7-271">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="082a7-271">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="082a7-272">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span><span class="sxs-lookup"><span data-stu-id="082a7-272">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="082a7-273">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span><span class="sxs-lookup"><span data-stu-id="082a7-273">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="082a7-274">Tools</span><span class="sxs-lookup"><span data-stu-id="082a7-274">Tools</span></span>
### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="082a7-275">Collect logs from the gateway configurer</span><span class="sxs-lookup"><span data-stu-id="082a7-275">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="082a7-276">You can collect several logs for the gateway.</span><span class="sxs-lookup"><span data-stu-id="082a7-276">You can collect several logs for the gateway.</span></span> <span data-ttu-id="082a7-277">Always start with the logs!</span><span class="sxs-lookup"><span data-stu-id="082a7-277">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="082a7-278">Installer logs</span><span class="sxs-lookup"><span data-stu-id="082a7-278">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="082a7-279">Configuration logs</span><span class="sxs-lookup"><span data-stu-id="082a7-279">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="082a7-280">Enterprise gateway service logs</span><span class="sxs-lookup"><span data-stu-id="082a7-280">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="082a7-281">Event logs</span><span class="sxs-lookup"><span data-stu-id="082a7-281">Event logs</span></span>

<span data-ttu-id="082a7-282">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span><span class="sxs-lookup"><span data-stu-id="082a7-282">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="082a7-283">Fiddler Trace</span><span class="sxs-lookup"><span data-stu-id="082a7-283">Fiddler Trace</span></span>

<span data-ttu-id="082a7-284">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="082a7-284">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="082a7-285">You can see this traffic with the Power BI service from the client machine.</span><span class="sxs-lookup"><span data-stu-id="082a7-285">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="082a7-286">This service might show errors and other related information.</span><span class="sxs-lookup"><span data-stu-id="082a7-286">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="082a7-287">Next Steps</span><span class="sxs-lookup"><span data-stu-id="082a7-287">Next Steps</span></span>
    
* [<span data-ttu-id="082a7-288">Connect to on-premises data from logic apps</span><span class="sxs-lookup"><span data-stu-id="082a7-288">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="082a7-289">Enterprise integration features</span><span class="sxs-lookup"><span data-stu-id="082a7-289">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="082a7-290">Connectors for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="082a7-290">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
