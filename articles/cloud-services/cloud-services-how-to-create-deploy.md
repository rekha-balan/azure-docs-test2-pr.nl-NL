---
title: How to create and deploy a cloud service | Microsoft Docs
description: Learn how to create and deploy a cloud service using the Quick Create method in Azure.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2017
ms.author: adegeo
ms.openlocfilehash: 625a1f073f5f9b525d4f7e14831966957cdc1443
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549433"
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="953e8-103">How to Create and Deploy a Cloud Service</span><span class="sxs-lookup"><span data-stu-id="953e8-103">How to Create and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-create-deploy-portal.md)
> * [Azure classic portal](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="953e8-106">The Azure classic portal provides two ways for you to create and deploy a cloud service: **Quick Create** and **Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="953e8-106">The Azure classic portal provides two ways for you to create and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="953e8-107">This topic explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span><span class="sxs-lookup"><span data-stu-id="953e8-107">This topic explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="953e8-108">When you use this method, the Azure classic portal makes available convenient links for completing all requirements as you go.</span><span class="sxs-lookup"><span data-stu-id="953e8-108">When you use this method, the Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="953e8-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using **Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="953e8-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using **Custom Create**.</span></span>

> [!NOTE]
> If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from **Quick Start** or the dashboard. For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.
> 
> 

## <a name="concepts"></a><span data-ttu-id="953e8-112">Concepts</span><span class="sxs-lookup"><span data-stu-id="953e8-112">Concepts</span></span>
<span data-ttu-id="953e8-113">Three components are required in order to deploy an application as a cloud service in Azure:</span><span class="sxs-lookup"><span data-stu-id="953e8-113">Three components are required in order to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="953e8-114">**Service Definition**</span><span class="sxs-lookup"><span data-stu-id="953e8-114">**Service Definition**</span></span>  
  <span data-ttu-id="953e8-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span><span class="sxs-lookup"><span data-stu-id="953e8-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="953e8-116">**Service Configuration**</span><span class="sxs-lookup"><span data-stu-id="953e8-116">**Service Configuration**</span></span>  
  <span data-ttu-id="953e8-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span><span class="sxs-lookup"><span data-stu-id="953e8-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="953e8-118">**Service Package**</span><span class="sxs-lookup"><span data-stu-id="953e8-118">**Service Package**</span></span>  
  <span data-ttu-id="953e8-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span><span class="sxs-lookup"><span data-stu-id="953e8-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="953e8-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="953e8-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="953e8-121">Prepare your app</span><span class="sxs-lookup"><span data-stu-id="953e8-121">Prepare your app</span></span>
<span data-ttu-id="953e8-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="953e8-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="953e8-123">The Azure SDK provides tools for preparing these required deployment files.</span><span class="sxs-lookup"><span data-stu-id="953e8-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="953e8-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span><span class="sxs-lookup"><span data-stu-id="953e8-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="953e8-125">Three cloud service features require special configurations before you export a service package:</span><span class="sxs-lookup"><span data-stu-id="953e8-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="953e8-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span><span class="sxs-lookup"><span data-stu-id="953e8-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="953e8-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="953e8-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="953e8-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="953e8-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="953e8-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="953e8-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="953e8-130">"Verbose monitoring\* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span><span class="sxs-lookup"><span data-stu-id="953e8-130">"Verbose monitoring\* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="953e8-131">To find out how to enable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="953e8-131">To find out how to enable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="953e8-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="953e8-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="953e8-133">Before you begin</span><span class="sxs-lookup"><span data-stu-id="953e8-133">Before you begin</span></span>
* <span data-ttu-id="953e8-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span><span class="sxs-lookup"><span data-stu-id="953e8-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="953e8-135">(You'll have an opportunity to do this later.)</span><span class="sxs-lookup"><span data-stu-id="953e8-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="953e8-136">If any role instances require a certificate, create the certificates.</span><span class="sxs-lookup"><span data-stu-id="953e8-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="953e8-137">Cloud services require a .pfx file with a private key.</span><span class="sxs-lookup"><span data-stu-id="953e8-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="953e8-138">You can [upload the certificates to Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy the cloud service.</span><span class="sxs-lookup"><span data-stu-id="953e8-138">You can [upload the certificates to Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy the cloud service.</span></span>
* <span data-ttu-id="953e8-139">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span><span class="sxs-lookup"><span data-stu-id="953e8-139">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span></span> <span data-ttu-id="953e8-140">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span><span class="sxs-lookup"><span data-stu-id="953e8-140">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span></span> <span data-ttu-id="953e8-141">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span><span class="sxs-lookup"><span data-stu-id="953e8-141">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="953e8-142">How to: Create a cloud service using Quick Create</span><span class="sxs-lookup"><span data-stu-id="953e8-142">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="953e8-143">In the [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="953e8-143">In the [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="953e8-145">In **URL**, enter a subdomain name to use in the public URL for accessing your cloud service in production deployments.</span><span class="sxs-lookup"><span data-stu-id="953e8-145">In **URL**, enter a subdomain name to use in the public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="953e8-146">The URL format for production deployments is: http://*myURL*.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="953e8-146">The URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="953e8-147">In **Region or Affinity Group**, select the geographic region or affinity group to deploy the cloud service to.</span><span class="sxs-lookup"><span data-stu-id="953e8-147">In **Region or Affinity Group**, select the geographic region or affinity group to deploy the cloud service to.</span></span> <span data-ttu-id="953e8-148">Select an affinity group if you want to deploy your cloud service to the same location as other Azure services within a region.</span><span class="sxs-lookup"><span data-stu-id="953e8-148">Select an affinity group if you want to deploy your cloud service to the same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="953e8-149">Click **Create Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="953e8-149">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="953e8-151">You can monitor the status of the process in the message area at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="953e8-151">You can monitor the status of the process in the message area at the bottom of the window.</span></span>
   
    <span data-ttu-id="953e8-152">The **Cloud Services** area opens, with the new cloud service displayed.</span><span class="sxs-lookup"><span data-stu-id="953e8-152">The **Cloud Services** area opens, with the new cloud service displayed.</span></span> <span data-ttu-id="953e8-153">When the status changes to Created, cloud service creation has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="953e8-153">When the status changes to Created, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="953e8-155">How to: Upload a certificate for a cloud service</span><span class="sxs-lookup"><span data-stu-id="953e8-155">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="953e8-156">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="953e8-156">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="953e8-158">Click either **Upload a certificate** or **Upload**.</span><span class="sxs-lookup"><span data-stu-id="953e8-158">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="953e8-159">In **File**, use **Browse** to select the certificate (.pfx file).</span><span class="sxs-lookup"><span data-stu-id="953e8-159">In **File**, use **Browse** to select the certificate (.pfx file).</span></span>
4. <span data-ttu-id="953e8-160">In **Password**, enter the private key for the certificate.</span><span class="sxs-lookup"><span data-stu-id="953e8-160">In **Password**, enter the private key for the certificate.</span></span>
5. <span data-ttu-id="953e8-161">Click **OK** (checkmark).</span><span class="sxs-lookup"><span data-stu-id="953e8-161">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="953e8-163">You can watch the progress of the upload in the message area, shown below.</span><span class="sxs-lookup"><span data-stu-id="953e8-163">You can watch the progress of the upload in the message area, shown below.</span></span> <span data-ttu-id="953e8-164">When the upload completes, the certificate is added to the table.</span><span class="sxs-lookup"><span data-stu-id="953e8-164">When the upload completes, the certificate is added to the table.</span></span> <span data-ttu-id="953e8-165">In the message area, click OK to close the message.</span><span class="sxs-lookup"><span data-stu-id="953e8-165">In the message area, click OK to close the message.</span></span>
   
    ![CloudServices_CertificateProgress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="953e8-167">How to: Deploy a cloud service</span><span class="sxs-lookup"><span data-stu-id="953e8-167">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="953e8-168">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="953e8-168">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="953e8-169">Click either **Upload a new production deployment** or **Upload**.</span><span class="sxs-lookup"><span data-stu-id="953e8-169">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="953e8-170">In **Deployment label**, enter a name for the new deployment - for example, MyCloudServicev4.</span><span class="sxs-lookup"><span data-stu-id="953e8-170">In **Deployment label**, enter a name for the new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="953e8-171">In **Package**, use **Browse** to select the service package file (.cspkg) to use.</span><span class="sxs-lookup"><span data-stu-id="953e8-171">In **Package**, use **Browse** to select the service package file (.cspkg) to use.</span></span>
5. <span data-ttu-id="953e8-172">In **Configuration**, use **Browse** to select the service configure file (.cscfg) to use.</span><span class="sxs-lookup"><span data-stu-id="953e8-172">In **Configuration**, use **Browse** to select the service configure file (.cscfg) to use.</span></span>
6. <span data-ttu-id="953e8-173">If the cloud service will include any roles with only one instance, select the **Deploy even if one or more roles contain a single instance** check box to enable the deployment to proceed.</span><span class="sxs-lookup"><span data-stu-id="953e8-173">If the cloud service will include any roles with only one instance, select the **Deploy even if one or more roles contain a single instance** check box to enable the deployment to proceed.</span></span>
   
    <span data-ttu-id="953e8-174">Azure can only guarantee 99.95 percent access to the cloud service during maintenance and service updates if every role has at least two instances.</span><span class="sxs-lookup"><span data-stu-id="953e8-174">Azure can only guarantee 99.95 percent access to the cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="953e8-175">If needed, you can add additional role instances on the **Scale** page after you deploy the cloud service.</span><span class="sxs-lookup"><span data-stu-id="953e8-175">If needed, you can add additional role instances on the **Scale** page after you deploy the cloud service.</span></span> <span data-ttu-id="953e8-176">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="953e8-176">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="953e8-177">Click **OK** (checkmark) to begin the cloud service deployment.</span><span class="sxs-lookup"><span data-stu-id="953e8-177">Click **OK** (checkmark) to begin the cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="953e8-179">You can monitor the status of the deployment in the message area.</span><span class="sxs-lookup"><span data-stu-id="953e8-179">You can monitor the status of the deployment in the message area.</span></span> <span data-ttu-id="953e8-180">Click OK to hide the message.</span><span class="sxs-lookup"><span data-stu-id="953e8-180">Click OK to hide the message.</span></span>
   
    ![CloudServices_UploadProgress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="953e8-182">Verify your deployment completed successfully</span><span class="sxs-lookup"><span data-stu-id="953e8-182">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="953e8-183">Click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="953e8-183">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="953e8-184">The status should show that the service is **Running**.</span><span class="sxs-lookup"><span data-stu-id="953e8-184">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="953e8-185">Under **quick glance**, click the site URL to open your cloud service in a web browser.</span><span class="sxs-lookup"><span data-stu-id="953e8-185">Under **quick glance**, click the site URL to open your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)

[TFSTutorialForCloudService]: cloud-services-continuous-delivery-use-vso.md

## <a name="next-steps"></a><span data-ttu-id="953e8-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="953e8-187">Next steps</span></span>
* <span data-ttu-id="953e8-188">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="953e8-188">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="953e8-189">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="953e8-189">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="953e8-190">[Manage your cloud service](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="953e8-190">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="953e8-191">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="953e8-191">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>










