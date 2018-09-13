---
title: Options for migrating out of Azure RemoteApp | Microsoft Docs
description: Learn about the options for migrating out of Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: mbaldwin
ms.openlocfilehash: 25ba53a1047863d01ba1fc2647af51fdd582feb1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671168"
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="fc544-103">Options for migrating out of Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fc544-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc544-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="fc544-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fc544-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="fc544-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="fc544-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span><span class="sxs-lookup"><span data-stu-id="fc544-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="fc544-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span><span class="sxs-lookup"><span data-stu-id="fc544-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="fc544-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span><span class="sxs-lookup"><span data-stu-id="fc544-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="fc544-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span><span class="sxs-lookup"><span data-stu-id="fc544-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="fc544-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span><span class="sxs-lookup"><span data-stu-id="fc544-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="fc544-111">Self-managed (IaaS) solutions</span><span class="sxs-lookup"><span data-stu-id="fc544-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="fc544-112">**RDS on IaaS**</span><span class="sxs-lookup"><span data-stu-id="fc544-112">**RDS on IaaS**</span></span>
<span data-ttu-id="fc544-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span><span class="sxs-lookup"><span data-stu-id="fc544-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="fc544-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span><span class="sxs-lookup"><span data-stu-id="fc544-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="fc544-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span><span class="sxs-lookup"><span data-stu-id="fc544-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="fc544-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="fc544-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="fc544-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span><span class="sxs-lookup"><span data-stu-id="fc544-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="fc544-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fc544-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="fc544-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span><span class="sxs-lookup"><span data-stu-id="fc544-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="fc544-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span><span class="sxs-lookup"><span data-stu-id="fc544-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="fc544-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span><span class="sxs-lookup"><span data-stu-id="fc544-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="fc544-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span><span class="sxs-lookup"><span data-stu-id="fc544-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="fc544-123">**Citrix on IaaS**</span><span class="sxs-lookup"><span data-stu-id="fc544-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="fc544-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span><span class="sxs-lookup"><span data-stu-id="fc544-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="fc544-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span><span class="sxs-lookup"><span data-stu-id="fc544-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="fc544-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span><span class="sxs-lookup"><span data-stu-id="fc544-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="fc544-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span><span class="sxs-lookup"><span data-stu-id="fc544-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="fc544-128">Fully managed (PaaS/SaaS) offerings</span><span class="sxs-lookup"><span data-stu-id="fc544-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="awingu"></a><span data-ttu-id="fc544-129">Awingu</span><span class="sxs-lookup"><span data-stu-id="fc544-129">Awingu</span></span>
<span data-ttu-id="fc544-130">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span><span class="sxs-lookup"><span data-stu-id="fc544-130">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="fc544-131">As such, making any applications securely available on any type of device.</span><span class="sxs-lookup"><span data-stu-id="fc544-131">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="fc544-132">For SaaS services, a wide range op Single-Sign-On options is available.</span><span class="sxs-lookup"><span data-stu-id="fc544-132">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="fc544-133">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span><span class="sxs-lookup"><span data-stu-id="fc544-133">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="fc544-134">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span><span class="sxs-lookup"><span data-stu-id="fc544-134">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="fc544-135">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span><span class="sxs-lookup"><span data-stu-id="fc544-135">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="fc544-136">Awingu's solution is multi-tenant, multi-AD and open API.</span><span class="sxs-lookup"><span data-stu-id="fc544-136">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="fc544-137">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="fc544-137">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="fc544-138">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span><span class="sxs-lookup"><span data-stu-id="fc544-138">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="fc544-139">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span><span class="sxs-lookup"><span data-stu-id="fc544-139">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="fc544-140">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="fc544-140">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="fc544-141">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="fc544-141">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="fc544-142">Primary location: Belgium</span><span class="sxs-lookup"><span data-stu-id="fc544-142">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="fc544-143">Operating regions: EMEA, North America and Brazil</span><span class="sxs-lookup"><span data-stu-id="fc544-143">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="fc544-144">Offer session-based RemoteApp and Desktop solutions: Yes, both</span><span class="sxs-lookup"><span data-stu-id="fc544-144">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="fc544-145">**Global**:</span><span class="sxs-lookup"><span data-stu-id="fc544-145">**Global**:</span></span>
> 
> <span data-ttu-id="fc544-146">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="fc544-146">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="fc544-147">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="fc544-147">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="fc544-148">Phone: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="fc544-148">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="fc544-149">**Belgium HQ**:</span><span class="sxs-lookup"><span data-stu-id="fc544-149">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="fc544-150">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="fc544-150">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="fc544-151">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="fc544-151">9000 Gent</span></span>
> 
> <span data-ttu-id="fc544-152">Email: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="fc544-152">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="fc544-153">Phone: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="fc544-153">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="fc544-154">**USA**:</span><span class="sxs-lookup"><span data-stu-id="fc544-154">**USA**:</span></span>
> 
> <span data-ttu-id="fc544-155">7th floor, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="fc544-155">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="fc544-156">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="fc544-156">New York, NY 10036</span></span>
> 
> <span data-ttu-id="fc544-157">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="fc544-157">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="fc544-158">Citrix XenApp Essentials (released April 2017)</span><span class="sxs-lookup"><span data-stu-id="fc544-158">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="fc544-159">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fc544-159">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span>  

<span data-ttu-id="fc544-160">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/global-partners/microsoft/remote-app.html).</span><span class="sxs-lookup"><span data-stu-id="fc544-160">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/global-partners/microsoft/remote-app.html).</span></span>  <span data-ttu-id="fc544-161">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span><span class="sxs-lookup"><span data-stu-id="fc544-161">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="fc544-162">Learn more about [Citrix XenApp Essentials](https://www.citrix.com/global-partners/microsoft/remote-app.html).</span><span class="sxs-lookup"><span data-stu-id="fc544-162">Learn more about [Citrix XenApp Essentials](https://www.citrix.com/global-partners/microsoft/remote-app.html).</span></span>

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="fc544-163">Citrix Cloud XenApp Service and XenDesktop Service</span><span class="sxs-lookup"><span data-stu-id="fc544-163">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="fc544-164">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span><span class="sxs-lookup"><span data-stu-id="fc544-164">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

### <a name="citrix-service-provider-program"></a><span data-ttu-id="fc544-165">Citrix Service Provider Program</span><span class="sxs-lookup"><span data-stu-id="fc544-165">Citrix Service Provider Program</span></span>
<span data-ttu-id="fc544-166">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span><span class="sxs-lookup"><span data-stu-id="fc544-166">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="fc544-167">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span><span class="sxs-lookup"><span data-stu-id="fc544-167">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="fc544-168">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span><span class="sxs-lookup"><span data-stu-id="fc544-168">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="fc544-169">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="fc544-169">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

### <a name="frame"></a><span data-ttu-id="fc544-170">Frame</span><span class="sxs-lookup"><span data-stu-id="fc544-170">Frame</span></span>

<span data-ttu-id="fc544-171">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span><span class="sxs-lookup"><span data-stu-id="fc544-171">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="fc544-172">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span><span class="sxs-lookup"><span data-stu-id="fc544-172">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="fc544-173">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span><span class="sxs-lookup"><span data-stu-id="fc544-173">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="fc544-174">Learn more about [Frame on Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="fc544-174">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="fc544-175">Primary location: San Mateo, CA, USA</span><span class="sxs-lookup"><span data-stu-id="fc544-175">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="fc544-176">Operation region: Worldwide</span><span class="sxs-lookup"><span data-stu-id="fc544-176">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="fc544-177">Microsoft Partner: Yes</span><span class="sxs-lookup"><span data-stu-id="fc544-177">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="fc544-178">Phone: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="fc544-178">Phone: 1-480-269-4668</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="fc544-179">Microsoft Hosted Service Provider</span><span class="sxs-lookup"><span data-stu-id="fc544-179">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="fc544-180">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span><span class="sxs-lookup"><span data-stu-id="fc544-180">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="fc544-181">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span><span class="sxs-lookup"><span data-stu-id="fc544-181">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="fc544-182">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span><span class="sxs-lookup"><span data-stu-id="fc544-182">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

#### <a name="aspex"></a><span data-ttu-id="fc544-183">ASPEX</span><span class="sxs-lookup"><span data-stu-id="fc544-183">ASPEX</span></span>
<span data-ttu-id="fc544-184">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span><span class="sxs-lookup"><span data-stu-id="fc544-184">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="fc544-185">ASPEX offers a wide range of managed services, devops, and consulting services.</span><span class="sxs-lookup"><span data-stu-id="fc544-185">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="fc544-186">Primary location: Antwerp, Belgium</span><span class="sxs-lookup"><span data-stu-id="fc544-186">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="fc544-187">Operation region: Western Europe</span><span class="sxs-lookup"><span data-stu-id="fc544-187">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="fc544-188">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="fc544-188">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="fc544-189">Microsoft Cloud Service Provider: Yes</span><span class="sxs-lookup"><span data-stu-id="fc544-189">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fc544-190">Offer session-based RemoteApp and Desktop solutions: Yes, both</span><span class="sxs-lookup"><span data-stu-id="fc544-190">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fc544-191">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="fc544-191">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="fc544-192">Phone: +3232202198</span><span class="sxs-lookup"><span data-stu-id="fc544-192">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="fc544-193">Mail: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="fc544-193">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="fc544-194">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="fc544-194">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="fc544-195">Conexlink (Platform name: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="fc544-195">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="fc544-196">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span><span class="sxs-lookup"><span data-stu-id="fc544-196">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="fc544-197">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span><span class="sxs-lookup"><span data-stu-id="fc544-197">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="fc544-198">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span><span class="sxs-lookup"><span data-stu-id="fc544-198">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="fc544-199">Primary location: Dallas, TX, USA</span><span class="sxs-lookup"><span data-stu-id="fc544-199">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="fc544-200">Operation region: Worldwide</span><span class="sxs-lookup"><span data-stu-id="fc544-200">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="fc544-201">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="fc544-201">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="fc544-202">Microsoft Cloud Service Provider: Yes</span><span class="sxs-lookup"><span data-stu-id="fc544-202">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fc544-203">Offer session-based RemoteApp and Desktop solutions: Yes, both</span><span class="sxs-lookup"><span data-stu-id="fc544-203">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fc544-204">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="fc544-204">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="fc544-205">Brian Garoutte, VP of Business Development</span><span class="sxs-lookup"><span data-stu-id="fc544-205">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="fc544-206">Phone: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="fc544-206">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="fc544-207">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="fc544-207">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

#### <a name="acuutech"></a><span data-ttu-id="fc544-208">Acuutech</span><span class="sxs-lookup"><span data-stu-id="fc544-208">Acuutech</span></span>
<span data-ttu-id="fc544-209">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span><span class="sxs-lookup"><span data-stu-id="fc544-209">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="fc544-210">Primary location: London, UK; Singapore; Houston, TX</span><span class="sxs-lookup"><span data-stu-id="fc544-210">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="fc544-211">Operation region: Worldwide</span><span class="sxs-lookup"><span data-stu-id="fc544-211">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="fc544-212">Partner status: Gold</span><span class="sxs-lookup"><span data-stu-id="fc544-212">Partner status: Gold</span></span>
> 
> <span data-ttu-id="fc544-213">Microsoft Cloud Service Provider: Yes</span><span class="sxs-lookup"><span data-stu-id="fc544-213">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fc544-214">Offer session-based RemoteApp and Desktop solutions: Yes, both</span><span class="sxs-lookup"><span data-stu-id="fc544-214">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fc544-215">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="fc544-215">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="fc544-216">**United Kingdom**:</span><span class="sxs-lookup"><span data-stu-id="fc544-216">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="fc544-217">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="fc544-217">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="fc544-218">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="fc544-218">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="fc544-219">\*\*Phone: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="fc544-219">\*\*Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="fc544-220">**Singapore**:</span><span class="sxs-lookup"><span data-stu-id="fc544-220">**Singapore**:</span></span>
>   
> <span data-ttu-id="fc544-221">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="fc544-221">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="fc544-222">The Globe, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="fc544-222">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="fc544-223">\*\*Phone: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="fc544-223">\*\*Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="fc544-224">**North America**:</span><span class="sxs-lookup"><span data-stu-id="fc544-224">**North America**:</span></span>
>   
> <span data-ttu-id="fc544-225">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="fc544-225">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="fc544-226">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="fc544-226">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="fc544-227">\*\*Phone: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="fc544-227">\*\*Phone: +1 713 691 0800</span></span>

#### <a name="saasplaza"></a><span data-ttu-id="fc544-228">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="fc544-228">**SaaSplaza**</span></span>
<span data-ttu-id="fc544-229">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span><span class="sxs-lookup"><span data-stu-id="fc544-229">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="fc544-230">Primary location: Netherlands</span><span class="sxs-lookup"><span data-stu-id="fc544-230">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="fc544-231">Operation Region: Worldwide</span><span class="sxs-lookup"><span data-stu-id="fc544-231">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="fc544-232">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="fc544-232">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="fc544-233">Microsoft Cloud Service Provider: Yes</span><span class="sxs-lookup"><span data-stu-id="fc544-233">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fc544-234">Offer session-based RemoteApp and Desktop solutions: Yes, both</span><span class="sxs-lookup"><span data-stu-id="fc544-234">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fc544-235">**EMEA**</span><span class="sxs-lookup"><span data-stu-id="fc544-235">**EMEA**</span></span>
> 
> <span data-ttu-id="fc544-236">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="fc544-236">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="fc544-237">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="fc544-237">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="fc544-238">The Netherlands</span><span class="sxs-lookup"><span data-stu-id="fc544-238">The Netherlands</span></span>
> 
> <span data-ttu-id="fc544-239">Phone: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="fc544-239">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="fc544-240">**Americas**</span><span class="sxs-lookup"><span data-stu-id="fc544-240">**Americas**</span></span>
> 
> <span data-ttu-id="fc544-241">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="fc544-241">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="fc544-242">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="fc544-242">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="fc544-243">San Diego</span><span class="sxs-lookup"><span data-stu-id="fc544-243">San Diego</span></span>
> 
> <span data-ttu-id="fc544-244">United States</span><span class="sxs-lookup"><span data-stu-id="fc544-244">United States</span></span>
> 
> <span data-ttu-id="fc544-245">Phone: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="fc544-245">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="fc544-246">**APAC**</span><span class="sxs-lookup"><span data-stu-id="fc544-246">**APAC**</span></span>
> 
> <span data-ttu-id="fc544-247">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="fc544-247">105 Cecil Street</span></span>
>    
> <span data-ttu-id="fc544-248">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="fc544-248">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="fc544-249">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="fc544-249">Singapore 069534</span></span>
> 
> <span data-ttu-id="fc544-250">Singapore</span><span class="sxs-lookup"><span data-stu-id="fc544-250">Singapore</span></span>
>   
> <span data-ttu-id="fc544-251">Phone - Singapore: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="fc544-251">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="fc544-252">Phone - Australia: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="fc544-252">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="fc544-253">Phone - New Zealand: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="fc544-253">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="fc544-254">Need more help?</span><span class="sxs-lookup"><span data-stu-id="fc544-254">Need more help?</span></span>
<span data-ttu-id="fc544-255">Still need help choosing or have further questions?</span><span class="sxs-lookup"><span data-stu-id="fc544-255">Still need help choosing or have further questions?</span></span> <span data-ttu-id="fc544-256">Use one of the following methods to get help.</span><span class="sxs-lookup"><span data-stu-id="fc544-256">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="fc544-257">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fc544-257">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="fc544-258">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="fc544-258">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="fc544-259">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="fc544-259">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="fc544-260">Call us.</span><span class="sxs-lookup"><span data-stu-id="fc544-260">Call us.</span></span> <span data-ttu-id="fc544-261">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="fc544-261">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

