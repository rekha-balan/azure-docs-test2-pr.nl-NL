---
title: 'Azure Active Directory Domain Services: Enable Azure Active Directory Domain Services | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c44e24f29a7457e8cd99685310e99af891bc63f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554398"
---
# <a name="enable-azure-active-directory-domain-services"></a><span data-ttu-id="bfffd-103">Enable Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="bfffd-103">Enable Azure Active Directory Domain Services</span></span>
## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="bfffd-104">Task 3: Enable Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="bfffd-104">Task 3: Enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="bfffd-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following:</span><span class="sxs-lookup"><span data-stu-id="bfffd-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following:</span></span>

1. <span data-ttu-id="bfffd-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bfffd-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bfffd-107">In the left pane, select the **Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="bfffd-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="bfffd-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="bfffd-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![Select Azure AD Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="bfffd-110">On the **preview directory** page, click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="bfffd-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![Configure tab of directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="bfffd-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="bfffd-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="bfffd-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span><span class="sxs-lookup"><span data-stu-id="bfffd-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![Enable Domain Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="bfffd-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span><span class="sxs-lookup"><span data-stu-id="bfffd-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="bfffd-116">Specify the **DNS domain name of domain services**.</span><span class="sxs-lookup"><span data-stu-id="bfffd-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="bfffd-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span><span class="sxs-lookup"><span data-stu-id="bfffd-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="bfffd-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span><span class="sxs-lookup"><span data-stu-id="bfffd-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="bfffd-119">You can also enter a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="bfffd-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="bfffd-120">In this example, the custom domain name is *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="bfffd-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="bfffd-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span><span class="sxs-lookup"><span data-stu-id="bfffd-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="bfffd-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span><span class="sxs-lookup"><span data-stu-id="bfffd-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="bfffd-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="bfffd-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="bfffd-124">Specifically, check to see whether:</span><span class="sxs-lookup"><span data-stu-id="bfffd-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="bfffd-125">You already have a domain with the same DNS domain name on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="bfffd-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="bfffd-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="bfffd-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="bfffd-127">You have an existing cloud service with that name on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="bfffd-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="bfffd-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span><span class="sxs-lookup"><span data-stu-id="bfffd-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="bfffd-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bfffd-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="bfffd-130">Also consider the following:</span><span class="sxs-lookup"><span data-stu-id="bfffd-130">Also consider the following:</span></span>

   * <span data-ttu-id="bfffd-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="bfffd-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="bfffd-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="bfffd-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="bfffd-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bfffd-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="bfffd-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="bfffd-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="bfffd-135">Do *not* select the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="bfffd-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="bfffd-136">See [networking considerations](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="bfffd-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="bfffd-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bfffd-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="bfffd-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="bfffd-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="bfffd-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bfffd-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span> 
    * <span data-ttu-id="bfffd-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span><span class="sxs-lookup"><span data-stu-id="bfffd-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![Enable Domain Services window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="bfffd-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="bfffd-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="bfffd-143">After you enable Azure Active Directory Domain Services, note that the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span><span class="sxs-lookup"><span data-stu-id="bfffd-143">After you enable Azure Active Directory Domain Services, note that the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="bfffd-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span><span class="sxs-lookup"><span data-stu-id="bfffd-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="bfffd-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="bfffd-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="bfffd-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span><span class="sxs-lookup"><span data-stu-id="bfffd-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![Domain Services window displaying first provisioned IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="bfffd-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span><span class="sxs-lookup"><span data-stu-id="bfffd-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="bfffd-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span><span class="sxs-lookup"><span data-stu-id="bfffd-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span> 
    
10. <span data-ttu-id="bfffd-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span><span class="sxs-lookup"><span data-stu-id="bfffd-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="bfffd-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span><span class="sxs-lookup"><span data-stu-id="bfffd-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![Domain Services window showing both provisioned IPs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="bfffd-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span><span class="sxs-lookup"><span data-stu-id="bfffd-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="bfffd-154">This synchronization process happens in the background.</span><span class="sxs-lookup"><span data-stu-id="bfffd-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="bfffd-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span><span class="sxs-lookup"><span data-stu-id="bfffd-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bfffd-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfffd-156">Next steps</span></span>
<span data-ttu-id="bfffd-157">Task 4: [Update the DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span><span class="sxs-lookup"><span data-stu-id="bfffd-157">Task 4: [Update the DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span></span>






