---
title: Azure Germany developer guide | Microsoft Docs
description: This article compares features and provides guidance on developing applications for Azure Germany.
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2017
ms.author: ralfwi
ms.openlocfilehash: 09b698f66e074a58ebe7ccb1c2fc308d74740294
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868604"
---
# <a name="azure-germany-developer-guide"></a><span data-ttu-id="46dd2-103">Azure Germany developer guide</span><span class="sxs-lookup"><span data-stu-id="46dd2-103">Azure Germany developer guide</span></span>
<span data-ttu-id="46dd2-104">The Azure Germany environment is an instance of Microsoft Azure that is separate from the rest of the Microsoft network.</span><span class="sxs-lookup"><span data-stu-id="46dd2-104">The Azure Germany environment is an instance of Microsoft Azure that is separate from the rest of the Microsoft network.</span></span> <span data-ttu-id="46dd2-105">This guide discusses the differences that application developers and administrators must understand to interact and work with separate regions of Azure.</span><span class="sxs-lookup"><span data-stu-id="46dd2-105">This guide discusses the differences that application developers and administrators must understand to interact and work with separate regions of Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="46dd2-106">Overview</span><span class="sxs-lookup"><span data-stu-id="46dd2-106">Overview</span></span>
<span data-ttu-id="46dd2-107">Microsoft provides various tools to help developers create and deploy cloud applications to the global Microsoft Azure services ("global Azure") and Microsoft Azure Germany services.</span><span class="sxs-lookup"><span data-stu-id="46dd2-107">Microsoft provides various tools to help developers create and deploy cloud applications to the global Microsoft Azure services ("global Azure") and Microsoft Azure Germany services.</span></span> <span data-ttu-id="46dd2-108">Azure Germany addresses the security and compliance needs of customers to follow German data privacy regulations.</span><span class="sxs-lookup"><span data-stu-id="46dd2-108">Azure Germany addresses the security and compliance needs of customers to follow German data privacy regulations.</span></span> <span data-ttu-id="46dd2-109">Azure Germany offers physical and network isolation from global Azure deployments and provides a data trustee acting under German law.</span><span class="sxs-lookup"><span data-stu-id="46dd2-109">Azure Germany offers physical and network isolation from global Azure deployments and provides a data trustee acting under German law.</span></span>

<span data-ttu-id="46dd2-110">When developers create and deploy applications to Azure Germany, as opposed to global Azure, they need to know the differences between the two sets of services.</span><span class="sxs-lookup"><span data-stu-id="46dd2-110">When developers create and deploy applications to Azure Germany, as opposed to global Azure, they need to know the differences between the two sets of services.</span></span> <span data-ttu-id="46dd2-111">The specific areas to understand are: setting up and configuring their programming environment, configuring endpoints, writing applications, and deploying the applications as services to Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="46dd2-111">The specific areas to understand are: setting up and configuring their programming environment, configuring endpoints, writing applications, and deploying the applications as services to Azure Germany.</span></span>

<span data-ttu-id="46dd2-112">The information in this guide summarizes these differences.</span><span class="sxs-lookup"><span data-stu-id="46dd2-112">The information in this guide summarizes these differences.</span></span> <span data-ttu-id="46dd2-113">It supplements the information that's available on the [Azure Germany](https://azure.microsoft.com/overview/clouds/germany/ "Azure Germany") site and the [Azure Documentation Center](https://azure.microsoft.com/documentation/).</span><span class="sxs-lookup"><span data-stu-id="46dd2-113">It supplements the information that's available on the [Azure Germany](https://azure.microsoft.com/overview/clouds/germany/ "Azure Germany") site and the [Azure Documentation Center](https://azure.microsoft.com/documentation/).</span></span> 

<span data-ttu-id="46dd2-114">Official information might also be available in other locations, such as:</span><span class="sxs-lookup"><span data-stu-id="46dd2-114">Official information might also be available in other locations, such as:</span></span>
* [<span data-ttu-id="46dd2-115">Microsoft Azure Trust Center</span><span class="sxs-lookup"><span data-stu-id="46dd2-115">Microsoft Azure Trust Center</span></span>](https://azure.microsoft.com/support/trust-center/ "Microsoft Azure Trust Center") 
* [<span data-ttu-id="46dd2-116">Azure blog</span><span class="sxs-lookup"><span data-stu-id="46dd2-116">Azure blog</span></span>](https://azure.microsoft.com/blog/ "Azure blog")
* [<span data-ttu-id="46dd2-117">Azure Germany blog</span><span class="sxs-lookup"><span data-stu-id="46dd2-117">Azure Germany blog</span></span>](https://blogs.msdn.microsoft.com/azuregermany/ "Azure Germany blog")

## <a name="guidance-for-developers"></a><span data-ttu-id="46dd2-118">Guidance for developers</span><span class="sxs-lookup"><span data-stu-id="46dd2-118">Guidance for developers</span></span>
<span data-ttu-id="46dd2-119">Most of the currently available technical content assumes that applications are being developed for global Azure rather than for Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="46dd2-119">Most of the currently available technical content assumes that applications are being developed for global Azure rather than for Azure Germany.</span></span> <span data-ttu-id="46dd2-120">For this reason, it’s important to be aware of two key differences in applications that you develop for hosting in Azure Germany:</span><span class="sxs-lookup"><span data-stu-id="46dd2-120">For this reason, it’s important to be aware of two key differences in applications that you develop for hosting in Azure Germany:</span></span>

* <span data-ttu-id="46dd2-121">Certain services and features that are in specific regions of global Azure might not be available in Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="46dd2-121">Certain services and features that are in specific regions of global Azure might not be available in Azure Germany.</span></span>
* <span data-ttu-id="46dd2-122">Feature configurations in Azure Germany might differ from those in global Azure.</span><span class="sxs-lookup"><span data-stu-id="46dd2-122">Feature configurations in Azure Germany might differ from those in global Azure.</span></span> <span data-ttu-id="46dd2-123">It's important to review your sample code, configurations, and steps to ensure that you are building and executing within the Azure Germany Cloud Services environment.</span><span class="sxs-lookup"><span data-stu-id="46dd2-123">It's important to review your sample code, configurations, and steps to ensure that you are building and executing within the Azure Germany Cloud Services environment.</span></span>

<span data-ttu-id="46dd2-124">Currently, Germany Central and Germany Northeast are the regions that are available in Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="46dd2-124">Currently, Germany Central and Germany Northeast are the regions that are available in Azure Germany.</span></span> <span data-ttu-id="46dd2-125">For regions and available services, see [Products available by region](https://azure.microsoft.com/regions/services).</span><span class="sxs-lookup"><span data-stu-id="46dd2-125">For regions and available services, see [Products available by region](https://azure.microsoft.com/regions/services).</span></span>


## <a name="endpoint-mapping"></a><span data-ttu-id="46dd2-126">Endpoint mapping</span><span class="sxs-lookup"><span data-stu-id="46dd2-126">Endpoint mapping</span></span>
<span data-ttu-id="46dd2-127">To learn about mapping global Azure and Azure SQL Database endpoints to Azure Germany-specific endpoints, see the following table:</span><span class="sxs-lookup"><span data-stu-id="46dd2-127">To learn about mapping global Azure and Azure SQL Database endpoints to Azure Germany-specific endpoints, see the following table:</span></span>

| <span data-ttu-id="46dd2-128">Name</span><span class="sxs-lookup"><span data-stu-id="46dd2-128">Name</span></span> | <span data-ttu-id="46dd2-129">Azure Germany endpoint</span><span class="sxs-lookup"><span data-stu-id="46dd2-129">Azure Germany endpoint</span></span> |
| --- | --- |
| <span data-ttu-id="46dd2-130">ActiveDirectoryServiceEndpointResourceId</span><span class="sxs-lookup"><span data-stu-id="46dd2-130">ActiveDirectoryServiceEndpointResourceId</span></span> | https://management.core.cloudapi.de/ |
| <span data-ttu-id="46dd2-131">GalleryUrl</span><span class="sxs-lookup"><span data-stu-id="46dd2-131">GalleryUrl</span></span>                               | https://gallery.cloudapi.de/ |
| <span data-ttu-id="46dd2-132">ManagementPortalUrl</span><span class="sxs-lookup"><span data-stu-id="46dd2-132">ManagementPortalUrl</span></span>                      | http://portal.microsoftazure.de/ |
| <span data-ttu-id="46dd2-133">ServiceManagementUrl</span><span class="sxs-lookup"><span data-stu-id="46dd2-133">ServiceManagementUrl</span></span>                     | https://management.core.cloudapi.de/ |
| <span data-ttu-id="46dd2-134">PublishSettingsFileUrl</span><span class="sxs-lookup"><span data-stu-id="46dd2-134">PublishSettingsFileUrl</span></span>                   | https://manage.microsoftazure.de/publishsettings/index |
| <span data-ttu-id="46dd2-135">ResourceManagerUrl</span><span class="sxs-lookup"><span data-stu-id="46dd2-135">ResourceManagerUrl</span></span>                       | https://management.microsoftazure.de/ |
| <span data-ttu-id="46dd2-136">SqlDatabaseDnsSuffix</span><span class="sxs-lookup"><span data-stu-id="46dd2-136">SqlDatabaseDnsSuffix</span></span>                     | <span data-ttu-id="46dd2-137">.database.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="46dd2-137">.database.cloudapi.de</span></span> |
| <span data-ttu-id="46dd2-138">StorageEndpointSuffix</span><span class="sxs-lookup"><span data-stu-id="46dd2-138">StorageEndpointSuffix</span></span>                    | <span data-ttu-id="46dd2-139">core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="46dd2-139">core.cloudapi.de</span></span> |
| <span data-ttu-id="46dd2-140">ActiveDirectoryAuthority</span><span class="sxs-lookup"><span data-stu-id="46dd2-140">ActiveDirectoryAuthority</span></span>                 | https://login.microsoftonline.de/ |
| <span data-ttu-id="46dd2-141">GraphUrl</span><span class="sxs-lookup"><span data-stu-id="46dd2-141">GraphUrl</span></span>                                 | https://graph.cloudapi.de/ |
| <span data-ttu-id="46dd2-142">TrafficManagerDnsSuffix</span><span class="sxs-lookup"><span data-stu-id="46dd2-142">TrafficManagerDnsSuffix</span></span>                  | <span data-ttu-id="46dd2-143">azuretrafficmanager.de</span><span class="sxs-lookup"><span data-stu-id="46dd2-143">azuretrafficmanager.de</span></span> |
| <span data-ttu-id="46dd2-144">AzureKeyVaultDnsSuffix</span><span class="sxs-lookup"><span data-stu-id="46dd2-144">AzureKeyVaultDnsSuffix</span></span>                   | <span data-ttu-id="46dd2-145">vault.microsoftazure.de</span><span class="sxs-lookup"><span data-stu-id="46dd2-145">vault.microsoftazure.de</span></span> |
| <span data-ttu-id="46dd2-146">AzureKeyVaultServiceEndpointResourceId</span><span class="sxs-lookup"><span data-stu-id="46dd2-146">AzureKeyVaultServiceEndpointResourceId</span></span>   | https://vault.microsoftazure.de |


## <a name="next-steps"></a><span data-ttu-id="46dd2-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="46dd2-147">Next steps</span></span>
<span data-ttu-id="46dd2-148">For more information about Azure Germany, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="46dd2-148">For more information about Azure Germany, see the following resources:</span></span>

* [<span data-ttu-id="46dd2-149">Sign up for a trial</span><span class="sxs-lookup"><span data-stu-id="46dd2-149">Sign up for a trial</span></span>](https://azure.microsoft.com/free/germany/)
* [<span data-ttu-id="46dd2-150">Acquiring Azure Germany</span><span class="sxs-lookup"><span data-stu-id="46dd2-150">Acquiring Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)
* <span data-ttu-id="46dd2-151">[Sign-in page](https://portal.microsoftazure.de/) if you already have an Azure Germany account</span><span class="sxs-lookup"><span data-stu-id="46dd2-151">[Sign-in page](https://portal.microsoftazure.de/) if you already have an Azure Germany account</span></span>
* [<span data-ttu-id="46dd2-152">Azure Germany overview</span><span class="sxs-lookup"><span data-stu-id="46dd2-152">Azure Germany overview</span></span>](./germany-welcome.md)
* [<span data-ttu-id="46dd2-153">Azure Germany blog</span><span class="sxs-lookup"><span data-stu-id="46dd2-153">Azure Germany blog</span></span>](http://blogs.msdn.microsoft.com/azuregermany/)
* [<span data-ttu-id="46dd2-154">Azure compliance</span><span class="sxs-lookup"><span data-stu-id="46dd2-154">Azure compliance</span></span>](https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings)

