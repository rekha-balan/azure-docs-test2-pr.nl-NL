---
title: How to use Azure API Management with Internal virtual network | Microsoft Docs
description: Learn how to setup and configure Azure API Management in Internal virtual network.
services: api-management
documentationcenter: ''
author: solankisamir
manager: kjoshi
editor: ''
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1941b25e7ae303b82d350b1964939120395b0cf2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550176"
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="2d92a-103">Using Azure API Management service with Internal Virtual Network</span><span class="sxs-lookup"><span data-stu-id="2d92a-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="2d92a-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span><span class="sxs-lookup"><span data-stu-id="2d92a-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="2d92a-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span><span class="sxs-lookup"><span data-stu-id="2d92a-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="2d92a-106">External</span><span class="sxs-lookup"><span data-stu-id="2d92a-106">External</span></span>
* <span data-ttu-id="2d92a-107">Internal</span><span class="sxs-lookup"><span data-stu-id="2d92a-107">Internal</span></span>

## <span data-ttu-id="2d92a-108"><a name="overview"> </a>Overview</span><span class="sxs-lookup"><span data-stu-id="2d92a-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="2d92a-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span><span class="sxs-lookup"><span data-stu-id="2d92a-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="2d92a-110">None of the service endpoints are registered on the Public DNS Server.</span><span class="sxs-lookup"><span data-stu-id="2d92a-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="2d92a-111">Using API Management in Internal mode, you can achieve the following scenarios</span><span class="sxs-lookup"><span data-stu-id="2d92a-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="2d92a-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span><span class="sxs-lookup"><span data-stu-id="2d92a-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="2d92a-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span><span class="sxs-lookup"><span data-stu-id="2d92a-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="2d92a-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span><span class="sxs-lookup"><span data-stu-id="2d92a-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="2d92a-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span><span class="sxs-lookup"><span data-stu-id="2d92a-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="2d92a-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span><span class="sxs-lookup"><span data-stu-id="2d92a-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="2d92a-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span><span class="sxs-lookup"><span data-stu-id="2d92a-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="2d92a-118">Enable VNET connection using Azure portal</span><span class="sxs-lookup"><span data-stu-id="2d92a-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="2d92a-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="2d92a-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="2d92a-120">Then set-up API Management to be deployed inside a Virtual network.</span><span class="sxs-lookup"><span data-stu-id="2d92a-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menu for Setting up APIM in Internal Virtual Network][api-management-using-internal-vnet-menu]

<span data-ttu-id="2d92a-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="2d92a-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![API Management Dashboard with Internal VNET configured][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="2d92a-124">Enable VNET connection using Powershell cmdlets</span><span class="sxs-lookup"><span data-stu-id="2d92a-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="2d92a-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2d92a-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="2d92a-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.apimanagement/v3.1.0/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span><span class="sxs-lookup"><span data-stu-id="2d92a-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.apimanagement/v3.1.0/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="2d92a-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.apimanagement/v3.1.0/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span><span class="sxs-lookup"><span data-stu-id="2d92a-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.apimanagement/v3.1.0/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <a name="apim-dns-configuration"></a><span data-ttu-id="2d92a-128">DNS configuration</span><span class="sxs-lookup"><span data-stu-id="2d92a-128">DNS configuration</span></span>
<span data-ttu-id="2d92a-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="2d92a-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="2d92a-130">For Internal Virtual network mode, you have to manage your own DNS.</span><span class="sxs-lookup"><span data-stu-id="2d92a-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="2d92a-131">API Management service does not listen to requests coming on IP addresses.</span><span class="sxs-lookup"><span data-stu-id="2d92a-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="2d92a-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span><span class="sxs-lookup"><span data-stu-id="2d92a-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="2d92a-133">Access on default host names:</span><span class="sxs-lookup"><span data-stu-id="2d92a-133">Access on default host names:</span></span>
<span data-ttu-id="2d92a-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span><span class="sxs-lookup"><span data-stu-id="2d92a-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="2d92a-135">Gateway / Proxy - contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="2d92a-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="2d92a-137">Direct Management Endpoint - contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="2d92a-138">GIT - contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="2d92a-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span><span class="sxs-lookup"><span data-stu-id="2d92a-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="2d92a-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span><span class="sxs-lookup"><span data-stu-id="2d92a-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="2d92a-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="2d92a-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="2d92a-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="2d92a-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2d92a-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="2d92a-145">You can then access all the service endpoints from the Virtual Machine you created.</span><span class="sxs-lookup"><span data-stu-id="2d92a-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="2d92a-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span><span class="sxs-lookup"><span data-stu-id="2d92a-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="2d92a-147">Access on custom domain names:</span><span class="sxs-lookup"><span data-stu-id="2d92a-147">Access on custom domain names:</span></span>
<span data-ttu-id="2d92a-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span><span class="sxs-lookup"><span data-stu-id="2d92a-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Setting up custom domain for API Management][api-management-custom-domain-name]

<span data-ttu-id="2d92a-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span><span class="sxs-lookup"><span data-stu-id="2d92a-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="2d92a-151"><a name="related-content"> </a>Related content</span><span class="sxs-lookup"><span data-stu-id="2d92a-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="2d92a-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="2d92a-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="2d92a-153">Virtual Network faqs</span><span class="sxs-lookup"><span data-stu-id="2d92a-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="2d92a-154">Creating A record in DNS</span><span class="sxs-lookup"><span data-stu-id="2d92a-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues



