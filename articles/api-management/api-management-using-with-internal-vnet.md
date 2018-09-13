---
title: How to use Azure API Management with internal virtual networks | Microsoft Docs
description: Learn how to set up and configure Azure API Management on an internal virtual network
services: api-management
documentationcenter: ''
author: vladvino
manager: kjoshi
editor: ''
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: apimpm
ms.openlocfilehash: 6b6fd7395f7aff303f4950fb07bd0472cf7057a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809223"
---
# <a name="using-azure-api-management-service-with-an-internal-virtual-network"></a><span data-ttu-id="0e279-103">Using Azure API Management service with an internal virtual network</span><span class="sxs-lookup"><span data-stu-id="0e279-103">Using Azure API Management service with an internal virtual network</span></span>
<span data-ttu-id="0e279-104">With Azure Virtual Networks, Azure API Management can manage APIs not accessible on the internet.</span><span class="sxs-lookup"><span data-stu-id="0e279-104">With Azure Virtual Networks, Azure API Management can manage APIs not accessible on the internet.</span></span> <span data-ttu-id="0e279-105">A number of VPN technologies are available to make the connection.</span><span class="sxs-lookup"><span data-stu-id="0e279-105">A number of VPN technologies are available to make the connection.</span></span> <span data-ttu-id="0e279-106">API Management can be deployed in two main modes inside a virtual network:</span><span class="sxs-lookup"><span data-stu-id="0e279-106">API Management can be deployed in two main modes inside a virtual network:</span></span>
* <span data-ttu-id="0e279-107">External</span><span class="sxs-lookup"><span data-stu-id="0e279-107">External</span></span>
* <span data-ttu-id="0e279-108">Internal</span><span class="sxs-lookup"><span data-stu-id="0e279-108">Internal</span></span>


<span data-ttu-id="0e279-109">When API Management deploys in internal virtual network mode, all the service endpoints (gateway, the Developer portal, the Azure portal, direct management, and Git) are only visible inside a virtual network that you control the access to.</span><span class="sxs-lookup"><span data-stu-id="0e279-109">When API Management deploys in internal virtual network mode, all the service endpoints (gateway, the Developer portal, the Azure portal, direct management, and Git) are only visible inside a virtual network that you control the access to.</span></span> <span data-ttu-id="0e279-110">None of the service endpoints are registered on the public DNS server.</span><span class="sxs-lookup"><span data-stu-id="0e279-110">None of the service endpoints are registered on the public DNS server.</span></span>

<span data-ttu-id="0e279-111">Using API Management in internal mode, you can achieve the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="0e279-111">Using API Management in internal mode, you can achieve the following scenarios:</span></span>
* <span data-ttu-id="0e279-112">Make APIs hosted in your private datacenter securely accessible by third parties outside of it by using site-to-site or Azure ExpressRoute VPN connections.</span><span class="sxs-lookup"><span data-stu-id="0e279-112">Make APIs hosted in your private datacenter securely accessible by third parties outside of it by using site-to-site or Azure ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="0e279-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-premises APIs through a common gateway.</span><span class="sxs-lookup"><span data-stu-id="0e279-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-premises APIs through a common gateway.</span></span>
* <span data-ttu-id="0e279-114">Manage your APIs hosted in multiple geographic locations by using a single gateway endpoint.</span><span class="sxs-lookup"><span data-stu-id="0e279-114">Manage your APIs hosted in multiple geographic locations by using a single gateway endpoint.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="0e279-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e279-115">Prerequisites</span></span>

<span data-ttu-id="0e279-116">To perform the steps described in this article, you must have:</span><span class="sxs-lookup"><span data-stu-id="0e279-116">To perform the steps described in this article, you must have:</span></span>

+ <span data-ttu-id="0e279-117">**An active Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="0e279-117">**An active Azure subscription**.</span></span>

    [!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

+ <span data-ttu-id="0e279-118">**An Azure API Management instance**.</span><span class="sxs-lookup"><span data-stu-id="0e279-118">**An Azure API Management instance**.</span></span> <span data-ttu-id="0e279-119">For more information, see [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="0e279-119">For more information, see [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

## <span data-ttu-id="0e279-120"><a name="enable-vpn"> </a>Creating an API Management in an internal virtual network</span><span class="sxs-lookup"><span data-stu-id="0e279-120"><a name="enable-vpn"> </a>Creating an API Management in an internal virtual network</span></span>
<span data-ttu-id="0e279-121">The API Management service in an internal virtual network is hosted behind an internal load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="0e279-121">The API Management service in an internal virtual network is hosted behind an internal load balancer (ILB).</span></span>

### <a name="enable-a-virtual-network-connection-using-the-azure-portal"></a><span data-ttu-id="0e279-122">Enable a virtual network connection using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0e279-122">Enable a virtual network connection using the Azure portal</span></span>

1. <span data-ttu-id="0e279-123">Browse to your Azure API Management instance in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0e279-123">Browse to your Azure API Management instance in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0e279-124">Select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="0e279-124">Select **Virtual network**.</span></span>
3. <span data-ttu-id="0e279-125">Configure the API Management instance to be deployed inside the virtual network.</span><span class="sxs-lookup"><span data-stu-id="0e279-125">Configure the API Management instance to be deployed inside the virtual network.</span></span>

    ![Menu for setting up an Azure API Management in an internal virtual network][api-management-using-internal-vnet-menu]

4. <span data-ttu-id="0e279-127">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="0e279-127">Select **Save**.</span></span>

<span data-ttu-id="0e279-128">After the deployment succeeds, you should see the internal virtual IP address of your service on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="0e279-128">After the deployment succeeds, you should see the internal virtual IP address of your service on the dashboard.</span></span>

![API Management dashboard with an internal virtual network configured][api-management-internal-vnet-dashboard]

> [!NOTE]
> <span data-ttu-id="0e279-130">The Test console available on the Azure Portal will not work for **Internal** VNET deployed service, as the Gateway Url is not registered on the Public DNS.</span><span class="sxs-lookup"><span data-stu-id="0e279-130">The Test console available on the Azure Portal will not work for **Internal** VNET deployed service, as the Gateway Url is not registered on the Public DNS.</span></span> <span data-ttu-id="0e279-131">You should instead use the Test Console provided on the **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="0e279-131">You should instead use the Test Console provided on the **Developer portal**.</span></span>

### <a name="enable-a-virtual-network-connection-by-using-powershell-cmdlets"></a><span data-ttu-id="0e279-132">Enable a virtual network connection by using PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="0e279-132">Enable a virtual network connection by using PowerShell cmdlets</span></span>
<span data-ttu-id="0e279-133">You can also enable virtual network connectivity by using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0e279-133">You can also enable virtual network connectivity by using PowerShell cmdlets.</span></span>

* <span data-ttu-id="0e279-134">Create an API Management service inside a virtual network: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a virtual network and configure it to use the internal virtual network type.</span><span class="sxs-lookup"><span data-stu-id="0e279-134">Create an API Management service inside a virtual network: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a virtual network and configure it to use the internal virtual network type.</span></span>

* <span data-ttu-id="0e279-135">Deploy an existing API Management service inside a virtual network: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing API Management service inside a virtual network and configure it to use the internal virtual network type.</span><span class="sxs-lookup"><span data-stu-id="0e279-135">Deploy an existing API Management service inside a virtual network: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing API Management service inside a virtual network and configure it to use the internal virtual network type.</span></span>

## <a name="apim-dns-configuration"></a><span data-ttu-id="0e279-136">DNS configuration</span><span class="sxs-lookup"><span data-stu-id="0e279-136">DNS configuration</span></span>
<span data-ttu-id="0e279-137">When API Management is in external virtual network mode, the DNS is managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="0e279-137">When API Management is in external virtual network mode, the DNS is managed by Azure.</span></span> <span data-ttu-id="0e279-138">For internal virtual network mode, you have to manage your own routing.</span><span class="sxs-lookup"><span data-stu-id="0e279-138">For internal virtual network mode, you have to manage your own routing.</span></span>

> [!NOTE]
> <span data-ttu-id="0e279-139">API Management service does not listen to requests coming from IP addresses.</span><span class="sxs-lookup"><span data-stu-id="0e279-139">API Management service does not listen to requests coming from IP addresses.</span></span> <span data-ttu-id="0e279-140">It only responds to requests to the host name configured on its service endpoints.</span><span class="sxs-lookup"><span data-stu-id="0e279-140">It only responds to requests to the host name configured on its service endpoints.</span></span> <span data-ttu-id="0e279-141">These endpoints include gateway, the Azure portal and the Developer portal, direct management endpoint, and Git.</span><span class="sxs-lookup"><span data-stu-id="0e279-141">These endpoints include gateway, the Azure portal and the Developer portal, direct management endpoint, and Git.</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="0e279-142">Access on default host names</span><span class="sxs-lookup"><span data-stu-id="0e279-142">Access on default host names</span></span>
<span data-ttu-id="0e279-143">When you create an API Management service, named "contoso" for example, the following service endpoints are configured by default:</span><span class="sxs-lookup"><span data-stu-id="0e279-143">When you create an API Management service, named "contoso" for example, the following service endpoints are configured by default:</span></span>

   * <span data-ttu-id="0e279-144">Gateway or proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-144">Gateway or proxy: contoso.azure-api.net</span></span>

   * <span data-ttu-id="0e279-145">The Azure portal and the Developer portal: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-145">The Azure portal and the Developer portal: contoso.portal.azure-api.net</span></span>

   * <span data-ttu-id="0e279-146">Direct management endpoint: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-146">Direct management endpoint: contoso.management.azure-api.net</span></span>

   * <span data-ttu-id="0e279-147">Git: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-147">Git: contoso.scm.azure-api.net</span></span>

<span data-ttu-id="0e279-148">To access these API Management service endpoints, you can create a virtual machine in a subnet connected to the virtual network in which API Management is deployed.</span><span class="sxs-lookup"><span data-stu-id="0e279-148">To access these API Management service endpoints, you can create a virtual machine in a subnet connected to the virtual network in which API Management is deployed.</span></span> <span data-ttu-id="0e279-149">Assuming the internal virtual IP address for your service is 10.0.0.5, you can map the hosts file, %SystemDrive%\drivers\etc\hosts, as follows:</span><span class="sxs-lookup"><span data-stu-id="0e279-149">Assuming the internal virtual IP address for your service is 10.0.0.5, you can map the hosts file, %SystemDrive%\drivers\etc\hosts, as follows:</span></span>

   * <span data-ttu-id="0e279-150">10.0.0.5     contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-150">10.0.0.5     contoso.azure-api.net</span></span>

   * <span data-ttu-id="0e279-151">10.0.0.5     contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-151">10.0.0.5     contoso.portal.azure-api.net</span></span>

   * <span data-ttu-id="0e279-152">10.0.0.5     contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-152">10.0.0.5     contoso.management.azure-api.net</span></span>

   * <span data-ttu-id="0e279-153">10.0.0.5     contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0e279-153">10.0.0.5     contoso.scm.azure-api.net</span></span>

<span data-ttu-id="0e279-154">You can then access all the service endpoints from the virtual machine you created.</span><span class="sxs-lookup"><span data-stu-id="0e279-154">You can then access all the service endpoints from the virtual machine you created.</span></span> <span data-ttu-id="0e279-155">If you use a custom DNS server in a virtual network, you can also create A DNS records and access these endpoints from anywhere in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="0e279-155">If you use a custom DNS server in a virtual network, you can also create A DNS records and access these endpoints from anywhere in your virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="0e279-156">Access on custom domain names</span><span class="sxs-lookup"><span data-stu-id="0e279-156">Access on custom domain names</span></span>

   1. <span data-ttu-id="0e279-157">If you don’t want to access the API Management service with the default host names, you can set up custom domain names for all your service endpoints as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="0e279-157">If you don’t want to access the API Management service with the default host names, you can set up custom domain names for all your service endpoints as shown in the following image:</span></span> 

   ![Setting up a custom domain for API Management][api-management-custom-domain-name]

   2. <span data-ttu-id="0e279-159">Then you can create records in your DNS server to access the endpoints that are only accessible from within your virtual network.</span><span class="sxs-lookup"><span data-stu-id="0e279-159">Then you can create records in your DNS server to access the endpoints that are only accessible from within your virtual network.</span></span>

## <span data-ttu-id="0e279-160"><a name="routing"> </a> Routing</span><span class="sxs-lookup"><span data-stu-id="0e279-160"><a name="routing"> </a> Routing</span></span>
+ <span data-ttu-id="0e279-161">A load balanced private virtual IP address from the subnet range will be reserved and used to access the API Management service endpoints from within the vnet.</span><span class="sxs-lookup"><span data-stu-id="0e279-161">A load balanced private virtual IP address from the subnet range will be reserved and used to access the API Management service endpoints from within the vnet.</span></span>
+ <span data-ttu-id="0e279-162">A load balanced public IP address (VIP) will also be reserved to provide access to the management service endpoint only over port 3443.</span><span class="sxs-lookup"><span data-stu-id="0e279-162">A load balanced public IP address (VIP) will also be reserved to provide access to the management service endpoint only over port 3443.</span></span>
+ <span data-ttu-id="0e279-163">An IP address from a subnet IP range (DIP) will be used to access resources within the vnet and a public IP address (VIP) will be used to access resources outside the vnet.</span><span class="sxs-lookup"><span data-stu-id="0e279-163">An IP address from a subnet IP range (DIP) will be used to access resources within the vnet and a public IP address (VIP) will be used to access resources outside the vnet.</span></span>
+ <span data-ttu-id="0e279-164">Load balanced public and private IP addresses can be found on the Overview/Essentials blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e279-164">Load balanced public and private IP addresses can be found on the Overview/Essentials blade in the Azure portal.</span></span>

## <span data-ttu-id="0e279-165"><a name="related-content"> </a>Related content</span><span class="sxs-lookup"><span data-stu-id="0e279-165"><a name="related-content"> </a>Related content</span></span>
<span data-ttu-id="0e279-166">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="0e279-166">To learn more, see the following articles:</span></span>
* <span data-ttu-id="0e279-167">[Common network configuration problems while setting up Azure API Management in a virtual network][Common network configuration problems]</span><span class="sxs-lookup"><span data-stu-id="0e279-167">[Common network configuration problems while setting up Azure API Management in a virtual network][Common network configuration problems]</span></span>
* [<span data-ttu-id="0e279-168">Virtual network FAQs</span><span class="sxs-lookup"><span data-stu-id="0e279-168">Virtual network FAQs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="0e279-169">Creating a record in DNS</span><span class="sxs-lookup"><span data-stu-id="0e279-169">Creating a record in DNS</span></span>](https://msdn.microsoft.com/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: get-started-create-service-instance.md
[Common network configuration problems]: api-management-using-with-vnet.md#network-configuration-issues

