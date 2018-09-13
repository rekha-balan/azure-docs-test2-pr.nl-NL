---
title: Azure Stack datacenter integration - DNS
description: Learn how to integrate Azure Stack DNS with your datacenter DNS
services: azure-stack
author: jeffgilb
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 02/28/2018
ms.author: jeffgilb
ms.reviewer: wfayed
keywords: ''
ms.openlocfilehash: b4935dc95ccf525c0a40b10dcc8c59ec8aba710e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969479"
---
# <a name="azure-stack-datacenter-integration---dns"></a><span data-ttu-id="a89fb-103">Azure Stack datacenter integration - DNS</span><span class="sxs-lookup"><span data-stu-id="a89fb-103">Azure Stack datacenter integration - DNS</span></span>
<span data-ttu-id="a89fb-104">To be able to access Azure Stack endpoints (`portal`, `adminportal`, `management`, `adminmanagement`, etc.)  from outside Azure Stack, you need to integrate the Azure Stack DNS services with the DNS servers that host the DNS zones you want to use in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a89fb-104">To be able to access Azure Stack endpoints (`portal`, `adminportal`, `management`, `adminmanagement`, etc.)  from outside Azure Stack, you need to integrate the Azure Stack DNS services with the DNS servers that host the DNS zones you want to use in Azure Stack.</span></span>

## <a name="azure-stack-dns-namespace"></a><span data-ttu-id="a89fb-105">Azure Stack DNS namespace</span><span class="sxs-lookup"><span data-stu-id="a89fb-105">Azure Stack DNS namespace</span></span>
<span data-ttu-id="a89fb-106">You are required to provide some important information related to DNS when you deploy Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a89fb-106">You are required to provide some important information related to DNS when you deploy Azure Stack.</span></span>


|<span data-ttu-id="a89fb-107">Field</span><span class="sxs-lookup"><span data-stu-id="a89fb-107">Field</span></span>  |<span data-ttu-id="a89fb-108">Description</span><span class="sxs-lookup"><span data-stu-id="a89fb-108">Description</span></span>  |<span data-ttu-id="a89fb-109">Example</span><span class="sxs-lookup"><span data-stu-id="a89fb-109">Example</span></span>|
|---------|---------|---------|
|<span data-ttu-id="a89fb-110">Region</span><span class="sxs-lookup"><span data-stu-id="a89fb-110">Region</span></span>|<span data-ttu-id="a89fb-111">The geographic location of your Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="a89fb-111">The geographic location of your Azure Stack deployment.</span></span>|`east`|
|<span data-ttu-id="a89fb-112">External Domain Name</span><span class="sxs-lookup"><span data-stu-id="a89fb-112">External Domain Name</span></span>|<span data-ttu-id="a89fb-113">The name of the zone you want to use for your Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="a89fb-113">The name of the zone you want to use for your Azure Stack deployment.</span></span>|`cloud.fabrikam.com`|
|<span data-ttu-id="a89fb-114">Internal Domain Name</span><span class="sxs-lookup"><span data-stu-id="a89fb-114">Internal Domain Name</span></span>|<span data-ttu-id="a89fb-115">The name of the internal zone that is used for infrastructure services in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a89fb-115">The name of the internal zone that is used for infrastructure services in Azure Stack.</span></span>  <span data-ttu-id="a89fb-116">It is Directory Service-integrated and private (not reachable from outside the Azure Stack deployment).</span><span class="sxs-lookup"><span data-stu-id="a89fb-116">It is Directory Service-integrated and private (not reachable from outside the Azure Stack deployment).</span></span>|`azurestack.local`|
|<span data-ttu-id="a89fb-117">DNS Forwarder</span><span class="sxs-lookup"><span data-stu-id="a89fb-117">DNS Forwarder</span></span>|<span data-ttu-id="a89fb-118">DNS servers that are used to forward DNS queries, DNS zones and records that are hosted outside Azure Stack, either on the corporate intranet or public internet.</span><span class="sxs-lookup"><span data-stu-id="a89fb-118">DNS servers that are used to forward DNS queries, DNS zones and records that are hosted outside Azure Stack, either on the corporate intranet or public internet.</span></span>|`10.57.175.34`<br>`8.8.8.8`|
|<span data-ttu-id="a89fb-119">Naming Prefix (Optional)</span><span class="sxs-lookup"><span data-stu-id="a89fb-119">Naming Prefix (Optional)</span></span>|<span data-ttu-id="a89fb-120">The naming prefix you want your Azure Stack infrastructure role instance machine names to have.</span><span class="sxs-lookup"><span data-stu-id="a89fb-120">The naming prefix you want your Azure Stack infrastructure role instance machine names to have.</span></span>  <span data-ttu-id="a89fb-121">If not provided, the default is `azs`.</span><span class="sxs-lookup"><span data-stu-id="a89fb-121">If not provided, the default is `azs`.</span></span>|`azs`|

<span data-ttu-id="a89fb-122">The fully qualified domain name (FQDN) of your Azure Stack deployment and endpoints is the combination of the Region parameter and the External Domain Name parameter.</span><span class="sxs-lookup"><span data-stu-id="a89fb-122">The fully qualified domain name (FQDN) of your Azure Stack deployment and endpoints is the combination of the Region parameter and the External Domain Name parameter.</span></span> <span data-ttu-id="a89fb-123">Using the values from the examples in the previous table, the FQDN for this Azure Stack deployment would be the following name:</span><span class="sxs-lookup"><span data-stu-id="a89fb-123">Using the values from the examples in the previous table, the FQDN for this Azure Stack deployment would be the following name:</span></span>

`east.cloud.fabrikam.com`

<span data-ttu-id="a89fb-124">As such, examples of some of the endpoints for this deployment would look like the following URLs:</span><span class="sxs-lookup"><span data-stu-id="a89fb-124">As such, examples of some of the endpoints for this deployment would look like the following URLs:</span></span>

`https://portal.east.cloud.fabrikam.com`

`https://adminportal.east.cloud.fabrikam.com`

<span data-ttu-id="a89fb-125">To use this example DNS namespace for an Azure Stack deployment, the following conditions are required:</span><span class="sxs-lookup"><span data-stu-id="a89fb-125">To use this example DNS namespace for an Azure Stack deployment, the following conditions are required:</span></span>

- <span data-ttu-id="a89fb-126">The zone `fabrikam.com` is registered either with a domain registrar, an internal corporate DNS server, or both, depending on your name resolution requirements.</span><span class="sxs-lookup"><span data-stu-id="a89fb-126">The zone `fabrikam.com` is registered either with a domain registrar, an internal corporate DNS server, or both, depending on your name resolution requirements.</span></span>
- <span data-ttu-id="a89fb-127">The child domain `cloud.fabrikam.com` exists under the zone `fabrikam.com`.</span><span class="sxs-lookup"><span data-stu-id="a89fb-127">The child domain `cloud.fabrikam.com` exists under the zone `fabrikam.com`.</span></span>
- <span data-ttu-id="a89fb-128">The DNS servers that host the zones `fabrikam.com` and `cloud.fabrikam.com` can be reached from the Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="a89fb-128">The DNS servers that host the zones `fabrikam.com` and `cloud.fabrikam.com` can be reached from the Azure Stack deployment.</span></span>

<span data-ttu-id="a89fb-129">To be able to resolve DNS names for Azure Stack endpoints and instances from outside Azure Stack, you need to integrate the DNS servers that host the external DNS zone for Azure Stack with the DNS servers that host the parent zone you want to use.</span><span class="sxs-lookup"><span data-stu-id="a89fb-129">To be able to resolve DNS names for Azure Stack endpoints and instances from outside Azure Stack, you need to integrate the DNS servers that host the external DNS zone for Azure Stack with the DNS servers that host the parent zone you want to use.</span></span>


## <a name="resolution-and-delegation"></a><span data-ttu-id="a89fb-130">Resolution and delegation</span><span class="sxs-lookup"><span data-stu-id="a89fb-130">Resolution and delegation</span></span>

<span data-ttu-id="a89fb-131">There are two types of DNS servers:</span><span class="sxs-lookup"><span data-stu-id="a89fb-131">There are two types of DNS servers:</span></span>

- <span data-ttu-id="a89fb-132">An authoritative DNS server hosts DNS zones.</span><span class="sxs-lookup"><span data-stu-id="a89fb-132">An authoritative DNS server hosts DNS zones.</span></span> <span data-ttu-id="a89fb-133">It answers DNS queries for records in those zones only.</span><span class="sxs-lookup"><span data-stu-id="a89fb-133">It answers DNS queries for records in those zones only.</span></span>
- <span data-ttu-id="a89fb-134">A recursive DNS server does not host DNS zones.</span><span class="sxs-lookup"><span data-stu-id="a89fb-134">A recursive DNS server does not host DNS zones.</span></span> <span data-ttu-id="a89fb-135">It answers all DNS queries by calling authoritative DNS servers to gather the data it needs.</span><span class="sxs-lookup"><span data-stu-id="a89fb-135">It answers all DNS queries by calling authoritative DNS servers to gather the data it needs.</span></span>

<span data-ttu-id="a89fb-136">Azure Stack includes both authoritative and recursive DNS servers.</span><span class="sxs-lookup"><span data-stu-id="a89fb-136">Azure Stack includes both authoritative and recursive DNS servers.</span></span> <span data-ttu-id="a89fb-137">The recursive servers are used to resolve names of everything except for the internal private zone and the external public DNS zone for that Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="a89fb-137">The recursive servers are used to resolve names of everything except for the internal private zone and the external public DNS zone for that Azure Stack deployment.</span></span> 

![Azure Stack DNS architecture](media/azure-stack-integrate-dns/Integrate-DNS-01.png)

## <a name="resolving-external-dns-names-from-azure-stack"></a><span data-ttu-id="a89fb-139">Resolving external DNS names from Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a89fb-139">Resolving external DNS names from Azure Stack</span></span>

<span data-ttu-id="a89fb-140">To resolve DNS names for endpoints outside Azure Stack (for example: www.bing.com), you need to provide DNS servers that Azure Stack can use to forward DNS requests for which Azure Stack is not authoritative.</span><span class="sxs-lookup"><span data-stu-id="a89fb-140">To resolve DNS names for endpoints outside Azure Stack (for example: www.bing.com), you need to provide DNS servers that Azure Stack can use to forward DNS requests for which Azure Stack is not authoritative.</span></span> <span data-ttu-id="a89fb-141">For deployment, DNS servers that Azure Stack forwards requests to are required in the Deployment Worksheet (in the DNS Forwarder field).</span><span class="sxs-lookup"><span data-stu-id="a89fb-141">For deployment, DNS servers that Azure Stack forwards requests to are required in the Deployment Worksheet (in the DNS Forwarder field).</span></span> <span data-ttu-id="a89fb-142">Provide at least two servers in this field for fault tolerance.</span><span class="sxs-lookup"><span data-stu-id="a89fb-142">Provide at least two servers in this field for fault tolerance.</span></span> <span data-ttu-id="a89fb-143">Without these values, Azure Stack deployment fails.</span><span class="sxs-lookup"><span data-stu-id="a89fb-143">Without these values, Azure Stack deployment fails.</span></span>

### <a name="configure-conditional-dns-forwarding"></a><span data-ttu-id="a89fb-144">Configure conditional DNS forwarding</span><span class="sxs-lookup"><span data-stu-id="a89fb-144">Configure conditional DNS forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a89fb-145">This only applies to an AD FS deployment.</span><span class="sxs-lookup"><span data-stu-id="a89fb-145">This only applies to an AD FS deployment.</span></span>

<span data-ttu-id="a89fb-146">To enable name resolution with your existing DNS infrastructure, configure conditional forwarding.</span><span class="sxs-lookup"><span data-stu-id="a89fb-146">To enable name resolution with your existing DNS infrastructure, configure conditional forwarding.</span></span>

<span data-ttu-id="a89fb-147">To add a conditional forwarder, you must use the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="a89fb-147">To add a conditional forwarder, you must use the privileged endpoint.</span></span>

<span data-ttu-id="a89fb-148">For this procedure, use a computer in your datacenter network that can communicate with the privileged endpoint in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a89fb-148">For this procedure, use a computer in your datacenter network that can communicate with the privileged endpoint in Azure Stack.</span></span>

1. <span data-ttu-id="a89fb-149">Open an elevated Windows PowerShell session (run as administrator), and connect to the IP address of the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="a89fb-149">Open an elevated Windows PowerShell session (run as administrator), and connect to the IP address of the privileged endpoint.</span></span> <span data-ttu-id="a89fb-150">Use the credentials for CloudAdmin authentication.</span><span class="sxs-lookup"><span data-stu-id="a89fb-150">Use the credentials for CloudAdmin authentication.</span></span>

   ```
   $cred=Get-Credential 
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $cred
   ```

2. <span data-ttu-id="a89fb-151">After you connect to the privileged endpoint, run the following PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="a89fb-151">After you connect to the privileged endpoint, run the following PowerShell command.</span></span> <span data-ttu-id="a89fb-152">Substitute the sample values provided with your domain name and IP addresses of the DNS servers you want to use.</span><span class="sxs-lookup"><span data-stu-id="a89fb-152">Substitute the sample values provided with your domain name and IP addresses of the DNS servers you want to use.</span></span>

   ```
   Register-CustomDnsServer -CustomDomainName "contoso.com" -CustomDnsIPAddresses "192.168.1.1","192.168.1.2"
   ```

## <a name="resolving-azure-stack-dns-names-from-outside-azure-stack"></a><span data-ttu-id="a89fb-153">Resolving Azure Stack DNS names from outside Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a89fb-153">Resolving Azure Stack DNS names from outside Azure Stack</span></span>
<span data-ttu-id="a89fb-154">The authoritative servers are the ones that hold the external DNS zone information, and any user-created zones.</span><span class="sxs-lookup"><span data-stu-id="a89fb-154">The authoritative servers are the ones that hold the external DNS zone information, and any user-created zones.</span></span> <span data-ttu-id="a89fb-155">Integrate with these servers to enable zone delegation or conditional forwarding to resolve Azure Stack DNS names from outside Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a89fb-155">Integrate with these servers to enable zone delegation or conditional forwarding to resolve Azure Stack DNS names from outside Azure Stack.</span></span>

## <a name="get-dns-server-external-endpoint-information"></a><span data-ttu-id="a89fb-156">Get DNS Server external endpoint information</span><span class="sxs-lookup"><span data-stu-id="a89fb-156">Get DNS Server external endpoint information</span></span>

<span data-ttu-id="a89fb-157">To integrate your Azure Stack deployment with your DNS infrastructure, you need the following information:</span><span class="sxs-lookup"><span data-stu-id="a89fb-157">To integrate your Azure Stack deployment with your DNS infrastructure, you need the following information:</span></span>

- <span data-ttu-id="a89fb-158">DNS server FQDNs</span><span class="sxs-lookup"><span data-stu-id="a89fb-158">DNS server FQDNs</span></span>
- <span data-ttu-id="a89fb-159">DNS server IP addresses</span><span class="sxs-lookup"><span data-stu-id="a89fb-159">DNS server IP addresses</span></span>

<span data-ttu-id="a89fb-160">The FQDNs for the Azure Stack DNS servers have the following format:</span><span class="sxs-lookup"><span data-stu-id="a89fb-160">The FQDNs for the Azure Stack DNS servers have the following format:</span></span>

`<NAMINGPREFIX>-ns01.<REGION>.<EXTERNALDOMAINNAME>`

`<NAMINGPREFIX>-ns02.<REGION>.<EXTERNALDOMAINNAME>`

<span data-ttu-id="a89fb-161">Using the sample values, the FQDNs for the DNS servers are:</span><span class="sxs-lookup"><span data-stu-id="a89fb-161">Using the sample values, the FQDNs for the DNS servers are:</span></span>

`azs-ns01.east.cloud.fabrikam.com`

`azs-ns02.east.cloud.fabrikam.com`


<span data-ttu-id="a89fb-162">This information is also created at the end of all Azure Stack deployments in a file named `AzureStackStampDeploymentInfo.json`.</span><span class="sxs-lookup"><span data-stu-id="a89fb-162">This information is also created at the end of all Azure Stack deployments in a file named `AzureStackStampDeploymentInfo.json`.</span></span> <span data-ttu-id="a89fb-163">This file is located in the `C:\CloudDeployment\logs` folder of the Deployment virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a89fb-163">This file is located in the `C:\CloudDeployment\logs` folder of the Deployment virtual machine.</span></span> <span data-ttu-id="a89fb-164">If you’re not sure what values were used for your Azure Stack deployment, you can get the values from here.</span><span class="sxs-lookup"><span data-stu-id="a89fb-164">If you’re not sure what values were used for your Azure Stack deployment, you can get the values from here.</span></span>

<span data-ttu-id="a89fb-165">If the Deployment virtual machine is no longer available or is inaccessible, you can obtain the values by connecting to the privileged endpoint and running the `Get-AzureStackInfo` PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a89fb-165">If the Deployment virtual machine is no longer available or is inaccessible, you can obtain the values by connecting to the privileged endpoint and running the `Get-AzureStackInfo` PowerShell cmdlet.</span></span> <span data-ttu-id="a89fb-166">For more information, see [privileged endpoint](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a89fb-166">For more information, see [privileged endpoint](azure-stack-privileged-endpoint.md).</span></span>

## <a name="setting-up-conditional-forwarding-to-azure-stack"></a><span data-ttu-id="a89fb-167">Setting up conditional forwarding to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a89fb-167">Setting up conditional forwarding to Azure Stack</span></span>

<span data-ttu-id="a89fb-168">The simplest and most secure way to integrate Azure Stack with your DNS infrastructure is to do conditional forwarding of the zone from the server that hosts the parent zone.</span><span class="sxs-lookup"><span data-stu-id="a89fb-168">The simplest and most secure way to integrate Azure Stack with your DNS infrastructure is to do conditional forwarding of the zone from the server that hosts the parent zone.</span></span> <span data-ttu-id="a89fb-169">This approach is recommended if you have direct control over the DNS servers that host the parent zone for your Azure Stack external DNS namespace.</span><span class="sxs-lookup"><span data-stu-id="a89fb-169">This approach is recommended if you have direct control over the DNS servers that host the parent zone for your Azure Stack external DNS namespace.</span></span>

<span data-ttu-id="a89fb-170">If you’re not familiar with how to do conditional forwarding with DNS, see the following TechNet article: [Assign a Conditional Forwarder for a Domain Name](https://technet.microsoft.com/library/cc794735), or the documentation specific to your DNS solution.</span><span class="sxs-lookup"><span data-stu-id="a89fb-170">If you’re not familiar with how to do conditional forwarding with DNS, see the following TechNet article: [Assign a Conditional Forwarder for a Domain Name](https://technet.microsoft.com/library/cc794735), or the documentation specific to your DNS solution.</span></span>

<span data-ttu-id="a89fb-171">In scenarios where you specified your external Azure Stack DNS Zone to look like a child domain of your corporate domain name, conditional forwarding cannot be used.</span><span class="sxs-lookup"><span data-stu-id="a89fb-171">In scenarios where you specified your external Azure Stack DNS Zone to look like a child domain of your corporate domain name, conditional forwarding cannot be used.</span></span> <span data-ttu-id="a89fb-172">DNS delegation must be configured.</span><span class="sxs-lookup"><span data-stu-id="a89fb-172">DNS delegation must be configured.</span></span>

<span data-ttu-id="a89fb-173">Example:</span><span class="sxs-lookup"><span data-stu-id="a89fb-173">Example:</span></span>

- <span data-ttu-id="a89fb-174">Corporate DNS Domain Name: `contoso.com`</span><span class="sxs-lookup"><span data-stu-id="a89fb-174">Corporate DNS Domain Name: `contoso.com`</span></span>
- <span data-ttu-id="a89fb-175">Azure Stack External DNS Domain Name: `azurestack.contoso.com`</span><span class="sxs-lookup"><span data-stu-id="a89fb-175">Azure Stack External DNS Domain Name: `azurestack.contoso.com`</span></span>

## <a name="delegating-the-external-dns-zone-to-azure-stack"></a><span data-ttu-id="a89fb-176">Delegating the external DNS zone to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a89fb-176">Delegating the external DNS zone to Azure Stack</span></span>

<span data-ttu-id="a89fb-177">For DNS names to be resolvable from outside an Azure Stack deployment, you need to set up DNS delegation.</span><span class="sxs-lookup"><span data-stu-id="a89fb-177">For DNS names to be resolvable from outside an Azure Stack deployment, you need to set up DNS delegation.</span></span>

<span data-ttu-id="a89fb-178">Each registrar has their own DNS management tools to change the name server records for a domain.</span><span class="sxs-lookup"><span data-stu-id="a89fb-178">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="a89fb-179">In the registrar's DNS management page, edit the NS records and replace the NS records for the zone with the ones in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a89fb-179">In the registrar's DNS management page, edit the NS records and replace the NS records for the zone with the ones in Azure Stack.</span></span>

<span data-ttu-id="a89fb-180">Most DNS registrars require you to provide a minimum of two DNS servers to complete the delegation.</span><span class="sxs-lookup"><span data-stu-id="a89fb-180">Most DNS registrars require you to provide a minimum of two DNS servers to complete the delegation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a89fb-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="a89fb-181">Next steps</span></span>

[<span data-ttu-id="a89fb-182">Firewall integration</span><span class="sxs-lookup"><span data-stu-id="a89fb-182">Firewall integration</span></span>](azure-stack-firewall.md)
