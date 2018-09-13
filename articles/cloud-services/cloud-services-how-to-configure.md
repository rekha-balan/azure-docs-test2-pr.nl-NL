---
title: How to configure a cloud service (classic portal) | Microsoft Docs
description: Learn how to configure cloud services in Azure. Learn to update the cloud service configuration and configure remote access to role instances.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2017
ms.author: adegeo
ms.openlocfilehash: a0dab3b27db4fc4f2d915ebaa36a7e3e72491ace
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662490"
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="0136b-104">How to Configure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="0136b-104">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-configure-portal.md)
> * [Azure classic portal](cloud-services-how-to-configure.md)
> 
> 

<span data-ttu-id="0136b-107">You can configure the most commonly used settings for a cloud service in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="0136b-107">You can configure the most commonly used settings for a cloud service in the Azure classic portal.</span></span> <span data-ttu-id="0136b-108">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="0136b-108">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="0136b-109">Either way, the configuration updates are pushed out to all role instances.</span><span class="sxs-lookup"><span data-stu-id="0136b-109">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="0136b-110">The Azure classic portal also allows you to [enable Remote Desktop Connection for a Role in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)</span><span class="sxs-lookup"><span data-stu-id="0136b-110">The Azure classic portal also allows you to [enable Remote Desktop Connection for a Role in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)</span></span>

<span data-ttu-id="0136b-111">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span><span class="sxs-lookup"><span data-stu-id="0136b-111">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="0136b-112">That enables one virtual machine to process client requests while the other is being updated.</span><span class="sxs-lookup"><span data-stu-id="0136b-112">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="0136b-113">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="0136b-113">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="0136b-114">Change a cloud service</span><span class="sxs-lookup"><span data-stu-id="0136b-114">Change a cloud service</span></span>
1. <span data-ttu-id="0136b-115">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="0136b-115">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
   
    ![Configuration Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    <span data-ttu-id="0136b-117">On the **Configure** page, you can configure monitoring, update role settings, and choose the guest operating system and family for role instances.</span><span class="sxs-lookup"><span data-stu-id="0136b-117">On the **Configure** page, you can configure monitoring, update role settings, and choose the guest operating system and family for role instances.</span></span> 
2. <span data-ttu-id="0136b-118">In **monitoring**, set the monitoring level to Verbose or Minimal, and configure the diagnostics connection strings that are required for verbose monitoring.</span><span class="sxs-lookup"><span data-stu-id="0136b-118">In **monitoring**, set the monitoring level to Verbose or Minimal, and configure the diagnostics connection strings that are required for verbose monitoring.</span></span>
3. <span data-ttu-id="0136b-119">For service roles (grouped by role), you can update the following settings:</span><span class="sxs-lookup"><span data-stu-id="0136b-119">For service roles (grouped by role), you can update the following settings:</span></span>
   
    * <span data-ttu-id="0136b-120">**Settings** Modify the values of miscellaneous configuration settings that are specified in the *ConfigurationSettings* elements of the service configuration (.cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="0136b-120">**Settings** Modify the values of miscellaneous configuration settings that are specified in the *ConfigurationSettings* elements of the service configuration (.cscfg) file.</span></span>

    * <span data-ttu-id="0136b-121">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="0136b-121">**Certificates**</span></span>  
        <span data-ttu-id="0136b-122">Change the certificate thumbprint that's being used in SSL encryption for a role.</span><span class="sxs-lookup"><span data-stu-id="0136b-122">Change the certificate thumbprint that's being used in SSL encryption for a role.</span></span> <span data-ttu-id="0136b-123">To change a certificate, you must first upload the new certificate (on the **Certificates** page).</span><span class="sxs-lookup"><span data-stu-id="0136b-123">To change a certificate, you must first upload the new certificate (on the **Certificates** page).</span></span> <span data-ttu-id="0136b-124">Then update the thumbprint in the certificate string displayed in the role settings.</span><span class="sxs-lookup"><span data-stu-id="0136b-124">Then update the thumbprint in the certificate string displayed in the role settings.</span></span>
4. <span data-ttu-id="0136b-125">In **operating system**, you can change the operating system family or version for role instances, or choose **Automatic** to enable automatic updates of the current operating system version.</span><span class="sxs-lookup"><span data-stu-id="0136b-125">In **operating system**, you can change the operating system family or version for role instances, or choose **Automatic** to enable automatic updates of the current operating system version.</span></span> <span data-ttu-id="0136b-126">The operating system settings apply to web roles and worker roles, but do not affect Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="0136b-126">The operating system settings apply to web roles and worker roles, but do not affect Virtual Machines.</span></span>
   
    <span data-ttu-id="0136b-127">During deployment, the most recent operating system version is installed on all role instances, and the operating systems are updated automatically by default.</span><span class="sxs-lookup"><span data-stu-id="0136b-127">During deployment, the most recent operating system version is installed on all role instances, and the operating systems are updated automatically by default.</span></span> 
   
    <span data-ttu-id="0136b-128">If you need for your cloud service to run on a different operating system version because of compatibility requirements in your code, you can choose an operating system family and version.</span><span class="sxs-lookup"><span data-stu-id="0136b-128">If you need for your cloud service to run on a different operating system version because of compatibility requirements in your code, you can choose an operating system family and version.</span></span> <span data-ttu-id="0136b-129">When you choose a specific operating system version, automatic operating system updates for the cloud service are suspended.</span><span class="sxs-lookup"><span data-stu-id="0136b-129">When you choose a specific operating system version, automatic operating system updates for the cloud service are suspended.</span></span> <span data-ttu-id="0136b-130">You will need to ensure the operating systems receive updates.</span><span class="sxs-lookup"><span data-stu-id="0136b-130">You will need to ensure the operating systems receive updates.</span></span>
   
    <span data-ttu-id="0136b-131">If you resolve all compatibility issues that your apps have with the most recent operating system version, you can enable automatic operating system updates by setting the operating system version to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="0136b-131">If you resolve all compatibility issues that your apps have with the most recent operating system version, you can enable automatic operating system updates by setting the operating system version to **Automatic**.</span></span> 
   
    ![OS Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. <span data-ttu-id="0136b-133">To save your configuration settings, and push them to the role instances, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0136b-133">To save your configuration settings, and push them to the role instances, click **Save**.</span></span> <span data-ttu-id="0136b-134">(Click **Discard** to cancel the changes.) **Save** and **Discard** are added to the command bar after you change a setting.</span><span class="sxs-lookup"><span data-stu-id="0136b-134">(Click **Discard** to cancel the changes.) **Save** and **Discard** are added to the command bar after you change a setting.</span></span>

## <a name="update-a-cloud-service-configuration-file"></a><span data-ttu-id="0136b-135">Update a cloud service configuration file</span><span class="sxs-lookup"><span data-stu-id="0136b-135">Update a cloud service configuration file</span></span>
1. <span data-ttu-id="0136b-136">Download a cloud service configuration file (.cscfg) with the current configuration.</span><span class="sxs-lookup"><span data-stu-id="0136b-136">Download a cloud service configuration file (.cscfg) with the current configuration.</span></span> <span data-ttu-id="0136b-137">On the **Configure** page for the cloud service, click **Download**.</span><span class="sxs-lookup"><span data-stu-id="0136b-137">On the **Configure** page for the cloud service, click **Download**.</span></span> <span data-ttu-id="0136b-138">Then click **Save**, or click **Save As** to save the file.</span><span class="sxs-lookup"><span data-stu-id="0136b-138">Then click **Save**, or click **Save As** to save the file.</span></span>
2. <span data-ttu-id="0136b-139">After you update the service configuration file, upload and apply the configuration updates:</span><span class="sxs-lookup"><span data-stu-id="0136b-139">After you update the service configuration file, upload and apply the configuration updates:</span></span>
   
   1. <span data-ttu-id="0136b-140">On the **Configure** page, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="0136b-140">On the **Configure** page, click **Upload**.</span></span>
      
       ![Upload Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. <span data-ttu-id="0136b-142">In **Configuration file**, use **Browse** to select the updated .cscfg file.</span><span class="sxs-lookup"><span data-stu-id="0136b-142">In **Configuration file**, use **Browse** to select the updated .cscfg file.</span></span>
   3. <span data-ttu-id="0136b-143">If your cloud service contains any roles that have only one instance, select the **Apply configuration even if one or more roles contain a single instance** check box to enable the configuration updates for the roles to proceed.</span><span class="sxs-lookup"><span data-stu-id="0136b-143">If your cloud service contains any roles that have only one instance, select the **Apply configuration even if one or more roles contain a single instance** check box to enable the configuration updates for the roles to proceed.</span></span>
      
       <span data-ttu-id="0136b-144">Unless you define at least two instances of every role, Azure cannot guarantee at least 99.95 percent availability of your cloud service during service configuration updates.</span><span class="sxs-lookup"><span data-stu-id="0136b-144">Unless you define at least two instances of every role, Azure cannot guarantee at least 99.95 percent availability of your cloud service during service configuration updates.</span></span> <span data-ttu-id="0136b-145">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="0136b-145">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
   4. <span data-ttu-id="0136b-146">Click **OK** (checkmark).</span><span class="sxs-lookup"><span data-stu-id="0136b-146">Click **OK** (checkmark).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0136b-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="0136b-147">Next steps</span></span>
* <span data-ttu-id="0136b-148">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0136b-148">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="0136b-149">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="0136b-149">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="0136b-150">[Manage your cloud service](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="0136b-150">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* [<span data-ttu-id="0136b-151">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="0136b-151">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>](cloud-services-role-enable-remote-desktop.md)
* <span data-ttu-id="0136b-152">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="0136b-152">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>




