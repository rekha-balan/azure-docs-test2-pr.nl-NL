---
title: How to create and deploy a cloud service | Microsoft Docs
description: Learn how to create and deploy a cloud service using the Azure portal.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: be33c0fef9dab28d4607047a6d849c8458b26498
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553854"
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="6ef7c-103">How to create and deploy a cloud service</span><span class="sxs-lookup"><span data-stu-id="6ef7c-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-create-deploy-portal.md)
> * [Azure classic portal](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="6ef7c-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="6ef7c-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="6ef7c-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="6ef7c-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard. For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.
>
>

## <a name="concepts"></a><span data-ttu-id="6ef7c-112">Concepts</span><span class="sxs-lookup"><span data-stu-id="6ef7c-112">Concepts</span></span>
<span data-ttu-id="6ef7c-113">Three components are required to deploy an application as a cloud service in Azure:</span><span class="sxs-lookup"><span data-stu-id="6ef7c-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="6ef7c-114">**Service Definition**</span><span class="sxs-lookup"><span data-stu-id="6ef7c-114">**Service Definition**</span></span>  
  <span data-ttu-id="6ef7c-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="6ef7c-116">**Service Configuration**</span><span class="sxs-lookup"><span data-stu-id="6ef7c-116">**Service Configuration**</span></span>  
  <span data-ttu-id="6ef7c-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="6ef7c-118">**Service Package**</span><span class="sxs-lookup"><span data-stu-id="6ef7c-118">**Service Package**</span></span>  
  <span data-ttu-id="6ef7c-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="6ef7c-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="6ef7c-121">Prepare your app</span><span class="sxs-lookup"><span data-stu-id="6ef7c-121">Prepare your app</span></span>
<span data-ttu-id="6ef7c-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="6ef7c-123">The Azure SDK provides tools for preparing these required deployment files.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="6ef7c-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="6ef7c-125">Three cloud service features require special configurations before you export a service package:</span><span class="sxs-lookup"><span data-stu-id="6ef7c-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="6ef7c-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="6ef7c-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span> <span data-ttu-id="6ef7c-128">This can only be done in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-128">This can only be done in the classic portal.</span></span>
* <span data-ttu-id="6ef7c-129">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-129">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="6ef7c-130">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-130">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="6ef7c-131">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-131">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="6ef7c-132">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-132">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="6ef7c-133">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-133">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6ef7c-134">Before you begin</span><span class="sxs-lookup"><span data-stu-id="6ef7c-134">Before you begin</span></span>
* <span data-ttu-id="6ef7c-135">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-135">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="6ef7c-136">(You'll have an opportunity to do this later.)</span><span class="sxs-lookup"><span data-stu-id="6ef7c-136">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="6ef7c-137">If any role instances require a certificate, create the certificates.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-137">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="6ef7c-138">Cloud services require a .pfx file with a private key.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-138">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="6ef7c-139">[You can upload the certificates to Azure]() as you create and deploy the cloud service.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-139">[You can upload the certificates to Azure]() as you create and deploy the cloud service.</span></span>
* <span data-ttu-id="6ef7c-140">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-140">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span></span> <span data-ttu-id="6ef7c-141">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-141">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span></span> <span data-ttu-id="6ef7c-142">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-142">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="6ef7c-143">Create and deploy</span><span class="sxs-lookup"><span data-stu-id="6ef7c-143">Create and deploy</span></span>
1. <span data-ttu-id="6ef7c-144">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-144">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6ef7c-145">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-145">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Publish your cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="6ef7c-147">At the bottom of the information page that displays, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-147">At the bottom of the information page that displays, click **Create**.</span></span>
4. <span data-ttu-id="6ef7c-148">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-148">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
5. <span data-ttu-id="6ef7c-149">Create a new **Resource Group** or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-149">Create a new **Resource Group** or select an existing one.</span></span>
6. <span data-ttu-id="6ef7c-150">Select a **Location**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-150">Select a **Location**.</span></span>
7. <span data-ttu-id="6ef7c-151">Click **Package**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-151">Click **Package**.</span></span> <span data-ttu-id="6ef7c-152">This will open the **Upload a package** blade.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-152">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="6ef7c-153">Fill in the required fields.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-153">Fill in the required fields.</span></span> <span data-ttu-id="6ef7c-154">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-154">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>

    > [!IMPORTANT]
    > Cloud Services can only be associated with [classic storage accounts](../azure-resource-manager/resource-manager-deployment-model.md). If you see a message saying that no storage accounts were found for your subscription and location, make sure you have created a classic storage account for your cloud service in that location.

8. <span data-ttu-id="6ef7c-157">Make sure that **Start deployment** is selected.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-157">Make sure that **Start deployment** is selected.</span></span>
9. <span data-ttu-id="6ef7c-158">Click **OK** which will close the **Upload a package** blade.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-158">Click **OK** which will close the **Upload a package** blade.</span></span>
10. <span data-ttu-id="6ef7c-159">If you do not have any certificates to add, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-159">If you do not have any certificates to add, click **Create**.</span></span>

    ![Publish your cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="6ef7c-161">Upload a certificate</span><span class="sxs-lookup"><span data-stu-id="6ef7c-161">Upload a certificate</span></span>
<span data-ttu-id="6ef7c-162">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-162">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="6ef7c-163">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span><span class="sxs-lookup"><span data-stu-id="6ef7c-163">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="6ef7c-164">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-164">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="6ef7c-165">Click **Create** on the **Cloud Service** blade.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-165">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="6ef7c-166">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-166">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Publish your cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="6ef7c-168">Verify your deployment completed successfully</span><span class="sxs-lookup"><span data-stu-id="6ef7c-168">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="6ef7c-169">Click the cloud service instance.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-169">Click the cloud service instance.</span></span>

    <span data-ttu-id="6ef7c-170">The status should show that the service is **Running**.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-170">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="6ef7c-171">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span><span class="sxs-lookup"><span data-stu-id="6ef7c-171">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="6ef7c-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ef7c-173">Next steps</span></span>
* <span data-ttu-id="6ef7c-174">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-174">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="6ef7c-175">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-175">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="6ef7c-176">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-176">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="6ef7c-177">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ef7c-177">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>




