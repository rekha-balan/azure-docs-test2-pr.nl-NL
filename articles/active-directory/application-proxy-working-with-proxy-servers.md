---
title: Work with existing on-premises proxy servers and Azure AD | Microsoft Docs
description: Covers how to work with existing on-premises proxy servers.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: kgremban
ms.openlocfilehash: 9ab4cf72db7a3995f7b547114899ba264a832eea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550104"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="d5159-103">Work with existing on-premises proxy servers</span><span class="sxs-lookup"><span data-stu-id="d5159-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="d5159-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy Connector to work with outbound proxy servers.</span><span class="sxs-lookup"><span data-stu-id="d5159-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy Connector to work with outbound proxy servers.</span></span> <span data-ttu-id="d5159-105">It is intended for customers with network environments that have existing proxies.</span><span class="sxs-lookup"><span data-stu-id="d5159-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="d5159-106">We start by looking at these main deployment scenarios:</span><span class="sxs-lookup"><span data-stu-id="d5159-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="d5159-107">Configure connectors to bypass your on-premises outbound proxies.</span><span class="sxs-lookup"><span data-stu-id="d5159-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="d5159-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="d5159-109">For more information about how connectors work, see [How to provide secure remote access to on-premises applications](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).</span><span class="sxs-lookup"><span data-stu-id="d5159-109">For more information about how connectors work, see [How to provide secure remote access to on-premises applications](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).</span></span>

## <a name="configure-your-connectors"></a><span data-ttu-id="d5159-110">Configure your connectors</span><span class="sxs-lookup"><span data-stu-id="d5159-110">Configure your connectors</span></span>

<span data-ttu-id="d5159-111">The core connector service uses Azure Service Bus to handle some of the underlying communications to the Azure AD Application Proxy service.</span><span class="sxs-lookup"><span data-stu-id="d5159-111">The core connector service uses Azure Service Bus to handle some of the underlying communications to the Azure AD Application Proxy service.</span></span> <span data-ttu-id="d5159-112">Service Bus brings with it additional configuration requirements.</span><span class="sxs-lookup"><span data-stu-id="d5159-112">Service Bus brings with it additional configuration requirements.</span></span>

<span data-ttu-id="d5159-113">For information about resolving Azure AD connectivity problems, see [How to troubleshoot Azure AD Application Proxy connectivity problems](https://blogs.technet.microsoft.com/applicationproxyblog/2015/03/24/how-to-troubleshoot-azure-ad-application-proxy-connectivity-problems).</span><span class="sxs-lookup"><span data-stu-id="d5159-113">For information about resolving Azure AD connectivity problems, see [How to troubleshoot Azure AD Application Proxy connectivity problems](https://blogs.technet.microsoft.com/applicationproxyblog/2015/03/24/how-to-troubleshoot-azure-ad-application-proxy-connectivity-problems).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="d5159-114">Configure the outbound proxy</span><span class="sxs-lookup"><span data-stu-id="d5159-114">Configure the outbound proxy</span></span>

<span data-ttu-id="d5159-115">If you have an outbound proxy in your environment, ensure that the account that's doing the installation is appropriately configured to use the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-115">If you have an outbound proxy in your environment, ensure that the account that's doing the installation is appropriately configured to use the outbound proxy.</span></span> <span data-ttu-id="d5159-116">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span><span class="sxs-lookup"><span data-stu-id="d5159-116">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="d5159-117">To configure the proxy settings by using Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="d5159-117">To configure the proxy settings by using Microsoft Edge:</span></span>

1. <span data-ttu-id="d5159-118">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span><span class="sxs-lookup"><span data-stu-id="d5159-118">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="d5159-119">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span><span class="sxs-lookup"><span data-stu-id="d5159-119">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="d5159-120">Fill in the necessary proxy settings.</span><span class="sxs-lookup"><span data-stu-id="d5159-120">Fill in the necessary proxy settings.</span></span>

   ![Dialog box for proxy settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="d5159-122">Bypass outbound proxies</span><span class="sxs-lookup"><span data-stu-id="d5159-122">Bypass outbound proxies</span></span>

<span data-ttu-id="d5159-123">By default, the underlying OS components that the connector uses for making outbound requests automatically attempt to locate a proxy server on the network.</span><span class="sxs-lookup"><span data-stu-id="d5159-123">By default, the underlying OS components that the connector uses for making outbound requests automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="d5159-124">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span><span class="sxs-lookup"><span data-stu-id="d5159-124">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="d5159-125">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="d5159-125">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="d5159-126">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="d5159-126">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="d5159-127">This request becomes the proxy configuration script in your environment.</span><span class="sxs-lookup"><span data-stu-id="d5159-127">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="d5159-128">The connector uses this script to select an outbound proxy server.</span><span class="sxs-lookup"><span data-stu-id="d5159-128">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="d5159-129">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-129">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="d5159-130">In the next section, we cover the configuration steps needed on the outbound proxy to make the traffic flow through it.</span><span class="sxs-lookup"><span data-stu-id="d5159-130">In the next section, we cover the configuration steps needed on the outbound proxy to make the traffic flow through it.</span></span> <span data-ttu-id="d5159-131">But first, let’s address how you can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span><span class="sxs-lookup"><span data-stu-id="d5159-131">But first, let’s address how you can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="d5159-132">This is what we recommend (if your network policy allows for it), because it means that you have one less configuration to maintain.</span><span class="sxs-lookup"><span data-stu-id="d5159-132">This is what we recommend (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="d5159-133">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the [system.net] section shown in this code sample:</span><span class="sxs-lookup"><span data-stu-id="d5159-133">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the [system.net] section shown in this code sample:</span></span>

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
<span data-ttu-id="d5159-134">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="d5159-134">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="d5159-135">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span><span class="sxs-lookup"><span data-stu-id="d5159-135">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="d5159-136">Use the outbound proxy server</span><span class="sxs-lookup"><span data-stu-id="d5159-136">Use the outbound proxy server</span></span>

<span data-ttu-id="d5159-137">As mentioned earlier, some customer environments require all outbound traffic to go through an outbound proxy, without exception.</span><span class="sxs-lookup"><span data-stu-id="d5159-137">As mentioned earlier, some customer environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="d5159-138">As a result, bypassing the proxy is not an option.</span><span class="sxs-lookup"><span data-stu-id="d5159-138">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="d5159-139">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="d5159-139">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram.</span></span>

 ![Configuring connector traffic to go through an outbound proxy to Azure AD Application Proxy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="d5159-141">As a result of having only outbound traffic, there's no need to set up load balancing between the connectors or configure inbound access through your firewalls.</span><span class="sxs-lookup"><span data-stu-id="d5159-141">As a result of having only outbound traffic, there's no need to set up load balancing between the connectors or configure inbound access through your firewalls.</span></span>

<span data-ttu-id="d5159-142">In any case, you need to perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d5159-142">In any case, you need to perform the following steps:</span></span>
1. <span data-ttu-id="d5159-143">Configure the Connector Updater service to go through the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-143">Configure the Connector Updater service to go through the outbound proxy.</span></span>
2. <span data-ttu-id="d5159-144">Configure the proxy settings to permit connections to the Azure AD Application Proxy service.</span><span class="sxs-lookup"><span data-stu-id="d5159-144">Configure the proxy settings to permit connections to the Azure AD Application Proxy service.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="d5159-145">Step 1: Configure the connector and related services to go through the outbound proxy</span><span class="sxs-lookup"><span data-stu-id="d5159-145">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="d5159-146">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span><span class="sxs-lookup"><span data-stu-id="d5159-146">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="d5159-147">However, you can explicitly configure the connector to go through an outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-147">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="d5159-148">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the [system.net] section shown in this code sample:</span><span class="sxs-lookup"><span data-stu-id="d5159-148">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the [system.net] section shown in this code sample:</span></span>

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

>[!NOTE]
><span data-ttu-id="d5159-149">Change _proxyserver:8080_ to reflect your local proxy server name or IP address and the port that it's listening on.</span><span class="sxs-lookup"><span data-stu-id="d5159-149">Change _proxyserver:8080_ to reflect your local proxy server name or IP address and the port that it's listening on.</span></span>
>

<span data-ttu-id="d5159-150">Then configure the Connector Updater service to use the proxy, by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="d5159-150">Then configure the Connector Updater service to use the proxy, by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="d5159-151">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span><span class="sxs-lookup"><span data-stu-id="d5159-151">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="d5159-152">There are four aspects to consider at the outbound proxy:</span><span class="sxs-lookup"><span data-stu-id="d5159-152">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="d5159-153">Proxy outbound rules</span><span class="sxs-lookup"><span data-stu-id="d5159-153">Proxy outbound rules</span></span>
* <span data-ttu-id="d5159-154">Proxy authentication</span><span class="sxs-lookup"><span data-stu-id="d5159-154">Proxy authentication</span></span>
* <span data-ttu-id="d5159-155">Proxy ports</span><span class="sxs-lookup"><span data-stu-id="d5159-155">Proxy ports</span></span>
* <span data-ttu-id="d5159-156">SSL inspection</span><span class="sxs-lookup"><span data-stu-id="d5159-156">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="d5159-157">Proxy outbound rules</span><span class="sxs-lookup"><span data-stu-id="d5159-157">Proxy outbound rules</span></span>
<span data-ttu-id="d5159-158">Allow access to the following endpoints for connector service access:</span><span class="sxs-lookup"><span data-stu-id="d5159-158">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="d5159-159">\*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="d5159-159">\*.msappproxy.net</span></span>
* <span data-ttu-id="d5159-160">\*.servicebus.microsoft.net</span><span class="sxs-lookup"><span data-stu-id="d5159-160">\*.servicebus.microsoft.net</span></span>

<span data-ttu-id="d5159-161">For initial registration, allow access to the following endpoints:</span><span class="sxs-lookup"><span data-stu-id="d5159-161">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="d5159-162">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5159-162">login.windows.net</span></span>
* <span data-ttu-id="d5159-163">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5159-163">login.microsoftonline.com</span></span>

<span data-ttu-id="d5159-164">The underlying Service Bus control channels that the connector service uses also require connectivity to specific IP addresses.</span><span class="sxs-lookup"><span data-stu-id="d5159-164">The underlying Service Bus control channels that the connector service uses also require connectivity to specific IP addresses.</span></span> <span data-ttu-id="d5159-165">Until Service Bus moves to an FQDN instead, there are two options:</span><span class="sxs-lookup"><span data-stu-id="d5159-165">Until Service Bus moves to an FQDN instead, there are two options:</span></span>

* <span data-ttu-id="d5159-166">Allow the connector outbound access to all destinations.</span><span class="sxs-lookup"><span data-stu-id="d5159-166">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="d5159-167">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d5159-167">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span>

>[!NOTE]
><span data-ttu-id="d5159-168">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span><span class="sxs-lookup"><span data-stu-id="d5159-168">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="d5159-169">You will need to put a process in place to ensure that your access rules are updated accordingly.</span><span class="sxs-lookup"><span data-stu-id="d5159-169">You will need to put a process in place to ensure that your access rules are updated accordingly.</span></span>
>

#### <a name="proxy-authentication"></a><span data-ttu-id="d5159-170">Proxy authentication</span><span class="sxs-lookup"><span data-stu-id="d5159-170">Proxy authentication</span></span>

<span data-ttu-id="d5159-171">Proxy authentication is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="d5159-171">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="d5159-172">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span><span class="sxs-lookup"><span data-stu-id="d5159-172">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="d5159-173">Proxy ports</span><span class="sxs-lookup"><span data-stu-id="d5159-173">Proxy ports</span></span>

<span data-ttu-id="d5159-174">The connector makes outbound SSL-based connections by using the CONNECT method.</span><span class="sxs-lookup"><span data-stu-id="d5159-174">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="d5159-175">This method essentially sets up a tunnel through the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-175">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="d5159-176">Some proxy servers, by default, allow outbound tunneling to only standard SSL ports such as 443.</span><span class="sxs-lookup"><span data-stu-id="d5159-176">Some proxy servers, by default, allow outbound tunneling to only standard SSL ports such as 443.</span></span> <span data-ttu-id="d5159-177">If this is the case, the proxy server must be configured to allow tunneling to additional ports.</span><span class="sxs-lookup"><span data-stu-id="d5159-177">If this is the case, the proxy server must be configured to allow tunneling to additional ports.</span></span>

<span data-ttu-id="d5159-178">Configure the proxy server to allow tunneling to nonstandard SSL ports 8080, 9090, 9091, and 10100-10120.</span><span class="sxs-lookup"><span data-stu-id="d5159-178">Configure the proxy server to allow tunneling to nonstandard SSL ports 8080, 9090, 9091, and 10100-10120.</span></span>

>[!NOTE]
><span data-ttu-id="d5159-179">When Service Bus runs over HTTPS, it uses port 443.</span><span class="sxs-lookup"><span data-stu-id="d5159-179">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="d5159-180">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span><span class="sxs-lookup"><span data-stu-id="d5159-180">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>
>

<span data-ttu-id="d5159-181">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span><span class="sxs-lookup"><span data-stu-id="d5159-181">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="d5159-182">SSL inspection</span><span class="sxs-lookup"><span data-stu-id="d5159-182">SSL inspection</span></span>
<span data-ttu-id="d5159-183">Do not use SSL inspection for the connector traffic, because it will cause problems for the connector traffic.</span><span class="sxs-lookup"><span data-stu-id="d5159-183">Do not use SSL inspection for the connector traffic, because it will cause problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="d5159-184">Troubleshoot connector proxy problems and service connectivity issues</span><span class="sxs-lookup"><span data-stu-id="d5159-184">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="d5159-185">Now you should see all traffic flowing through the proxy.</span><span class="sxs-lookup"><span data-stu-id="d5159-185">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="d5159-186">If you have problems, the following troubleshooting information should help.</span><span class="sxs-lookup"><span data-stu-id="d5159-186">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="d5159-187">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span><span class="sxs-lookup"><span data-stu-id="d5159-187">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="d5159-188">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span><span class="sxs-lookup"><span data-stu-id="d5159-188">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="d5159-189">You can use the monitoring tool of your choice.</span><span class="sxs-lookup"><span data-stu-id="d5159-189">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="d5159-190">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="d5159-190">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="d5159-191">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="d5159-191">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="d5159-192">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span><span class="sxs-lookup"><span data-stu-id="d5159-192">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="d5159-193">Take a capture by using Network Monitor</span><span class="sxs-lookup"><span data-stu-id="d5159-193">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="d5159-194">To start a capture:</span><span class="sxs-lookup"><span data-stu-id="d5159-194">To start a capture:</span></span>

1. <span data-ttu-id="d5159-195">Open Network Monitor and click **New Capture**.</span><span class="sxs-lookup"><span data-stu-id="d5159-195">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="d5159-196">Click the **Start** button.</span><span class="sxs-lookup"><span data-stu-id="d5159-196">Click the **Start** button.</span></span>

   ![Network Monitor window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="d5159-198">After you complete a capture, click the **Stop** button to end it.</span><span class="sxs-lookup"><span data-stu-id="d5159-198">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="d5159-199">Take a capture of connector traffic</span><span class="sxs-lookup"><span data-stu-id="d5159-199">Take a capture of connector traffic</span></span>

<span data-ttu-id="d5159-200">For initial troubleshooting, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d5159-200">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="d5159-201">From services.msc, stop the Azure AD Application Proxy Connector service.</span><span class="sxs-lookup"><span data-stu-id="d5159-201">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="d5159-202">Start the network capture.</span><span class="sxs-lookup"><span data-stu-id="d5159-202">Start the network capture.</span></span>
3. <span data-ttu-id="d5159-203">Start the Azure AD Application Proxy Connector service.</span><span class="sxs-lookup"><span data-stu-id="d5159-203">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="d5159-204">Stop the network capture.</span><span class="sxs-lookup"><span data-stu-id="d5159-204">Stop the network capture.</span></span>

   ![Azure AD Application Proxy Connector service in services.msc](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="d5159-206">Look at the requests from the connector to the proxy server</span><span class="sxs-lookup"><span data-stu-id="d5159-206">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="d5159-207">Now that you’ve got a network capture, you're ready to filter it.</span><span class="sxs-lookup"><span data-stu-id="d5159-207">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="d5159-208">The key to looking at the trace is understanding how to filter the capture.</span><span class="sxs-lookup"><span data-stu-id="d5159-208">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="d5159-209">One filter is as follows (where 8080 is the proxy service port):</span><span class="sxs-lookup"><span data-stu-id="d5159-209">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="d5159-210">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="d5159-210">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="d5159-211">If you enter this filter in the **Display Filter** window and select **Apply**, it will filter the captured traffic based on the filter.</span><span class="sxs-lookup"><span data-stu-id="d5159-211">If you enter this filter in the **Display Filter** window and select **Apply**, it will filter the captured traffic based on the filter.</span></span>

<span data-ttu-id="d5159-212">The preceding filter will show just the HTTP requests and responses to/from the proxy port.</span><span class="sxs-lookup"><span data-stu-id="d5159-212">The preceding filter will show just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="d5159-213">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span><span class="sxs-lookup"><span data-stu-id="d5159-213">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Example list of filtered HTTP requests and responses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="d5159-215">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span><span class="sxs-lookup"><span data-stu-id="d5159-215">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="d5159-216">Upon success, you'll get an HTTP OK (200) response.</span><span class="sxs-lookup"><span data-stu-id="d5159-216">Upon success, you'll get an HTTP OK (200) response.</span></span>

<span data-ttu-id="d5159-217">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span><span class="sxs-lookup"><span data-stu-id="d5159-217">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="d5159-218">At this point, you engage your proxy server support team.</span><span class="sxs-lookup"><span data-stu-id="d5159-218">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="d5159-219">Identify failed TCP connection attempts</span><span class="sxs-lookup"><span data-stu-id="d5159-219">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="d5159-220">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span><span class="sxs-lookup"><span data-stu-id="d5159-220">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="d5159-221">Another Network Monitor filter that helps you to easily identify this problem is:</span><span class="sxs-lookup"><span data-stu-id="d5159-221">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="d5159-222">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="d5159-222">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="d5159-223">A SYN packet is the first packet sent to establish a TCP connection.</span><span class="sxs-lookup"><span data-stu-id="d5159-223">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="d5159-224">If this packet doesn’t return a response, the SYN is reattempted.</span><span class="sxs-lookup"><span data-stu-id="d5159-224">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="d5159-225">You can use the preceding filter to see any retransmitted SYNs.</span><span class="sxs-lookup"><span data-stu-id="d5159-225">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="d5159-226">Then, you can check whether these SYNs correspond to any connector-related traffic.</span><span class="sxs-lookup"><span data-stu-id="d5159-226">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="d5159-227">The following example shows a failed connection attempt to Service Bus port 9352:</span><span class="sxs-lookup"><span data-stu-id="d5159-227">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Example response for a failed connection attempt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="d5159-229">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span><span class="sxs-lookup"><span data-stu-id="d5159-229">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="d5159-230">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span><span class="sxs-lookup"><span data-stu-id="d5159-230">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="d5159-231">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d5159-231">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="d5159-232">Network trace analysis is not for everyone.</span><span class="sxs-lookup"><span data-stu-id="d5159-232">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="d5159-233">But it can be a valuable tool to get quick information about what's going on with your network.</span><span class="sxs-lookup"><span data-stu-id="d5159-233">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="d5159-234">If you continue to struggle with connector connectivity issues, please create a ticket with our support team.</span><span class="sxs-lookup"><span data-stu-id="d5159-234">If you continue to struggle with connector connectivity issues, please create a ticket with our support team.</span></span> <span data-ttu-id="d5159-235">The team can assist you with further troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="d5159-235">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="d5159-236">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="d5159-236">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5159-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5159-237">Next steps</span></span>

[<span data-ttu-id="d5159-238">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="d5159-238">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br>
[<span data-ttu-id="d5159-239">How to silently install the Azure AD Application Proxy Connector </span><span class="sxs-lookup"><span data-stu-id="d5159-239">How to silently install the Azure AD Application Proxy Connector </span></span>](active-directory-application-proxy-silent-installation.md)






