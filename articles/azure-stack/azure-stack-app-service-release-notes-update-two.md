---
title: App Service on Azure Stack update 2 release notes | Microsoft Docs
description: Learn about what's in update two for App Service on Azure Stack, the known issues, and where to download the update.
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2018
ms.author: anwestg
ms.reviewer: brenduns
ms.openlocfilehash: be09773a1ce3e80547d9e5f0e9de2a2d9e093c60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856682"
---
# <a name="app-service-on-azure-stack-update-2-release-notes"></a><span data-ttu-id="f809b-103">App Service on Azure Stack update 2 release notes</span><span class="sxs-lookup"><span data-stu-id="f809b-103">App Service on Azure Stack update 2 release notes</span></span>

<span data-ttu-id="f809b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="f809b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="f809b-105">These release notes describe the improvements and fixes in Azure App Service on Azure Stack Update 2 and any known issues.</span><span class="sxs-lookup"><span data-stu-id="f809b-105">These release notes describe the improvements and fixes in Azure App Service on Azure Stack Update 2 and any known issues.</span></span> <span data-ttu-id="f809b-106">Known issues are divided into issues directly related to the deployment, update process, and issues with the build     (post-installation).</span><span class="sxs-lookup"><span data-stu-id="f809b-106">Known issues are divided into issues directly related to the deployment, update process, and issues with the build     (post-installation).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f809b-107">Apply the 1804 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.2.</span><span class="sxs-lookup"><span data-stu-id="f809b-107">Apply the 1804 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.2.</span></span>
>
>

## <a name="build-reference"></a><span data-ttu-id="f809b-108">Build reference</span><span class="sxs-lookup"><span data-stu-id="f809b-108">Build reference</span></span>

<span data-ttu-id="f809b-109">The App Service on Azure Stack Update 2 build number is **72.0.13698.10**</span><span class="sxs-lookup"><span data-stu-id="f809b-109">The App Service on Azure Stack Update 2 build number is **72.0.13698.10**</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f809b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f809b-110">Prerequisites</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f809b-111">New deployments of Azure App Service on Azure Stack now require a [three-subject wildcard certificate](azure-stack-app-service-before-you-get-started.md#get-certificates) due to improvements in the way in which SSO for Kudu is now handled in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f809b-111">New deployments of Azure App Service on Azure Stack now require a [three-subject wildcard certificate](azure-stack-app-service-before-you-get-started.md#get-certificates) due to improvements in the way in which SSO for Kudu is now handled in Azure App Service.</span></span> <span data-ttu-id="f809b-112">The new subject is **\*.sso.appservice.\<region\>.\<domainname\>.\<extension\>**</span><span class="sxs-lookup"><span data-stu-id="f809b-112">The new subject is **\*.sso.appservice.\<region\>.\<domainname\>.\<extension\>**</span></span>
>
>

<span data-ttu-id="f809b-113">Refer to the [Before You Get Started documentation](azure-stack-app-service-before-you-get-started.md) before beginning deployment.</span><span class="sxs-lookup"><span data-stu-id="f809b-113">Refer to the [Before You Get Started documentation](azure-stack-app-service-before-you-get-started.md) before beginning deployment.</span></span>

### <a name="new-features-and-fixes"></a><span data-ttu-id="f809b-114">New features and fixes</span><span class="sxs-lookup"><span data-stu-id="f809b-114">New features and fixes</span></span>

<span data-ttu-id="f809b-115">Azure App Service on Azure Stack Update 2 includes the following improvements and fixes:</span><span class="sxs-lookup"><span data-stu-id="f809b-115">Azure App Service on Azure Stack Update 2 includes the following improvements and fixes:</span></span>

- <span data-ttu-id="f809b-116">Updates to **App Service Tenant, Admin, Functions portals and Kudu tools**.</span><span class="sxs-lookup"><span data-stu-id="f809b-116">Updates to **App Service Tenant, Admin, Functions portals and Kudu tools**.</span></span> <span data-ttu-id="f809b-117">Consistent with Azure Stack Portal SDK version.</span><span class="sxs-lookup"><span data-stu-id="f809b-117">Consistent with Azure Stack Portal SDK version.</span></span>

- <span data-ttu-id="f809b-118">Updates to core service to improve reliability and error messaging enabling easier diagnosis of common issues.</span><span class="sxs-lookup"><span data-stu-id="f809b-118">Updates to core service to improve reliability and error messaging enabling easier diagnosis of common issues.</span></span>

- <span data-ttu-id="f809b-119">**Updates to the following application frameworks and tools**:</span><span class="sxs-lookup"><span data-stu-id="f809b-119">**Updates to the following application frameworks and tools**:</span></span>
  - <span data-ttu-id="f809b-120">Added .Net Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="f809b-120">Added .Net Framework 4.7.1</span></span>
  - <span data-ttu-id="f809b-121">Added **Node.JS** versions:</span><span class="sxs-lookup"><span data-stu-id="f809b-121">Added **Node.JS** versions:</span></span>
    - <span data-ttu-id="f809b-122">NodeJS 6.12.3</span><span class="sxs-lookup"><span data-stu-id="f809b-122">NodeJS 6.12.3</span></span>
    - <span data-ttu-id="f809b-123">NodeJS 8.9.4</span><span class="sxs-lookup"><span data-stu-id="f809b-123">NodeJS 8.9.4</span></span>
    - <span data-ttu-id="f809b-124">NodeJS 8.10.0</span><span class="sxs-lookup"><span data-stu-id="f809b-124">NodeJS 8.10.0</span></span>
    - <span data-ttu-id="f809b-125">NodeJS 8.11.1</span><span class="sxs-lookup"><span data-stu-id="f809b-125">NodeJS 8.11.1</span></span>
  - <span data-ttu-id="f809b-126">Added **NPM** versions:</span><span class="sxs-lookup"><span data-stu-id="f809b-126">Added **NPM** versions:</span></span>
    - <span data-ttu-id="f809b-127">5.6.0</span><span class="sxs-lookup"><span data-stu-id="f809b-127">5.6.0</span></span>
  - <span data-ttu-id="f809b-128">Updated .Net Core components to be consistent with Azure App Service in public cloud.</span><span class="sxs-lookup"><span data-stu-id="f809b-128">Updated .Net Core components to be consistent with Azure App Service in public cloud.</span></span>
  - <span data-ttu-id="f809b-129">Updated Kudu</span><span class="sxs-lookup"><span data-stu-id="f809b-129">Updated Kudu</span></span>

- <span data-ttu-id="f809b-130">Auto Swap of deployment slots feature enabled - [Configuring Auto Swap](https://docs.microsoft.com/azure/app-service/web-sites-staged-publishing#configure-auto-swap)</span><span class="sxs-lookup"><span data-stu-id="f809b-130">Auto Swap of deployment slots feature enabled - [Configuring Auto Swap](https://docs.microsoft.com/azure/app-service/web-sites-staged-publishing#configure-auto-swap)</span></span>

- <span data-ttu-id="f809b-131">Testing in Production feature enabled - [Introduction to Testing in Production](https://azure.microsoft.com/resources/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/)</span><span class="sxs-lookup"><span data-stu-id="f809b-131">Testing in Production feature enabled - [Introduction to Testing in Production](https://azure.microsoft.com/resources/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/)</span></span>

- <span data-ttu-id="f809b-132">Azure Functions Proxies enabled - [Work with Azure Functions Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies)</span><span class="sxs-lookup"><span data-stu-id="f809b-132">Azure Functions Proxies enabled - [Work with Azure Functions Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies)</span></span>

- <span data-ttu-id="f809b-133">App Service Admin extension UX support added for:</span><span class="sxs-lookup"><span data-stu-id="f809b-133">App Service Admin extension UX support added for:</span></span>
  - <span data-ttu-id="f809b-134">Secret rotation</span><span class="sxs-lookup"><span data-stu-id="f809b-134">Secret rotation</span></span>
  - <span data-ttu-id="f809b-135">Certificate rotation</span><span class="sxs-lookup"><span data-stu-id="f809b-135">Certificate rotation</span></span>
  - <span data-ttu-id="f809b-136">System credential rotation</span><span class="sxs-lookup"><span data-stu-id="f809b-136">System credential rotation</span></span>
  - <span data-ttu-id="f809b-137">Connection string rotation</span><span class="sxs-lookup"><span data-stu-id="f809b-137">Connection string rotation</span></span>

### <a name="known-issues-post-installation"></a><span data-ttu-id="f809b-138">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="f809b-138">Known issues (post-installation)</span></span>

- <span data-ttu-id="f809b-139">Workers are unable to reach file server when App Service is deployed in an existing virtual network and the file server is only available on the private network.</span><span class="sxs-lookup"><span data-stu-id="f809b-139">Workers are unable to reach file server when App Service is deployed in an existing virtual network and the file server is only available on the private network.</span></span>

<span data-ttu-id="f809b-140">If you chose to deploy into an existing virtual network and an internal IP address to connect to your file server, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the file server.</span><span class="sxs-lookup"><span data-stu-id="f809b-140">If you chose to deploy into an existing virtual network and an internal IP address to connect to your file server, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the file server.</span></span> <span data-ttu-id="f809b-141">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span><span class="sxs-lookup"><span data-stu-id="f809b-141">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span></span>
 * <span data-ttu-id="f809b-142">Source: Any</span><span class="sxs-lookup"><span data-stu-id="f809b-142">Source: Any</span></span>
 * <span data-ttu-id="f809b-143">Source port range: \*</span><span class="sxs-lookup"><span data-stu-id="f809b-143">Source port range: \*</span></span>
 * <span data-ttu-id="f809b-144">Destination: IP Addresses</span><span class="sxs-lookup"><span data-stu-id="f809b-144">Destination: IP Addresses</span></span>
 * <span data-ttu-id="f809b-145">Destination IP address range: Range of IPs for your file server</span><span class="sxs-lookup"><span data-stu-id="f809b-145">Destination IP address range: Range of IPs for your file server</span></span>
 * <span data-ttu-id="f809b-146">Destination port range: 445</span><span class="sxs-lookup"><span data-stu-id="f809b-146">Destination port range: 445</span></span>
 * <span data-ttu-id="f809b-147">Protocol: TCP</span><span class="sxs-lookup"><span data-stu-id="f809b-147">Protocol: TCP</span></span>
 * <span data-ttu-id="f809b-148">Action: Allow</span><span class="sxs-lookup"><span data-stu-id="f809b-148">Action: Allow</span></span>
 * <span data-ttu-id="f809b-149">Priority: 700</span><span class="sxs-lookup"><span data-stu-id="f809b-149">Priority: 700</span></span>
 * <span data-ttu-id="f809b-150">Name: Outbound_Allow_SMB445</span><span class="sxs-lookup"><span data-stu-id="f809b-150">Name: Outbound_Allow_SMB445</span></span>

### <a name="known-issues-for-cloud-admins-operating-azure-app-service-on-azure-stack"></a><span data-ttu-id="f809b-151">Known issues for Cloud Admins operating Azure App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f809b-151">Known issues for Cloud Admins operating Azure App Service on Azure Stack</span></span>

<span data-ttu-id="f809b-152">Refer to the documentation in the [Azure Stack 1804 Release Notes](azure-stack-update-1804.md)</span><span class="sxs-lookup"><span data-stu-id="f809b-152">Refer to the documentation in the [Azure Stack 1804 Release Notes](azure-stack-update-1804.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f809b-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="f809b-153">Next steps</span></span>

- <span data-ttu-id="f809b-154">For an overview of Azure App Service, see [Azure App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f809b-154">For an overview of Azure App Service, see [Azure App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>
- <span data-ttu-id="f809b-155">For more information about how to prepare to deploy App Service on Azure Stack, see [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f809b-155">For more information about how to prepare to deploy App Service on Azure Stack, see [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md).</span></span>
