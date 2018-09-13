---
title: Azure Government Web, Mobile and API | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: brendalee
manager: zakramer
ms.assetid: a1e173a9-996a-4091-a2e3-6b1e36da9ae1
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 12/5/2016
ms.author: brendal
ms.openlocfilehash: 28aa30cd1757e8b48e099920cb3c7f6ce2df1c25
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551978"
---
# <a name="azure-government-web--mobile"></a><span data-ttu-id="f0650-103">Azure Government Web + Mobile</span><span class="sxs-lookup"><span data-stu-id="f0650-103">Azure Government Web + Mobile</span></span>
## <a name="app-services"></a><span data-ttu-id="f0650-104">App Services</span><span class="sxs-lookup"><span data-stu-id="f0650-104">App Services</span></span>
### <a name="variations"></a><span data-ttu-id="f0650-105">Variations</span><span class="sxs-lookup"><span data-stu-id="f0650-105">Variations</span></span>
<span data-ttu-id="f0650-106">Azure App Services is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="f0650-106">Azure App Services is generally available in Azure Government.</span></span>

<span data-ttu-id="f0650-107">The Address for Azure App Service apps created in Azure Government is different from those created in the public cloud:</span><span class="sxs-lookup"><span data-stu-id="f0650-107">The Address for Azure App Service apps created in Azure Government is different from those created in the public cloud:</span></span>

| <span data-ttu-id="f0650-108">Service Type</span><span class="sxs-lookup"><span data-stu-id="f0650-108">Service Type</span></span> | <span data-ttu-id="f0650-109">Azure Public</span><span class="sxs-lookup"><span data-stu-id="f0650-109">Azure Public</span></span> | <span data-ttu-id="f0650-110">Azure Government</span><span class="sxs-lookup"><span data-stu-id="f0650-110">Azure Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f0650-111">App Service</span><span class="sxs-lookup"><span data-stu-id="f0650-111">App Service</span></span> |<span data-ttu-id="f0650-112">\*.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f0650-112">\*.azurewebsites.net</span></span> |<span data-ttu-id="f0650-113">\*.azurewebsites.us</span><span class="sxs-lookup"><span data-stu-id="f0650-113">\*.azurewebsites.us</span></span>|

<span data-ttu-id="f0650-114">Some App Service features available in the public cloud are not yet available in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="f0650-114">Some App Service features available in the public cloud are not yet available in Azure Government:</span></span>

- <span data-ttu-id="f0650-115">App Service Environments</span><span class="sxs-lookup"><span data-stu-id="f0650-115">App Service Environments</span></span>
- <span data-ttu-id="f0650-116">App deployment</span><span class="sxs-lookup"><span data-stu-id="f0650-116">App deployment</span></span>
    - <span data-ttu-id="f0650-117">Continuous Delivery(preview)</span><span class="sxs-lookup"><span data-stu-id="f0650-117">Continuous Delivery(preview)</span></span>
- <span data-ttu-id="f0650-118">Settings</span><span class="sxs-lookup"><span data-stu-id="f0650-118">Settings</span></span>
    - <span data-ttu-id="f0650-119">vNet integration and Hybrid connections</span><span class="sxs-lookup"><span data-stu-id="f0650-119">vNet integration and Hybrid connections</span></span>
    - <span data-ttu-id="f0650-120">Security scanning</span><span class="sxs-lookup"><span data-stu-id="f0650-120">Security scanning</span></span>
- <span data-ttu-id="f0650-121">Development Tools</span><span class="sxs-lookup"><span data-stu-id="f0650-121">Development Tools</span></span>
    - <span data-ttu-id="f0650-122">Performance test</span><span class="sxs-lookup"><span data-stu-id="f0650-122">Performance test</span></span>
    - <span data-ttu-id="f0650-123">Resource explorer</span><span class="sxs-lookup"><span data-stu-id="f0650-123">Resource explorer</span></span>
    - <span data-ttu-id="f0650-124">PHP Debugging</span><span class="sxs-lookup"><span data-stu-id="f0650-124">PHP Debugging</span></span>
- <span data-ttu-id="f0650-125">Monitoring</span><span class="sxs-lookup"><span data-stu-id="f0650-125">Monitoring</span></span>
    - <span data-ttu-id="f0650-126">Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0650-126">Application Insights</span></span>
    - <span data-ttu-id="f0650-127">Metrics per instance</span><span class="sxs-lookup"><span data-stu-id="f0650-127">Metrics per instance</span></span>
    - <span data-ttu-id="f0650-128">Live HTTP traffic</span><span class="sxs-lookup"><span data-stu-id="f0650-128">Live HTTP traffic</span></span>
    - <span data-ttu-id="f0650-129">Application events</span><span class="sxs-lookup"><span data-stu-id="f0650-129">Application events</span></span>
    - <span data-ttu-id="f0650-130">FREB logs</span><span class="sxs-lookup"><span data-stu-id="f0650-130">FREB logs</span></span>
- <span data-ttu-id="f0650-131">Support & Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f0650-131">Support & Troubleshooting</span></span>
    - <span data-ttu-id="f0650-132">App Service Advisor</span><span class="sxs-lookup"><span data-stu-id="f0650-132">App Service Advisor</span></span>
    - <span data-ttu-id="f0650-133">Failure History</span><span class="sxs-lookup"><span data-stu-id="f0650-133">Failure History</span></span>
    - <span data-ttu-id="f0650-134">Diagnostics as a Service</span><span class="sxs-lookup"><span data-stu-id="f0650-134">Diagnostics as a Service</span></span>
    - <span data-ttu-id="f0650-135">Mitigate</span><span class="sxs-lookup"><span data-stu-id="f0650-135">Mitigate</span></span>


### <a name="considerations"></a><span data-ttu-id="f0650-136">Considerations</span><span class="sxs-lookup"><span data-stu-id="f0650-136">Considerations</span></span>
<span data-ttu-id="f0650-137">The following information identifies the Azure Government boundary for App Service:</span><span class="sxs-lookup"><span data-stu-id="f0650-137">The following information identifies the Azure Government boundary for App Service:</span></span>

| <span data-ttu-id="f0650-138">Regulated/controlled data permitted</span><span class="sxs-lookup"><span data-stu-id="f0650-138">Regulated/controlled data permitted</span></span> | <span data-ttu-id="f0650-139">Regulated/controlled data not permitted</span><span class="sxs-lookup"><span data-stu-id="f0650-139">Regulated/controlled data not permitted</span></span> |
| --- | --- |
| <span data-ttu-id="f0650-140">Data entered, stored, and processed within Azure App Service can contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="f0650-140">Data entered, stored, and processed within Azure App Service can contain export controlled data.</span></span> <span data-ttu-id="f0650-141">Binaries running within Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f0650-141">Binaries running within Azure App Service.</span></span> <span data-ttu-id="f0650-142">Static authenticators, such as passwords and smartcard PINs for access to Azure platform components.</span><span class="sxs-lookup"><span data-stu-id="f0650-142">Static authenticators, such as passwords and smartcard PINs for access to Azure platform components.</span></span> <span data-ttu-id="f0650-143">Private keys of certificates used to manage Azure platform components.</span><span class="sxs-lookup"><span data-stu-id="f0650-143">Private keys of certificates used to manage Azure platform components.</span></span> <span data-ttu-id="f0650-144">SQL connection strings.</span><span class="sxs-lookup"><span data-stu-id="f0650-144">SQL connection strings.</span></span> <span data-ttu-id="f0650-145">Other security information/secrets, such as certificates, encryption keys, master keys, and storage keys stored in Azure services.</span><span class="sxs-lookup"><span data-stu-id="f0650-145">Other security information/secrets, such as certificates, encryption keys, master keys, and storage keys stored in Azure services.</span></span> |<span data-ttu-id="f0650-146">Metadata is not permitted to contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="f0650-146">Metadata is not permitted to contain export controlled data.</span></span> <span data-ttu-id="f0650-147">This metadata includes all configuration data entered when creating and maintaining your Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f0650-147">This metadata includes all configuration data entered when creating and maintaining your Azure App Service.</span></span> <span data-ttu-id="f0650-148">Do not enter Regulated/controlled data into the following fields: Resource groups, Resource names, Resource tags</span><span class="sxs-lookup"><span data-stu-id="f0650-148">Do not enter Regulated/controlled data into the following fields: Resource groups, Resource names, Resource tags</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f0650-149">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f0650-149">Next Steps</span></span>
<span data-ttu-id="f0650-150">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog.](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="f0650-150">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog.](https://blogs.msdn.microsoft.com/azuregov/)</span></span>

