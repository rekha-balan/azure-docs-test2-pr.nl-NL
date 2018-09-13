---
title: Common cloud service management tasks | Microsoft Docs
description: Learn how to manage cloud services in the Azure portal. These examples use the Azure portal.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/27/2016
ms.author: adegeo
ms.openlocfilehash: ed491a981a9d2abe71e5d94a699eca0893ee8eae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563008"
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="53e05-104">How to Manage Cloud Services</span><span class="sxs-lookup"><span data-stu-id="53e05-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-manage-portal.md)
> * [Azure classic portal](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="53e05-107">Your cloud service is managed in the **Cloud Services (classic)** area of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="53e05-107">Your cloud service is managed in the **Cloud Services (classic)** area of the Azure portal.</span></span> <span data-ttu-id="53e05-108">This article describes some common actions you would take while managing your cloud services.</span><span class="sxs-lookup"><span data-stu-id="53e05-108">This article describes some common actions you would take while managing your cloud services.</span></span> <span data-ttu-id="53e05-109">Which includes updating, deleting, scaling, and promoting a staged deployment to production.</span><span class="sxs-lookup"><span data-stu-id="53e05-109">Which includes updating, deleting, scaling, and promoting a staged deployment to production.</span></span>

<span data-ttu-id="53e05-110">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53e05-110">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="53e05-111">How to: Update a cloud service role or deployment</span><span class="sxs-lookup"><span data-stu-id="53e05-111">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="53e05-112">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span><span class="sxs-lookup"><span data-stu-id="53e05-112">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="53e05-113">You can update a single role or all roles.</span><span class="sxs-lookup"><span data-stu-id="53e05-113">You can update a single role or all roles.</span></span> <span data-ttu-id="53e05-114">To update, you can upload a new service package or service configuration file.</span><span class="sxs-lookup"><span data-stu-id="53e05-114">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="53e05-115">In the [Azure portal][Azure portal], select the cloud service you want to update.</span><span class="sxs-lookup"><span data-stu-id="53e05-115">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="53e05-116">This step opens the cloud service instance blade.</span><span class="sxs-lookup"><span data-stu-id="53e05-116">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="53e05-117">In the blade, click the **Update** button.</span><span class="sxs-lookup"><span data-stu-id="53e05-117">In the blade, click the **Update** button.</span></span>

    ![Update Button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="53e05-119">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="53e05-119">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="53e05-121">**Optionally** update the deployment label and the storage account.</span><span class="sxs-lookup"><span data-stu-id="53e05-121">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="53e05-122">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span><span class="sxs-lookup"><span data-stu-id="53e05-122">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="53e05-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="53e05-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="53e05-124">With two role instances, one virtual machine will process client requests while the other is updated.</span><span class="sxs-lookup"><span data-stu-id="53e05-124">With two role instances, one virtual machine will process client requests while the other is updated.</span></span>

6. <span data-ttu-id="53e05-125">Check **Start deployment** to have the update applied after the upload of the package has finished.</span><span class="sxs-lookup"><span data-stu-id="53e05-125">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="53e05-126">Click **OK** to begin updating the service.</span><span class="sxs-lookup"><span data-stu-id="53e05-126">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="53e05-127">How to: Swap deployments to promote a staged deployment to production</span><span class="sxs-lookup"><span data-stu-id="53e05-127">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="53e05-128">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span><span class="sxs-lookup"><span data-stu-id="53e05-128">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="53e05-129">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span><span class="sxs-lookup"><span data-stu-id="53e05-129">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="53e05-130">You can swap deployments from the **Cloud Services** page or the dashboard.</span><span class="sxs-lookup"><span data-stu-id="53e05-130">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="53e05-131">In the [Azure portal][Azure portal], select the cloud service you want to update.</span><span class="sxs-lookup"><span data-stu-id="53e05-131">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="53e05-132">This step opens the cloud service instance blade.</span><span class="sxs-lookup"><span data-stu-id="53e05-132">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="53e05-133">In the blade, click the **Swap** button.</span><span class="sxs-lookup"><span data-stu-id="53e05-133">In the blade, click the **Swap** button.</span></span>

    ![Cloud Services Swap](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="53e05-135">The following confirmation prompt opens.</span><span class="sxs-lookup"><span data-stu-id="53e05-135">The following confirmation prompt opens.</span></span>

    ![Cloud Services Swap](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="53e05-137">After you verify the deployment information, click **OK** to swap the deployments.</span><span class="sxs-lookup"><span data-stu-id="53e05-137">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="53e05-138">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span><span class="sxs-lookup"><span data-stu-id="53e05-138">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="53e05-139">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span><span class="sxs-lookup"><span data-stu-id="53e05-139">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="53e05-140">Common questions about swapping deployments</span><span class="sxs-lookup"><span data-stu-id="53e05-140">Common questions about swapping deployments</span></span>

<span data-ttu-id="53e05-141">**What are the prerequisites for swapping deployments?**</span><span class="sxs-lookup"><span data-stu-id="53e05-141">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="53e05-142">There are two key prerequisites for a successful deployment swap:</span><span class="sxs-lookup"><span data-stu-id="53e05-142">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="53e05-143">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span><span class="sxs-lookup"><span data-stu-id="53e05-143">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="53e05-144">Otherwise, the swap will fail.</span><span class="sxs-lookup"><span data-stu-id="53e05-144">Otherwise, the swap will fail.</span></span>

- <span data-ttu-id="53e05-145">All instances of your roles must be running before you can perform the swap.</span><span class="sxs-lookup"><span data-stu-id="53e05-145">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="53e05-146">You can check the status of your instances in the overview blade of the Azure portal or by using [the Get-AzureRole command in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/servicemanagement/azure.service/v3.1.0/get-azurerole).</span><span class="sxs-lookup"><span data-stu-id="53e05-146">You can check the status of your instances in the overview blade of the Azure portal or by using [the Get-AzureRole command in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/servicemanagement/azure.service/v3.1.0/get-azurerole).</span></span>

<span data-ttu-id="53e05-147">Note that guest OS updates and service healing operations can also cause deployment swaps to fail.</span><span class="sxs-lookup"><span data-stu-id="53e05-147">Note that guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="53e05-148">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="53e05-148">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span></span>

<span data-ttu-id="53e05-149">**Does a swap incur downtime for my application? How should I handle it?**</span><span class="sxs-lookup"><span data-stu-id="53e05-149">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="53e05-150">As described in the last section, a deployment swap is typically very fast since it is just a configuration change in the Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="53e05-150">As described in the last section, a deployment swap is typically very fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="53e05-151">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span><span class="sxs-lookup"><span data-stu-id="53e05-151">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="53e05-152">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="53e05-152">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="53e05-153">How to: Link a resource to a cloud service</span><span class="sxs-lookup"><span data-stu-id="53e05-153">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="53e05-154">The Azure portal does not link resources together like the current Azure classic portal does.</span><span class="sxs-lookup"><span data-stu-id="53e05-154">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="53e05-155">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="53e05-155">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="53e05-156">How to: Delete deployments and a cloud service</span><span class="sxs-lookup"><span data-stu-id="53e05-156">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="53e05-157">Before you can delete a cloud service, you must delete each existing deployment.</span><span class="sxs-lookup"><span data-stu-id="53e05-157">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="53e05-158">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span><span class="sxs-lookup"><span data-stu-id="53e05-158">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="53e05-159">You are billed for compute costs for deployed role instances that are stopped.</span><span class="sxs-lookup"><span data-stu-id="53e05-159">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="53e05-160">Use the following procedure to delete a deployment or your cloud service.</span><span class="sxs-lookup"><span data-stu-id="53e05-160">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="53e05-161">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span><span class="sxs-lookup"><span data-stu-id="53e05-161">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="53e05-162">This step opens the cloud service instance blade.</span><span class="sxs-lookup"><span data-stu-id="53e05-162">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="53e05-163">In the blade, click the **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="53e05-163">In the blade, click the **Delete** button.</span></span>

    ![Cloud Services Swap](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="53e05-165">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span><span class="sxs-lookup"><span data-stu-id="53e05-165">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Cloud Services Swap](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="53e05-167">Click the **Delete** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="53e05-167">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="53e05-168">To delete the cloud service, click **Delete cloud service**.</span><span class="sxs-lookup"><span data-stu-id="53e05-168">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="53e05-169">Then, at the confirmation prompt, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="53e05-169">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account. For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.
>
>

[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="53e05-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="53e05-172">Next steps</span></span>
* <span data-ttu-id="53e05-173">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53e05-173">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="53e05-174">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53e05-174">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="53e05-175">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53e05-175">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="53e05-176">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53e05-176">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>






