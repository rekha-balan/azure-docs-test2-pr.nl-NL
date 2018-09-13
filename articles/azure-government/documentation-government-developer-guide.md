---
title: Azure Government developer guide | Microsoft Docs
description: This article compares features and provides guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: smichelotti
manager: zakramer
ms.assetid: 6e04e9aa-1a73-442c-a46c-2e4ff87e58d5
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 03/19/2017
ms.author: stemi
ms.openlocfilehash: f4b1acd9ef59315555b110de36183720c80bbfd9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555028"
---
# <a name="azure-government-developer-guide"></a><span data-ttu-id="c3726-103">Azure Government developer guide</span><span class="sxs-lookup"><span data-stu-id="c3726-103">Azure Government developer guide</span></span>
<span data-ttu-id="c3726-104">The Azure Government environment is a physical instance that is separate from the rest of the Microsoft network.</span><span class="sxs-lookup"><span data-stu-id="c3726-104">The Azure Government environment is a physical instance that is separate from the rest of the Microsoft network.</span></span> <span data-ttu-id="c3726-105">This guide discusses the differences that application developers and administrators must understand to interact and work with separate regions of Azure.</span><span class="sxs-lookup"><span data-stu-id="c3726-105">This guide discusses the differences that application developers and administrators must understand to interact and work with separate regions of Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="c3726-106">Overview</span><span class="sxs-lookup"><span data-stu-id="c3726-106">Overview</span></span>
<span data-ttu-id="c3726-107">Azure Government is a separate instance of the Microsoft Azure service.</span><span class="sxs-lookup"><span data-stu-id="c3726-107">Azure Government is a separate instance of the Microsoft Azure service.</span></span> <span data-ttu-id="c3726-108">It addresses the security and compliance needs of United States federal agencies, state and local governments, and their solution providers.</span><span class="sxs-lookup"><span data-stu-id="c3726-108">It addresses the security and compliance needs of United States federal agencies, state and local governments, and their solution providers.</span></span> <span data-ttu-id="c3726-109">Azure Government offers physical isolation from non-US government deployments and provides screened US personnel.</span><span class="sxs-lookup"><span data-stu-id="c3726-109">Azure Government offers physical isolation from non-US government deployments and provides screened US personnel.</span></span>

<span data-ttu-id="c3726-110">Microsoft provides various tools to help developers create and deploy cloud applications to the global Microsoft Azure service (“global service”) and Microsoft Azure Government services.</span><span class="sxs-lookup"><span data-stu-id="c3726-110">Microsoft provides various tools to help developers create and deploy cloud applications to the global Microsoft Azure service (“global service”) and Microsoft Azure Government services.</span></span>

<span data-ttu-id="c3726-111">When developers create and deploy applications to Azure Government services, as opposed to the global service, they need to know the key differences between the two services.</span><span class="sxs-lookup"><span data-stu-id="c3726-111">When developers create and deploy applications to Azure Government services, as opposed to the global service, they need to know the key differences between the two services.</span></span> <span data-ttu-id="c3726-112">The specific areas to understand are: setting up and configuring their programming environment, configuring endpoints, writing applications, and deploying the applications as services to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c3726-112">The specific areas to understand are: setting up and configuring their programming environment, configuring endpoints, writing applications, and deploying the applications as services to Azure Government.</span></span>

<span data-ttu-id="c3726-113">The information in this document summarizes the differences between the two services.</span><span class="sxs-lookup"><span data-stu-id="c3726-113">The information in this document summarizes the differences between the two services.</span></span> <span data-ttu-id="c3726-114">It supplements the information that's available on the [Azure Government](http://www.azure.com/gov "Azure Government") site and the [Microsoft Azure Technical Library](http://msdn.microsoft.com/cloud-app-development-msdn "MSDN") on MSDN.</span><span class="sxs-lookup"><span data-stu-id="c3726-114">It supplements the information that's available on the [Azure Government](http://www.azure.com/gov "Azure Government") site and the [Microsoft Azure Technical Library](http://msdn.microsoft.com/cloud-app-development-msdn "MSDN") on MSDN.</span></span> <span data-ttu-id="c3726-115">Official information might also be available in other locations, such as the [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/ "Microsoft Azure Trust Center"), [Azure Documentation Center](https://azure.microsoft.com/documentation/), and [Azure Blogs](https://azure.microsoft.com/blog/ "Azure Blogs").</span><span class="sxs-lookup"><span data-stu-id="c3726-115">Official information might also be available in other locations, such as the [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/ "Microsoft Azure Trust Center"), [Azure Documentation Center](https://azure.microsoft.com/documentation/), and [Azure Blogs](https://azure.microsoft.com/blog/ "Azure Blogs").</span></span>

<span data-ttu-id="c3726-116">This content is intended for partners and developers who are deploying to Microsoft Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c3726-116">This content is intended for partners and developers who are deploying to Microsoft Azure Government.</span></span>

## <a name="guidance-for-developers"></a><span data-ttu-id="c3726-117">Guidance for developers</span><span class="sxs-lookup"><span data-stu-id="c3726-117">Guidance for developers</span></span>
<span data-ttu-id="c3726-118">Most of the currently available technical content assumes that applications are being developed for the global service rather than for Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c3726-118">Most of the currently available technical content assumes that applications are being developed for the global service rather than for Azure Government.</span></span> <span data-ttu-id="c3726-119">For this reason, it’s important to be aware of two key differences in applications that you develop for hosting in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c3726-119">For this reason, it’s important to be aware of two key differences in applications that you develop for hosting in Azure Government.</span></span>

* <span data-ttu-id="c3726-120">Certain services and features that are in specific regions of the global service might not be available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c3726-120">Certain services and features that are in specific regions of the global service might not be available in Azure Government.</span></span>
* <span data-ttu-id="c3726-121">Feature configurations in Azure Government might differ from those in the global service.</span><span class="sxs-lookup"><span data-stu-id="c3726-121">Feature configurations in Azure Government might differ from those in the global service.</span></span> <span data-ttu-id="c3726-122">Therefore, it's important to review your sample code, configurations, and steps to ensure that you are building and executing within the Azure Government Cloud Services environment.</span><span class="sxs-lookup"><span data-stu-id="c3726-122">Therefore, it's important to review your sample code, configurations, and steps to ensure that you are building and executing within the Azure Government Cloud Services environment.</span></span>

<span data-ttu-id="c3726-123">Currently, US GOV Iowa and US GOV Virginia are the datacenters that support Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c3726-123">Currently, US GOV Iowa and US GOV Virginia are the datacenters that support Azure Government.</span></span> <span data-ttu-id="c3726-124">For current datacenters and available services, see [Products available by region](https://azure.microsoft.com/regions/services).</span><span class="sxs-lookup"><span data-stu-id="c3726-124">For current datacenters and available services, see [Products available by region](https://azure.microsoft.com/regions/services).</span></span>


## <a name="endpoint-mapping"></a><span data-ttu-id="c3726-125">Endpoint mapping</span><span class="sxs-lookup"><span data-stu-id="c3726-125">Endpoint mapping</span></span>
<span data-ttu-id="c3726-126">To learn about mapping public Azure and SQL Database endpoints to Azure Government-specific endpoints, see the following table:</span><span class="sxs-lookup"><span data-stu-id="c3726-126">To learn about mapping public Azure and SQL Database endpoints to Azure Government-specific endpoints, see the following table:</span></span>

| <span data-ttu-id="c3726-127">Name</span><span class="sxs-lookup"><span data-stu-id="c3726-127">Name</span></span> | <span data-ttu-id="c3726-128">Azure Government endpoint</span><span class="sxs-lookup"><span data-stu-id="c3726-128">Azure Government endpoint</span></span> |
| --- | --- |
| <span data-ttu-id="c3726-129">ActiveDirectoryServiceEndpointResourceId</span><span class="sxs-lookup"><span data-stu-id="c3726-129">ActiveDirectoryServiceEndpointResourceId</span></span>  | https://management.core.usgovcloudapi.net/ |
| <span data-ttu-id="c3726-130">GalleryUrl</span><span class="sxs-lookup"><span data-stu-id="c3726-130">GalleryUrl</span></span> | https://gallery.usgovcloudapi.net/ |
| <span data-ttu-id="c3726-131">ManagementPortalUrl</span><span class="sxs-lookup"><span data-stu-id="c3726-131">ManagementPortalUrl</span></span> | https://manage.windowsazure.us |
| <span data-ttu-id="c3726-132">ServiceManagementUrl</span><span class="sxs-lookup"><span data-stu-id="c3726-132">ServiceManagementUrl</span></span> | https://management.core.usgovcloudapi.net/ |
| <span data-ttu-id="c3726-133">PublishSettingsFileUrl</span><span class="sxs-lookup"><span data-stu-id="c3726-133">PublishSettingsFileUrl</span></span> | https://manage.windowsazure.us/publishsettings/index |
| <span data-ttu-id="c3726-134">ResourceManagerUrl</span><span class="sxs-lookup"><span data-stu-id="c3726-134">ResourceManagerUrl</span></span> | https://management.usgovcloudapi.net/ |
| <span data-ttu-id="c3726-135">SqlDatabaseDnsSuffix</span><span class="sxs-lookup"><span data-stu-id="c3726-135">SqlDatabaseDnsSuffix</span></span> | <span data-ttu-id="c3726-136">.database.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="c3726-136">.database.usgovcloudapi.net</span></span> |
| <span data-ttu-id="c3726-137">StorageEndpointSuffix</span><span class="sxs-lookup"><span data-stu-id="c3726-137">StorageEndpointSuffix</span></span> | <span data-ttu-id="c3726-138">core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="c3726-138">core.usgovcloudapi.net</span></span> |
| <span data-ttu-id="c3726-139">ActiveDirectoryAuthority</span><span class="sxs-lookup"><span data-stu-id="c3726-139">ActiveDirectoryAuthority</span></span> | https://login.microsoftonline.us/ |
| <span data-ttu-id="c3726-140">GraphUrl</span><span class="sxs-lookup"><span data-stu-id="c3726-140">GraphUrl</span></span> | https://graph.windows.net/ |
| <span data-ttu-id="c3726-141">GraphEndpointResourceId</span><span class="sxs-lookup"><span data-stu-id="c3726-141">GraphEndpointResourceId</span></span> | https://graph.windows.net/ |
| <span data-ttu-id="c3726-142">TrafficManagerDnsSuffix</span><span class="sxs-lookup"><span data-stu-id="c3726-142">TrafficManagerDnsSuffix</span></span> | <span data-ttu-id="c3726-143">usgovtrafficmanager.net</span><span class="sxs-lookup"><span data-stu-id="c3726-143">usgovtrafficmanager.net</span></span> |
| <span data-ttu-id="c3726-144">AzureKeyVaultDnsSuffix</span><span class="sxs-lookup"><span data-stu-id="c3726-144">AzureKeyVaultDnsSuffix</span></span> | <span data-ttu-id="c3726-145">vault.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="c3726-145">vault.usgovcloudapi.net</span></span> |
| <span data-ttu-id="c3726-146">AzureKeyVaultServiceEndpointResourceId</span><span class="sxs-lookup"><span data-stu-id="c3726-146">AzureKeyVaultServiceEndpointResourceId</span></span> | https://vault.usgovcloudapi.net |

> [!NOTE]
> <span data-ttu-id="c3726-147">The **ActiveDirectoryAuthority** for Azure Government has changed from https://login-us.microsoftonline.com to https://login.microsoftonline.us.</span><span class="sxs-lookup"><span data-stu-id="c3726-147">The **ActiveDirectoryAuthority** for Azure Government has changed from https://login-us.microsoftonline.com to https://login.microsoftonline.us.</span></span>  <span data-ttu-id="c3726-148">The original URL will continue to work but all applications should be updated to the new authority URL.</span><span class="sxs-lookup"><span data-stu-id="c3726-148">The original URL will continue to work but all applications should be updated to the new authority URL.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c3726-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3726-149">Next steps</span></span>
<span data-ttu-id="c3726-150">For more information about Azure Government, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="c3726-150">For more information about Azure Government, see the following resources:</span></span>

* [<span data-ttu-id="c3726-151">Sign up for a trial</span><span class="sxs-lookup"><span data-stu-id="c3726-151">Sign up for a trial</span></span>](https://azuregov.microsoft.com/trial/azuregovtrial)
* [<span data-ttu-id="c3726-152">Acquiring and accessing Azure Government</span><span class="sxs-lookup"><span data-stu-id="c3726-152">Acquiring and accessing Azure Government</span></span>](http://azure.com/gov)
* [<span data-ttu-id="c3726-153">Azure Government Overview</span><span class="sxs-lookup"><span data-stu-id="c3726-153">Azure Government Overview</span></span>](/azure-government-overview)
* [<span data-ttu-id="c3726-154">Azure Government Blog</span><span class="sxs-lookup"><span data-stu-id="c3726-154">Azure Government Blog</span></span>](http://blogs.msdn.microsoft.com/azuregov/)
* [<span data-ttu-id="c3726-155">Azure Compliance</span><span class="sxs-lookup"><span data-stu-id="c3726-155">Azure Compliance</span></span>](https://www.microsoft.com/trustcenter/compliance/complianceofferings)
