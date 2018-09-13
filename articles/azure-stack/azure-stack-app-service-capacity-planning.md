---
title: Capacity planning for Azure App Service server roles in Azure Stack | Microsoft Docs
description: Capacity planning for Azure App Service server roles in Azure Stack
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2018
ms.author: brenduns
ms.reviewer: anwestg
ms.openlocfilehash: f54481fe59df21b500ee860d1e9a202ed32bdd87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871664"
---
# <a name="capacity-planning-for-azure-app-service-server-roles-in-azure-stack"></a><span data-ttu-id="e662e-103">Capacity planning for Azure App Service server roles in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e662e-103">Capacity planning for Azure App Service server roles in Azure Stack</span></span>

<span data-ttu-id="e662e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="e662e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="e662e-105">To set up a production ready deployment of Azure App Service on Azure Stack, you must plan for the capacity you expect the system to support.</span><span class="sxs-lookup"><span data-stu-id="e662e-105">To set up a production ready deployment of Azure App Service on Azure Stack, you must plan for the capacity you expect the system to support.</span></span>  

<span data-ttu-id="e662e-106">This article provides guidance for the minimum number of compute instances and compute SKUs you should use for any production deployment.</span><span class="sxs-lookup"><span data-stu-id="e662e-106">This article provides guidance for the minimum number of compute instances and compute SKUs you should use for any production deployment.</span></span>

<span data-ttu-id="e662e-107">You can plan your App Service capacity strategy using these guidelines.</span><span class="sxs-lookup"><span data-stu-id="e662e-107">You can plan your App Service capacity strategy using these guidelines.</span></span> <span data-ttu-id="e662e-108">Future versions of Azure Stack will provide high availability options for App Service.</span><span class="sxs-lookup"><span data-stu-id="e662e-108">Future versions of Azure Stack will provide high availability options for App Service.</span></span>

| <span data-ttu-id="e662e-109">App Service server role</span><span class="sxs-lookup"><span data-stu-id="e662e-109">App Service server role</span></span> | <span data-ttu-id="e662e-110">Minimum recommended number of instances</span><span class="sxs-lookup"><span data-stu-id="e662e-110">Minimum recommended number of instances</span></span> | <span data-ttu-id="e662e-111">Recommended compute SKU</span><span class="sxs-lookup"><span data-stu-id="e662e-111">Recommended compute SKU</span></span>|
| --- | --- | --- |
| <span data-ttu-id="e662e-112">Controller</span><span class="sxs-lookup"><span data-stu-id="e662e-112">Controller</span></span> | <span data-ttu-id="e662e-113">2</span><span class="sxs-lookup"><span data-stu-id="e662e-113">2</span></span> | <span data-ttu-id="e662e-114">A1</span><span class="sxs-lookup"><span data-stu-id="e662e-114">A1</span></span> |
| <span data-ttu-id="e662e-115">Front End</span><span class="sxs-lookup"><span data-stu-id="e662e-115">Front End</span></span> | <span data-ttu-id="e662e-116">2</span><span class="sxs-lookup"><span data-stu-id="e662e-116">2</span></span> | <span data-ttu-id="e662e-117">A1</span><span class="sxs-lookup"><span data-stu-id="e662e-117">A1</span></span> |
| <span data-ttu-id="e662e-118">Management</span><span class="sxs-lookup"><span data-stu-id="e662e-118">Management</span></span> | <span data-ttu-id="e662e-119">2</span><span class="sxs-lookup"><span data-stu-id="e662e-119">2</span></span> | <span data-ttu-id="e662e-120">A3</span><span class="sxs-lookup"><span data-stu-id="e662e-120">A3</span></span> |
| <span data-ttu-id="e662e-121">Publisher</span><span class="sxs-lookup"><span data-stu-id="e662e-121">Publisher</span></span> | <span data-ttu-id="e662e-122">2</span><span class="sxs-lookup"><span data-stu-id="e662e-122">2</span></span> | <span data-ttu-id="e662e-123">A1</span><span class="sxs-lookup"><span data-stu-id="e662e-123">A1</span></span> |
| <span data-ttu-id="e662e-124">Web Workers - shared</span><span class="sxs-lookup"><span data-stu-id="e662e-124">Web Workers - shared</span></span> | <span data-ttu-id="e662e-125">2</span><span class="sxs-lookup"><span data-stu-id="e662e-125">2</span></span> | <span data-ttu-id="e662e-126">A1</span><span class="sxs-lookup"><span data-stu-id="e662e-126">A1</span></span> |
| <span data-ttu-id="e662e-127">Web Workers - dedicated</span><span class="sxs-lookup"><span data-stu-id="e662e-127">Web Workers - dedicated</span></span> | <span data-ttu-id="e662e-128">2 per tier</span><span class="sxs-lookup"><span data-stu-id="e662e-128">2 per tier</span></span> | <span data-ttu-id="e662e-129">A1</span><span class="sxs-lookup"><span data-stu-id="e662e-129">A1</span></span> |

## <a name="controller-role"></a><span data-ttu-id="e662e-130">Controller role</span><span class="sxs-lookup"><span data-stu-id="e662e-130">Controller role</span></span>

<span data-ttu-id="e662e-131">**Recommended minimum**: Two instances of A1 Standard</span><span class="sxs-lookup"><span data-stu-id="e662e-131">**Recommended minimum**: Two instances of A1 Standard</span></span>

<span data-ttu-id="e662e-132">The Azure App Service Controller typically experiences low consumption of CPU, memory, and network resources.</span><span class="sxs-lookup"><span data-stu-id="e662e-132">The Azure App Service Controller typically experiences low consumption of CPU, memory, and network resources.</span></span> <span data-ttu-id="e662e-133">However, for high availability, you must have two controllers.</span><span class="sxs-lookup"><span data-stu-id="e662e-133">However, for high availability, you must have two controllers.</span></span> <span data-ttu-id="e662e-134">Two controllers are also the maximum number of controllers permitted.</span><span class="sxs-lookup"><span data-stu-id="e662e-134">Two controllers are also the maximum number of controllers permitted.</span></span> <span data-ttu-id="e662e-135">You can create the second Web Sites Controller direct from the installer during deployment.</span><span class="sxs-lookup"><span data-stu-id="e662e-135">You can create the second Web Sites Controller direct from the installer during deployment.</span></span>

## <a name="front-end-role"></a><span data-ttu-id="e662e-136">Front End role</span><span class="sxs-lookup"><span data-stu-id="e662e-136">Front End role</span></span>

<span data-ttu-id="e662e-137">**Recommended minimum**: Two instances of A1 Standard</span><span class="sxs-lookup"><span data-stu-id="e662e-137">**Recommended minimum**: Two instances of A1 Standard</span></span>

<span data-ttu-id="e662e-138">The Front End routes requests to Web Workers depending on Web Worker availability.</span><span class="sxs-lookup"><span data-stu-id="e662e-138">The Front End routes requests to Web Workers depending on Web Worker availability.</span></span> <span data-ttu-id="e662e-139">For high availability, you should have more than one Front End, and you can have more than two.</span><span class="sxs-lookup"><span data-stu-id="e662e-139">For high availability, you should have more than one Front End, and you can have more than two.</span></span> <span data-ttu-id="e662e-140">For capacity planning purposes, consider that each core can handle approximately 100 requests per second.</span><span class="sxs-lookup"><span data-stu-id="e662e-140">For capacity planning purposes, consider that each core can handle approximately 100 requests per second.</span></span>

## <a name="management-role"></a><span data-ttu-id="e662e-141">Management role</span><span class="sxs-lookup"><span data-stu-id="e662e-141">Management role</span></span>

<span data-ttu-id="e662e-142">**Recommended minimum**: Two instances of A3 Standard</span><span class="sxs-lookup"><span data-stu-id="e662e-142">**Recommended minimum**: Two instances of A3 Standard</span></span>

<span data-ttu-id="e662e-143">The Azure App Service Management Role is responsible for the App Service Azure Resource Manager and API Endpoints, portal extensions (admin, tenant, Functions portal), and the data service.</span><span class="sxs-lookup"><span data-stu-id="e662e-143">The Azure App Service Management Role is responsible for the App Service Azure Resource Manager and API Endpoints, portal extensions (admin, tenant, Functions portal), and the data service.</span></span> <span data-ttu-id="e662e-144">The Management Server role typically requires only about 4-GB RAM in a production environment.</span><span class="sxs-lookup"><span data-stu-id="e662e-144">The Management Server role typically requires only about 4-GB RAM in a production environment.</span></span> <span data-ttu-id="e662e-145">However, it may experience high CPU levels when many management tasks (such as web site creation) are performed.</span><span class="sxs-lookup"><span data-stu-id="e662e-145">However, it may experience high CPU levels when many management tasks (such as web site creation) are performed.</span></span> <span data-ttu-id="e662e-146">For high availability, you should have more than one server assigned to this role, and at least two cores per server.</span><span class="sxs-lookup"><span data-stu-id="e662e-146">For high availability, you should have more than one server assigned to this role, and at least two cores per server.</span></span>

## <a name="publisher-role"></a><span data-ttu-id="e662e-147">Publisher role</span><span class="sxs-lookup"><span data-stu-id="e662e-147">Publisher role</span></span>

<span data-ttu-id="e662e-148">**Recommended minimum**: Two instances of A1 Standard</span><span class="sxs-lookup"><span data-stu-id="e662e-148">**Recommended minimum**: Two instances of A1 Standard</span></span>

<span data-ttu-id="e662e-149">If many users are publishing simultaneously, the Publisher role may experience heavy CPU usage.</span><span class="sxs-lookup"><span data-stu-id="e662e-149">If many users are publishing simultaneously, the Publisher role may experience heavy CPU usage.</span></span> <span data-ttu-id="e662e-150">For high availability, make more than one Publisher role available.</span><span class="sxs-lookup"><span data-stu-id="e662e-150">For high availability, make more than one Publisher role available.</span></span>  <span data-ttu-id="e662e-151">The Publisher only handles FTP/FTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="e662e-151">The Publisher only handles FTP/FTPS traffic.</span></span>

## <a name="web-worker-role"></a><span data-ttu-id="e662e-152">Web worker role</span><span class="sxs-lookup"><span data-stu-id="e662e-152">Web worker role</span></span>

<span data-ttu-id="e662e-153">**Recommended minimum**: Two instances of A1 Standard</span><span class="sxs-lookup"><span data-stu-id="e662e-153">**Recommended minimum**: Two instances of A1 Standard</span></span>

<span data-ttu-id="e662e-154">For high availability, you should have at least four Web Worker Roles, two for Shared web site mode and two for each Dedicated worker tier you plan to offer.</span><span class="sxs-lookup"><span data-stu-id="e662e-154">For high availability, you should have at least four Web Worker Roles, two for Shared web site mode and two for each Dedicated worker tier you plan to offer.</span></span> <span data-ttu-id="e662e-155">The Shared and dedicated compute modes provide different levels of service to tenants.</span><span class="sxs-lookup"><span data-stu-id="e662e-155">The Shared and dedicated compute modes provide different levels of service to tenants.</span></span> <span data-ttu-id="e662e-156">You might need more Web Workers if many of your customers are:</span><span class="sxs-lookup"><span data-stu-id="e662e-156">You might need more Web Workers if many of your customers are:</span></span>

- <span data-ttu-id="e662e-157">Using dedicated compute mode worker tiers (which are resource-intensive.)</span><span class="sxs-lookup"><span data-stu-id="e662e-157">Using dedicated compute mode worker tiers (which are resource-intensive.)</span></span>
- <span data-ttu-id="e662e-158">Running in shared compute mode.</span><span class="sxs-lookup"><span data-stu-id="e662e-158">Running in shared compute mode.</span></span>

<span data-ttu-id="e662e-159">After a user has created an App Service Plan for a dedicated compute mode SKU, the number of Web Worker(s) specified in that App Service Plan will no longer be available to users.</span><span class="sxs-lookup"><span data-stu-id="e662e-159">After a user has created an App Service Plan for a dedicated compute mode SKU, the number of Web Worker(s) specified in that App Service Plan will no longer be available to users.</span></span>

<span data-ttu-id="e662e-160">To provide Azure Functions to users in the consumption plan model, you must deploy Shared Web Workers.</span><span class="sxs-lookup"><span data-stu-id="e662e-160">To provide Azure Functions to users in the consumption plan model, you must deploy Shared Web Workers.</span></span>

<span data-ttu-id="e662e-161">When deciding on the number of shared Web Worker roles to use, review these considerations:</span><span class="sxs-lookup"><span data-stu-id="e662e-161">When deciding on the number of shared Web Worker roles to use, review these considerations:</span></span>

- <span data-ttu-id="e662e-162">**Memory**: Memory is the most critical resource for a Web Worker role.</span><span class="sxs-lookup"><span data-stu-id="e662e-162">**Memory**: Memory is the most critical resource for a Web Worker role.</span></span> <span data-ttu-id="e662e-163">Insufficient memory impacts web site performance when virtual memory is swapped from disk.</span><span class="sxs-lookup"><span data-stu-id="e662e-163">Insufficient memory impacts web site performance when virtual memory is swapped from disk.</span></span> <span data-ttu-id="e662e-164">Each server requires about 1.2 GB of RAM for the operating system.</span><span class="sxs-lookup"><span data-stu-id="e662e-164">Each server requires about 1.2 GB of RAM for the operating system.</span></span> <span data-ttu-id="e662e-165">RAM above this threshold can be used to run web sites.</span><span class="sxs-lookup"><span data-stu-id="e662e-165">RAM above this threshold can be used to run web sites.</span></span>
- <span data-ttu-id="e662e-166">**Percentage of active web sites**: Typically, about 5 percent of applications in an Azure App Service on Azure Stack deployment are active.</span><span class="sxs-lookup"><span data-stu-id="e662e-166">**Percentage of active web sites**: Typically, about 5 percent of applications in an Azure App Service on Azure Stack deployment are active.</span></span> <span data-ttu-id="e662e-167">However, the percentage of applications that are active at any given moment can be higher or lower.</span><span class="sxs-lookup"><span data-stu-id="e662e-167">However, the percentage of applications that are active at any given moment can be higher or lower.</span></span> <span data-ttu-id="e662e-168">With an active application rate of 5 percent, the maximum number of applications to place in an Azure App Service on Azure Stack deployment should be less than:</span><span class="sxs-lookup"><span data-stu-id="e662e-168">With an active application rate of 5 percent, the maximum number of applications to place in an Azure App Service on Azure Stack deployment should be less than:</span></span>
  - <span data-ttu-id="e662e-169">20 times the number of active web sites (5 x 20 = 100).</span><span class="sxs-lookup"><span data-stu-id="e662e-169">20 times the number of active web sites (5 x 20 = 100).</span></span>
- <span data-ttu-id="e662e-170">**Average memory footprint**: The average memory footprint for applications observed in production environments is about 70 MB.</span><span class="sxs-lookup"><span data-stu-id="e662e-170">**Average memory footprint**: The average memory footprint for applications observed in production environments is about 70 MB.</span></span> <span data-ttu-id="e662e-171">Using this footprint, the memory allocated across all Web Worker role computers or VMs can be calculated as follows:</span><span class="sxs-lookup"><span data-stu-id="e662e-171">Using this footprint, the memory allocated across all Web Worker role computers or VMs can be calculated as follows:</span></span>

    <span data-ttu-id="e662e-172">*Number of Provisioned applications \* 70 MB \* 5% - (Number of Web Worker Roles \* 1044 MB)*</span><span class="sxs-lookup"><span data-stu-id="e662e-172">*Number of Provisioned applications \* 70 MB \* 5% - (Number of Web Worker Roles \* 1044 MB)*</span></span>

   <span data-ttu-id="e662e-173">For example, if there are 5,000 applications on environment that is running 10 Web Worker roles, each Web Worker role VM should have 7060 MB RAM:</span><span class="sxs-lookup"><span data-stu-id="e662e-173">For example, if there are 5,000 applications on environment that is running 10 Web Worker roles, each Web Worker role VM should have 7060 MB RAM:</span></span>

   <span data-ttu-id="e662e-174">5,000 \* 70 \* 0.05 – (10 \* 1044) = 7060 (=about 7 GB)</span><span class="sxs-lookup"><span data-stu-id="e662e-174">5,000 \* 70 \* 0.05 – (10 \* 1044) = 7060 (=about 7 GB)</span></span>

   <span data-ttu-id="e662e-175">For information on adding more worker instances, see [Adding more worker roles](azure-stack-app-service-add-worker-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e662e-175">For information on adding more worker instances, see [Adding more worker roles](azure-stack-app-service-add-worker-roles.md).</span></span>

## <a name="file-server-role"></a><span data-ttu-id="e662e-176">File server role</span><span class="sxs-lookup"><span data-stu-id="e662e-176">File server role</span></span>

<span data-ttu-id="e662e-177">For the File Server role, you can use a Standalone file server for development and testing, for example when deploying Azure App Service on the Azure Stack Development Kit you can use this template - <https://aka.ms/appsvconmasdkfstemplate>.</span><span class="sxs-lookup"><span data-stu-id="e662e-177">For the File Server role, you can use a Standalone file server for development and testing, for example when deploying Azure App Service on the Azure Stack Development Kit you can use this template - <https://aka.ms/appsvconmasdkfstemplate>.</span></span> <span data-ttu-id="e662e-178">For production purposes, you should use a pre-configured Windows File Server, or a pre-configured non-Windows file server.</span><span class="sxs-lookup"><span data-stu-id="e662e-178">For production purposes, you should use a pre-configured Windows File Server, or a pre-configured non-Windows file server.</span></span>

<span data-ttu-id="e662e-179">In production environments, the File Server role experiences intensive disk I/O.</span><span class="sxs-lookup"><span data-stu-id="e662e-179">In production environments, the File Server role experiences intensive disk I/O.</span></span> <span data-ttu-id="e662e-180">Because it houses all of the content and application files for user web sites, you should pre-configure one of the following for this role:</span><span class="sxs-lookup"><span data-stu-id="e662e-180">Because it houses all of the content and application files for user web sites, you should pre-configure one of the following for this role:</span></span>

- <span data-ttu-id="e662e-181">a Windows File Server</span><span class="sxs-lookup"><span data-stu-id="e662e-181">a Windows File Server</span></span>
- <span data-ttu-id="e662e-182">a Windows File Server Cluster</span><span class="sxs-lookup"><span data-stu-id="e662e-182">a Windows File Server Cluster</span></span>
- <span data-ttu-id="e662e-183">a non-Windows file server</span><span class="sxs-lookup"><span data-stu-id="e662e-183">a non-Windows file server</span></span>
- <span data-ttu-id="e662e-184">a non-Windows file server cluster</span><span class="sxs-lookup"><span data-stu-id="e662e-184">a non-Windows file server cluster</span></span>
- <span data-ttu-id="e662e-185">a NAS (Network Attached Storage) device</span><span class="sxs-lookup"><span data-stu-id="e662e-185">a NAS (Network Attached Storage) device</span></span>

<span data-ttu-id="e662e-186">For more information, see [provision a file server](azure-stack-app-service-before-you-get-started.md#prepare-the-file-server).</span><span class="sxs-lookup"><span data-stu-id="e662e-186">For more information, see [provision a file server](azure-stack-app-service-before-you-get-started.md#prepare-the-file-server).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e662e-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="e662e-187">Next steps</span></span>

[<span data-ttu-id="e662e-188">Before you get started with App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e662e-188">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
