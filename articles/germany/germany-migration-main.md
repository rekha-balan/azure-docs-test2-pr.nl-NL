---
title: Migration from Azure Germany to global Azure
description: Main intro to migration from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 750f58f825071e9b84b4fa40404088544af72f15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866344"
---
# <a name="introduction-to-migration-guidance-for-azure-germany"></a><span data-ttu-id="ac8e9-103">Introduction to migration guidance for Azure Germany</span><span class="sxs-lookup"><span data-stu-id="ac8e9-103">Introduction to migration guidance for Azure Germany</span></span>

<span data-ttu-id="ac8e9-104">These articles provide guidance to migrate your workloads from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-104">These articles provide guidance to migrate your workloads from Azure Germany to global Azure.</span></span> <span data-ttu-id="ac8e9-105">Although Azure provides tools to migrate resources at the [Azure Migration Center](https://azure.microsoft.com/migration/), some of these tools are designed only for migrations inside the same tenant or the same region.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-105">Although Azure provides tools to migrate resources at the [Azure Migration Center](https://azure.microsoft.com/migration/), some of these tools are designed only for migrations inside the same tenant or the same region.</span></span>

<span data-ttu-id="ac8e9-106">The two regions in Germany are strictly separated from global Azure, including separate Azure Active Directory for each cloud.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-106">The two regions in Germany are strictly separated from global Azure, including separate Azure Active Directory for each cloud.</span></span> <span data-ttu-id="ac8e9-107">As a result, Azure tenants are always different between global Azure and Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-107">As a result, Azure tenants are always different between global Azure and Azure Germany.</span></span> <span data-ttu-id="ac8e9-108">Some of the standard migration tools are based on moving resources inside the *same* tenant.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-108">Some of the standard migration tools are based on moving resources inside the *same* tenant.</span></span> <span data-ttu-id="ac8e9-109">When migrating between *different* tenants, below is a list of tools available.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-109">When migrating between *different* tenants, below is a list of tools available.</span></span>

## <a name="migration-process"></a><span data-ttu-id="ac8e9-110">Migration Process</span><span class="sxs-lookup"><span data-stu-id="ac8e9-110">Migration Process</span></span>

<span data-ttu-id="ac8e9-111">Your journey to migrate workload from Azure Germany to global Azure will typically follow similar processes used for migrating applications to the Cloud.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-111">Your journey to migrate workload from Azure Germany to global Azure will typically follow similar processes used for migrating applications to the Cloud.</span></span>

![Assess -> Plan -> Migrate -> Validate](./media/germany-migration-main/migration-steps.png)

### <a name="assess"></a><span data-ttu-id="ac8e9-113">Assess</span><span class="sxs-lookup"><span data-stu-id="ac8e9-113">Assess</span></span>

- <span data-ttu-id="ac8e9-114">Understand your organizationAzure Germany footprint by bringing together Azure Account owners, Subscription admins, Tenant admins, and Finance/Accounting teams.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-114">Understand your organizationAzure Germany footprint by bringing together Azure Account owners, Subscription admins, Tenant admins, and Finance/Accounting teams.</span></span> <span data-ttu-id="ac8e9-115">Together, they'll provide a complete picture of Azure usage for large organizations.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-115">Together, they'll provide a complete picture of Azure usage for large organizations.</span></span>

- <span data-ttu-id="ac8e9-116">Compile inventory of resources</span><span class="sxs-lookup"><span data-stu-id="ac8e9-116">Compile inventory of resources</span></span>
  - <span data-ttu-id="ac8e9-117">Each Subscription Admin and Tenant admin will execute a series of scripts to list resource groups, the resources within each of the groups, and their deployment settings</span><span class="sxs-lookup"><span data-stu-id="ac8e9-117">Each Subscription Admin and Tenant admin will execute a series of scripts to list resource groups, the resources within each of the groups, and their deployment settings</span></span>
  - <span data-ttu-id="ac8e9-118">Document dependencies across applications within Azure, and with external systems</span><span class="sxs-lookup"><span data-stu-id="ac8e9-118">Document dependencies across applications within Azure, and with external systems</span></span>
  - <span data-ttu-id="ac8e9-119">Document the count of each Azure resource, and the amount of data associated with each instance that needs to be migrated</span><span class="sxs-lookup"><span data-stu-id="ac8e9-119">Document the count of each Azure resource, and the amount of data associated with each instance that needs to be migrated</span></span>
  - <span data-ttu-id="ac8e9-120">Ensure the application architecture documents are consistent with the Azure resources list</span><span class="sxs-lookup"><span data-stu-id="ac8e9-120">Ensure the application architecture documents are consistent with the Azure resources list</span></span>

<span data-ttu-id="ac8e9-121">At the end of this stage, you'll have</span><span class="sxs-lookup"><span data-stu-id="ac8e9-121">At the end of this stage, you'll have</span></span>

- <span data-ttu-id="ac8e9-122">a complete list of Azure resources in use,</span><span class="sxs-lookup"><span data-stu-id="ac8e9-122">a complete list of Azure resources in use,</span></span>
- <span data-ttu-id="ac8e9-123">dependencies across those resources, and</span><span class="sxs-lookup"><span data-stu-id="ac8e9-123">dependencies across those resources, and</span></span>
- <span data-ttu-id="ac8e9-124">complexity of migration effort</span><span class="sxs-lookup"><span data-stu-id="ac8e9-124">complexity of migration effort</span></span>

### <a name="plan"></a><span data-ttu-id="ac8e9-125">Plan</span><span class="sxs-lookup"><span data-stu-id="ac8e9-125">Plan</span></span>

- <span data-ttu-id="ac8e9-126">Use the output of the dependency analysis from Assessment stage to define related components.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-126">Use the output of the dependency analysis from Assessment stage to define related components.</span></span> <span data-ttu-id="ac8e9-127">Consider migrating them together in a '**migration package**'</span><span class="sxs-lookup"><span data-stu-id="ac8e9-127">Consider migrating them together in a '**migration package**'</span></span>
- <span data-ttu-id="ac8e9-128">[Optional] Take this migration opportunity to apply [Gartner 5-R criteria](https://www.gartner.com/newsroom/id/1684114), and optimize your workload</span><span class="sxs-lookup"><span data-stu-id="ac8e9-128">[Optional] Take this migration opportunity to apply [Gartner 5-R criteria](https://www.gartner.com/newsroom/id/1684114), and optimize your workload</span></span>
- <span data-ttu-id="ac8e9-129">Determine Target environment in global Azure</span><span class="sxs-lookup"><span data-stu-id="ac8e9-129">Determine Target environment in global Azure</span></span>
  - <span data-ttu-id="ac8e9-130">Identify the target global Azure tenant (if your organization doesn't already have a presence, create one)</span><span class="sxs-lookup"><span data-stu-id="ac8e9-130">Identify the target global Azure tenant (if your organization doesn't already have a presence, create one)</span></span> 
  - <span data-ttu-id="ac8e9-131">create subscriptions</span><span class="sxs-lookup"><span data-stu-id="ac8e9-131">create subscriptions</span></span>
  - <span data-ttu-id="ac8e9-132">choose which global Azure location you prefer to migrate</span><span class="sxs-lookup"><span data-stu-id="ac8e9-132">choose which global Azure location you prefer to migrate</span></span>
  - <span data-ttu-id="ac8e9-133">Execute test migration scenarios that match your architecture from Azure Germany to Azure global</span><span class="sxs-lookup"><span data-stu-id="ac8e9-133">Execute test migration scenarios that match your architecture from Azure Germany to Azure global</span></span>
- <span data-ttu-id="ac8e9-134">Determine appropriate timeline/schedule of migration, and User acceptance test plan, for each migration package</span><span class="sxs-lookup"><span data-stu-id="ac8e9-134">Determine appropriate timeline/schedule of migration, and User acceptance test plan, for each migration package</span></span>

### <a name="migrate"></a><span data-ttu-id="ac8e9-135">Migrate</span><span class="sxs-lookup"><span data-stu-id="ac8e9-135">Migrate</span></span>

- <span data-ttu-id="ac8e9-136">Use the tools, techniques, and recommendations in this document to create new resources in Azure global, and configure applications</span><span class="sxs-lookup"><span data-stu-id="ac8e9-136">Use the tools, techniques, and recommendations in this document to create new resources in Azure global, and configure applications</span></span>

### <a name="validate"></a><span data-ttu-id="ac8e9-137">Validate</span><span class="sxs-lookup"><span data-stu-id="ac8e9-137">Validate</span></span>

- <span data-ttu-id="ac8e9-138">Perform User acceptance testing</span><span class="sxs-lookup"><span data-stu-id="ac8e9-138">Perform User acceptance testing</span></span>
- <span data-ttu-id="ac8e9-139">Ensure applications are working as expected</span><span class="sxs-lookup"><span data-stu-id="ac8e9-139">Ensure applications are working as expected</span></span>
- <span data-ttu-id="ac8e9-140">Synchronize latest data to target environment if applicable</span><span class="sxs-lookup"><span data-stu-id="ac8e9-140">Synchronize latest data to target environment if applicable</span></span>
- <span data-ttu-id="ac8e9-141">Cutover to new application instance in Azure global</span><span class="sxs-lookup"><span data-stu-id="ac8e9-141">Cutover to new application instance in Azure global</span></span>
- <span data-ttu-id="ac8e9-142">confirm production environment is working as expected</span><span class="sxs-lookup"><span data-stu-id="ac8e9-142">confirm production environment is working as expected</span></span>
- <span data-ttu-id="ac8e9-143">Decommission resources in Azure Germany</span><span class="sxs-lookup"><span data-stu-id="ac8e9-143">Decommission resources in Azure Germany</span></span>

## <a name="terms"></a><span data-ttu-id="ac8e9-144">Terms</span><span class="sxs-lookup"><span data-stu-id="ac8e9-144">Terms</span></span>

<span data-ttu-id="ac8e9-145">These terms are used in the following migration articles:</span><span class="sxs-lookup"><span data-stu-id="ac8e9-145">These terms are used in the following migration articles:</span></span>

<span data-ttu-id="ac8e9-146">*Source* describes where you come from (for example Azure Germany):</span><span class="sxs-lookup"><span data-stu-id="ac8e9-146">*Source* describes where you come from (for example Azure Germany):</span></span>

- <span data-ttu-id="ac8e9-147">Source tenant name: Name of the Tenant in Azure Germany (everything after the "@" in the account name).</span><span class="sxs-lookup"><span data-stu-id="ac8e9-147">Source tenant name: Name of the Tenant in Azure Germany (everything after the "@" in the account name).</span></span> <span data-ttu-id="ac8e9-148">Tenant names in Azure Germany are all ending on *microsoftazure.de*.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-148">Tenant names in Azure Germany are all ending on *microsoftazure.de*.</span></span>
- <span data-ttu-id="ac8e9-149">Source tenant ID: The ID of the tenant in Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-149">Source tenant ID: The ID of the tenant in Azure Germany.</span></span> <span data-ttu-id="ac8e9-150">The tenant ID shows up in the Azure portal when moving the mouse over the account name at the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-150">The tenant ID shows up in the Azure portal when moving the mouse over the account name at the upper right corner.</span></span>
- <span data-ttu-id="ac8e9-151">Source subscription ID: You can have more than one subscription under the same tenant.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-151">Source subscription ID: You can have more than one subscription under the same tenant.</span></span> <span data-ttu-id="ac8e9-152">Always make sure that you're using the correct subscription.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-152">Always make sure that you're using the correct subscription.</span></span>
- <span data-ttu-id="ac8e9-153">Source region: Either "**Germany Central**" ("**germanycentral**") or "**Germany Northeast**" ("**germanynortheast**"), depending on where the resource you want to migrate is located.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-153">Source region: Either "**Germany Central**" ("**germanycentral**") or "**Germany Northeast**" ("**germanynortheast**"), depending on where the resource you want to migrate is located.</span></span>

<span data-ttu-id="ac8e9-154">*Target* or *Destination* describes where you migrate to:</span><span class="sxs-lookup"><span data-stu-id="ac8e9-154">*Target* or *Destination* describes where you migrate to:</span></span>

- <span data-ttu-id="ac8e9-155">Target tenant name: Like Source tenant name, but in Azure public.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-155">Target tenant name: Like Source tenant name, but in Azure public.</span></span>
- <span data-ttu-id="ac8e9-156">Target tenant ID: Like Source tenant ID.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-156">Target tenant ID: Like Source tenant ID.</span></span>
- <span data-ttu-id="ac8e9-157">Target subscription ID: Like source subscription ID</span><span class="sxs-lookup"><span data-stu-id="ac8e9-157">Target subscription ID: Like source subscription ID</span></span>
- <span data-ttu-id="ac8e9-158">Target region: You can use nearly any region in global Azure, but most likely you want to migrate to "**West Europe**" ("**westeurope**") or "**North Europe**" ("**northeurope**").</span><span class="sxs-lookup"><span data-stu-id="ac8e9-158">Target region: You can use nearly any region in global Azure, but most likely you want to migrate to "**West Europe**" ("**westeurope**") or "**North Europe**" ("**northeurope**").</span></span>

> [!NOTE]
> <span data-ttu-id="ac8e9-159">Please verify that the service you are migrating is offered in the target region.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-159">Please verify that the service you are migrating is offered in the target region.</span></span> <span data-ttu-id="ac8e9-160">All Azure services available in Azure Germany are available in **West Europe**.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-160">All Azure services available in Azure Germany are available in **West Europe**.</span></span> <span data-ttu-id="ac8e9-161">All Azure services available in Azure Germany are also available in **North Europe**, except for G/GS VM series and Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-161">All Azure services available in Azure Germany are also available in **North Europe**, except for G/GS VM series and Machine Learning Studio.</span></span>

<span data-ttu-id="ac8e9-162">Also add the global Azure portal to your favorite links in your browser.</span><span class="sxs-lookup"><span data-stu-id="ac8e9-162">Also add the global Azure portal to your favorite links in your browser.</span></span> <span data-ttu-id="ac8e9-163">While Azure Germany portal is available under [https://portal.microsoftazure.de/](https://portal.microsoftazure.de/), the global Azure portal can be reached under [https://portal.azure.com/](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ac8e9-163">While Azure Germany portal is available under [https://portal.microsoftazure.de/](https://portal.microsoftazure.de/), the global Azure portal can be reached under [https://portal.azure.com/](https://portal.azure.com/).</span></span>

### <a name="next-steps"></a><span data-ttu-id="ac8e9-164">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ac8e9-164">Next Steps</span></span>

<span data-ttu-id="ac8e9-165">Learn about tools, techniques, and recommendations to migrate resources of the following service categories:</span><span class="sxs-lookup"><span data-stu-id="ac8e9-165">Learn about tools, techniques, and recommendations to migrate resources of the following service categories:</span></span>

- [<span data-ttu-id="ac8e9-166">Compute</span><span class="sxs-lookup"><span data-stu-id="ac8e9-166">Compute</span></span>](./germany-migration-compute.md)
- [<span data-ttu-id="ac8e9-167">Networking</span><span class="sxs-lookup"><span data-stu-id="ac8e9-167">Networking</span></span>](./germany-migration-networking.md)
- [<span data-ttu-id="ac8e9-168">Storage</span><span class="sxs-lookup"><span data-stu-id="ac8e9-168">Storage</span></span>](./germany-migration-storage.md)
- [<span data-ttu-id="ac8e9-169">Web</span><span class="sxs-lookup"><span data-stu-id="ac8e9-169">Web</span></span>](./germany-migration-web.md)
- [<span data-ttu-id="ac8e9-170">Databases</span><span class="sxs-lookup"><span data-stu-id="ac8e9-170">Databases</span></span>](./germany-migration-databases.md)
- [<span data-ttu-id="ac8e9-171">Analytics</span><span class="sxs-lookup"><span data-stu-id="ac8e9-171">Analytics</span></span>](./germany-migration-analytics.md)
- [<span data-ttu-id="ac8e9-172">Internet of Things (IoT)</span><span class="sxs-lookup"><span data-stu-id="ac8e9-172">Internet of Things (IoT)</span></span>](./germany-migration-iot.md)
- [<span data-ttu-id="ac8e9-173">Integration</span><span class="sxs-lookup"><span data-stu-id="ac8e9-173">Integration</span></span>](./germany-migration-integration.md)
- [<span data-ttu-id="ac8e9-174">Identity</span><span class="sxs-lookup"><span data-stu-id="ac8e9-174">Identity</span></span>](./germany-migration-identity.md)
- [<span data-ttu-id="ac8e9-175">Security</span><span class="sxs-lookup"><span data-stu-id="ac8e9-175">Security</span></span>](./germany-migration-security.md)
- [<span data-ttu-id="ac8e9-176">Management Tools</span><span class="sxs-lookup"><span data-stu-id="ac8e9-176">Management Tools</span></span>](./germany-migration-management-tools.md)
- [<span data-ttu-id="ac8e9-177">Media</span><span class="sxs-lookup"><span data-stu-id="ac8e9-177">Media</span></span>](./germany-migration-media.md)
