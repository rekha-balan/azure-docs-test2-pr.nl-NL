---
title: Work with existing on-premises proxy servers and Azure AD | Microsoft Docs
description: Covers how to work with existing on-premises proxy servers.
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
ms.date: 08/31/2017
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7f9d74ce60d2a433f6bb63be4f131ac430452036
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869906"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="d7ac1-103">Work with existing on-premises proxy servers</span><span class="sxs-lookup"><span data-stu-id="d7ac1-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="d7ac1-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="d7ac1-105">It is intended for customers with network environments that have existing proxies.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="d7ac1-106">We start by looking at these main deployment scenarios:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="d7ac1-107">Configure connectors to bypass your on-premises outbound proxies.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="d7ac1-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="d7ac1-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="d7ac1-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-connectors.md).</span></span>

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="d7ac1-110">Bypass outbound proxies</span><span class="sxs-lookup"><span data-stu-id="d7ac1-110">Bypass outbound proxies</span></span>

<span data-ttu-id="d7ac1-111">Connectors have underlying OS components that make outbound requests.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-111">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="d7ac1-112">These components automatically attempt to locate a proxy server on the network using Web Proxy Auto-Discovery (WPAD).</span><span class="sxs-lookup"><span data-stu-id="d7ac1-112">These components automatically attempt to locate a proxy server on the network using Web Proxy Auto-Discovery (WPAD).</span></span>

<span data-ttu-id="d7ac1-113">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-113">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="d7ac1-114">If the lookup resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-114">If the lookup resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="d7ac1-115">This request becomes the proxy configuration script in your environment.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-115">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="d7ac1-116">The connector uses this script to select an outbound proxy server.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-116">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="d7ac1-117">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-117">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="d7ac1-118">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-118">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="d7ac1-119">We recommend this approach, as long as your network policy allows for it, because it means that you have one less configuration to maintain.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-119">We recommend this approach, as long as your network policy allows for it, because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="d7ac1-120">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-120">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="d7ac1-121">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-121">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file.</span></span> <span data-ttu-id="d7ac1-122">This file is located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-122">This file is located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="d7ac1-123">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-123">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="d7ac1-124">Use the outbound proxy server</span><span class="sxs-lookup"><span data-stu-id="d7ac1-124">Use the outbound proxy server</span></span>

<span data-ttu-id="d7ac1-125">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-125">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="d7ac1-126">As a result, bypassing the proxy is not an option.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-126">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="d7ac1-127">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-127">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Configuring connector traffic to go through an outbound proxy to Azure AD Application Proxy](./media/application-proxy-configure-connectors-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="d7ac1-129">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-129">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

>[!NOTE]
><span data-ttu-id="d7ac1-130">Application Proxy does not support authentication to other proxies.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-130">Application Proxy does not support authentication to other proxies.</span></span> <span data-ttu-id="d7ac1-131">The connector/updater network service accounts should be able to connect to the proxy without being challenged for authentication.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-131">The connector/updater network service accounts should be able to connect to the proxy without being challenged for authentication.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="d7ac1-132">Step 1: Configure the connector and related services to go through the outbound proxy</span><span class="sxs-lookup"><span data-stu-id="d7ac1-132">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="d7ac1-133">If WPAD is enabled in the environment and configured appropriately, the connector automatically discovers the outbound proxy server and attempt to use it.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-133">If WPAD is enabled in the environment and configured appropriately, the connector automatically discovers the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="d7ac1-134">However, you can explicitly configure the connector to go through an outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-134">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="d7ac1-135">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-135">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="d7ac1-136">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-136">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="d7ac1-137">Next, configure the Connector Updater service to use the proxy by making a similar change to the C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config file.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-137">Next, configure the Connector Updater service to use the proxy by making a similar change to the C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config file.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="d7ac1-138">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span><span class="sxs-lookup"><span data-stu-id="d7ac1-138">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="d7ac1-139">There are four aspects to consider at the outbound proxy:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-139">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="d7ac1-140">Proxy outbound rules</span><span class="sxs-lookup"><span data-stu-id="d7ac1-140">Proxy outbound rules</span></span>
* <span data-ttu-id="d7ac1-141">Proxy authentication</span><span class="sxs-lookup"><span data-stu-id="d7ac1-141">Proxy authentication</span></span>
* <span data-ttu-id="d7ac1-142">Proxy ports</span><span class="sxs-lookup"><span data-stu-id="d7ac1-142">Proxy ports</span></span>
* <span data-ttu-id="d7ac1-143">SSL inspection</span><span class="sxs-lookup"><span data-stu-id="d7ac1-143">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="d7ac1-144">Proxy outbound rules</span><span class="sxs-lookup"><span data-stu-id="d7ac1-144">Proxy outbound rules</span></span>
<span data-ttu-id="d7ac1-145">Allow access to the following endpoints for connector service access:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-145">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="d7ac1-146">\*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="d7ac1-146">\*.msappproxy.net</span></span>
* <span data-ttu-id="d7ac1-147">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="d7ac1-147">\*.servicebus.windows.net</span></span>

<span data-ttu-id="d7ac1-148">For initial registration, allow access to the following endpoints:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-148">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="d7ac1-149">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="d7ac1-149">login.windows.net</span></span>
* <span data-ttu-id="d7ac1-150">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d7ac1-150">login.microsoftonline.com</span></span>

<span data-ttu-id="d7ac1-151">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-151">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="d7ac1-152">Allow the connector outbound access to all destinations.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-152">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="d7ac1-153">Allow the connector outbound access to all of the [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d7ac1-153">Allow the connector outbound access to all of the [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="d7ac1-154">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-154">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="d7ac1-155">You need to put a process in place to ensure that your access rules are updated accordingly.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-155">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span> <span data-ttu-id="d7ac1-156">Only using a subset of the IP addresses may cause your configuration to break.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-156">Only using a subset of the IP addresses may cause your configuration to break.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="d7ac1-157">Proxy authentication</span><span class="sxs-lookup"><span data-stu-id="d7ac1-157">Proxy authentication</span></span>

<span data-ttu-id="d7ac1-158">Proxy authentication is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-158">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="d7ac1-159">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-159">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="d7ac1-160">Proxy ports</span><span class="sxs-lookup"><span data-stu-id="d7ac1-160">Proxy ports</span></span>

<span data-ttu-id="d7ac1-161">The connector makes outbound SSL-based connections by using the CONNECT method.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-161">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="d7ac1-162">This method essentially sets up a tunnel through the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-162">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="d7ac1-163">Configure the proxy server to allow tunneling to ports 443 and 80.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-163">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="d7ac1-164">When Service Bus runs over HTTPS, it uses port 443.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-164">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="d7ac1-165">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-165">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="d7ac1-166">SSL inspection</span><span class="sxs-lookup"><span data-stu-id="d7ac1-166">SSL inspection</span></span>
<span data-ttu-id="d7ac1-167">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-167">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span> <span data-ttu-id="d7ac1-168">The connector uses a certificate to authenticate to the Application Proxy service, and that certificate can be lost during SSL inspection.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-168">The connector uses a certificate to authenticate to the Application Proxy service, and that certificate can be lost during SSL inspection.</span></span> 

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="d7ac1-169">Troubleshoot connector proxy problems and service connectivity issues</span><span class="sxs-lookup"><span data-stu-id="d7ac1-169">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="d7ac1-170">Now you should see all traffic flowing through the proxy.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-170">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="d7ac1-171">If you have problems, the following troubleshooting information should help.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-171">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="d7ac1-172">The best way to identify and troubleshoot connector connectivity issues is to take a network capture while starting the connector service.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-172">The best way to identify and troubleshoot connector connectivity issues is to take a network capture while starting the connector service.</span></span> <span data-ttu-id="d7ac1-173">Here are some quick tips on capturing and filtering network traces.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-173">Here are some quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="d7ac1-174">You can use the monitoring tool of your choice.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-174">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="d7ac1-175">For the purposes of this article, we used Microsoft Message Analyzer.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-175">For the purposes of this article, we used Microsoft Message Analyzer.</span></span> <span data-ttu-id="d7ac1-176">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=44226).</span><span class="sxs-lookup"><span data-stu-id="d7ac1-176">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=44226).</span></span>

<span data-ttu-id="d7ac1-177">The following examples are specific to Message Analyzer, but the principles can be applied to any analysis tool.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-177">The following examples are specific to Message Analyzer, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="d7ac1-178">Take a capture of connector traffic</span><span class="sxs-lookup"><span data-stu-id="d7ac1-178">Take a capture of connector traffic</span></span>

<span data-ttu-id="d7ac1-179">For initial troubleshooting, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7ac1-179">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="d7ac1-180">From services.msc, stop the Azure AD Application Proxy Connector service.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-180">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>

   ![Azure AD Application Proxy Connector service in services.msc](./media/application-proxy-configure-connectors-with-proxy-servers/services-local.png)

2. <span data-ttu-id="d7ac1-182">Run Message Analyzer as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-182">Run Message Analyzer as an administrator.</span></span>
3. <span data-ttu-id="d7ac1-183">Select **Start local trace**.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-183">Select **Start local trace**.</span></span>

   ![Start network capture](./media/application-proxy-configure-connectors-with-proxy-servers/start-local-trace.png)

3. <span data-ttu-id="d7ac1-185">Start the Azure AD Application Proxy Connector service.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-185">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="d7ac1-186">Stop the network capture.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-186">Stop the network capture.</span></span>

   ![Stop network capture](./media/application-proxy-configure-connectors-with-proxy-servers/stop-trace.png)

### <a name="check-if-the-connector-traffic-bypasses-outbound-proxies"></a><span data-ttu-id="d7ac1-188">Check if the connector traffic bypasses outbound proxies</span><span class="sxs-lookup"><span data-stu-id="d7ac1-188">Check if the connector traffic bypasses outbound proxies</span></span>

<span data-ttu-id="d7ac1-189">If you configured your Application Proxy connector to bypass the proxy servers and connect directly to the Application Proxy service, you want to look in the network capture for failed TCP connection attempts.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-189">If you configured your Application Proxy connector to bypass the proxy servers and connect directly to the Application Proxy service, you want to look in the network capture for failed TCP connection attempts.</span></span> 

<span data-ttu-id="d7ac1-190">Use the Message Analyzer filter to identify these attempts.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-190">Use the Message Analyzer filter to identify these attempts.</span></span> <span data-ttu-id="d7ac1-191">Enter `property.TCPSynRetransmit` in the filter box and select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-191">Enter `property.TCPSynRetransmit` in the filter box and select **Apply**.</span></span> 

<span data-ttu-id="d7ac1-192">A SYN packet is the first packet sent to establish a TCP connection.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-192">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="d7ac1-193">If this packet doesn’t return a response, the SYN is reattempted.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-193">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="d7ac1-194">You can use the preceding filter to see any retransmitted SYNs.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-194">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="d7ac1-195">Then, you can check whether these SYNs correspond to any connector-related traffic.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-195">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="d7ac1-196">If you expect the connector to make direct connections to the Azure services, SynRetransmit responses on port 443 are an indication that you have a network or firewall problem.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-196">If you expect the connector to make direct connections to the Azure services, SynRetransmit responses on port 443 are an indication that you have a network or firewall problem.</span></span>

### <a name="check-if-the-connector-traffic-uses-outbound-proxies"></a><span data-ttu-id="d7ac1-197">Check if the connector traffic uses outbound proxies</span><span class="sxs-lookup"><span data-stu-id="d7ac1-197">Check if the connector traffic uses outbound proxies</span></span>

<span data-ttu-id="d7ac1-198">If you configured your Application Proxy connector traffic to go through the proxy servers, you want to look for failed https connections to your proxy.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-198">If you configured your Application Proxy connector traffic to go through the proxy servers, you want to look for failed https connections to your proxy.</span></span> 

<span data-ttu-id="d7ac1-199">To filter the network capture for these connection attempts, enter `(https.Request or https.Response) and tcp.port==8080` in the Message Analyzer filter, replacing 8080 with your proxy service port.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-199">To filter the network capture for these connection attempts, enter `(https.Request or https.Response) and tcp.port==8080` in the Message Analyzer filter, replacing 8080 with your proxy service port.</span></span> <span data-ttu-id="d7ac1-200">Select **Apply** to see the filter results.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-200">Select **Apply** to see the filter results.</span></span> 

<span data-ttu-id="d7ac1-201">The preceding filter shows just the HTTPs requests and responses to/from the proxy port.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-201">The preceding filter shows just the HTTPs requests and responses to/from the proxy port.</span></span> <span data-ttu-id="d7ac1-202">You're looking for the CONNECT requests that show communication with the proxy server.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-202">You're looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="d7ac1-203">Upon success, you get an HTTP OK (200) response.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-203">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="d7ac1-204">If you see other response codes, such as 407 or 502, that means that the proxy is requiring authentication or not allowing the traffic for some other reason.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-204">If you see other response codes, such as 407 or 502, that means that the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="d7ac1-205">At this point, you engage your proxy server support team.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-205">At this point, you engage your proxy server support team.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7ac1-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7ac1-206">Next steps</span></span>

- [<span data-ttu-id="d7ac1-207">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="d7ac1-207">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-connectors.md)

- <span data-ttu-id="d7ac1-208">If you have problems with connector connectivity issues, ask your question in the [Azure Active Directory forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD&forum=WindowsAzureAD) or create a ticket with our support team.</span><span class="sxs-lookup"><span data-stu-id="d7ac1-208">If you have problems with connector connectivity issues, ask your question in the [Azure Active Directory forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD&forum=WindowsAzureAD) or create a ticket with our support team.</span></span>
