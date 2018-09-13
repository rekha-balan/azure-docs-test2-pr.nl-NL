---
title: Common cloud service management tasks (classic) | Microsoft Docs
description: Learn how to manage cloud services in the Azure classic portal.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/27/2016
ms.author: adegeo
ms.openlocfilehash: f9eb3a5762611168de0c702dc435bcf4004a0572
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563149"
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="e45fb-103">How to Manage Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e45fb-103">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-manage-portal.md)
> * [Azure classic portal](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="e45fb-106">In the **Cloud Services** area of the Azure classic portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span><span class="sxs-lookup"><span data-stu-id="e45fb-106">In the **Cloud Services** area of the Azure classic portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="e45fb-107">How to: Update a cloud service role or deployment</span><span class="sxs-lookup"><span data-stu-id="e45fb-107">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="e45fb-108">If you need to update the application code for your cloud service, use **Update** on the dashboard, **Cloud Services** page, or **Instances** page.</span><span class="sxs-lookup"><span data-stu-id="e45fb-108">If you need to update the application code for your cloud service, use **Update** on the dashboard, **Cloud Services** page, or **Instances** page.</span></span> <span data-ttu-id="e45fb-109">You can update a single role or all roles.</span><span class="sxs-lookup"><span data-stu-id="e45fb-109">You can update a single role or all roles.</span></span> <span data-ttu-id="e45fb-110">You'll need to upload a new service package and service configuration file.</span><span class="sxs-lookup"><span data-stu-id="e45fb-110">You'll need to upload a new service package and service configuration file.</span></span>

1. <span data-ttu-id="e45fb-111">In the [Azure classic portal](https://manage.windowsazure.com/), on the dashboard, **Cloud Services** page, or **Instances** page, click **Update**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-111">In the [Azure classic portal](https://manage.windowsazure.com/), on the dashboard, **Cloud Services** page, or **Instances** page, click **Update**.</span></span>

    ![UpdateDeployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. <span data-ttu-id="e45fb-113">In **Deployment label**, enter a name to identify the deployment (for example, mycloudservice4).</span><span class="sxs-lookup"><span data-stu-id="e45fb-113">In **Deployment label**, enter a name to identify the deployment (for example, mycloudservice4).</span></span> <span data-ttu-id="e45fb-114">You'll find the deployment label under **quick start** on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-114">You'll find the deployment label under **quick start** on the dashboard.</span></span>
3. <span data-ttu-id="e45fb-115">In **Package**, use **Browse** to upload the service package file (.cspkg).</span><span class="sxs-lookup"><span data-stu-id="e45fb-115">In **Package**, use **Browse** to upload the service package file (.cspkg).</span></span>
4. <span data-ttu-id="e45fb-116">In **Configuration**, use **Browse** to upload the service configuration file (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="e45fb-116">In **Configuration**, use **Browse** to upload the service configuration file (.cscfg).</span></span>
5. <span data-ttu-id="e45fb-117">In **Role**, select **All** if you want to upgrade all roles in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-117">In **Role**, select **All** if you want to upgrade all roles in the cloud service.</span></span> <span data-ttu-id="e45fb-118">To perform a single role update, select the role you want to update.</span><span class="sxs-lookup"><span data-stu-id="e45fb-118">To perform a single role update, select the role you want to update.</span></span> <span data-ttu-id="e45fb-119">Even if you select a specific role to update, the updates in the service configuration file are applied to all roles.</span><span class="sxs-lookup"><span data-stu-id="e45fb-119">Even if you select a specific role to update, the updates in the service configuration file are applied to all roles.</span></span>
6. <span data-ttu-id="e45fb-120">If the update changes the number of roles or the size of any role, select the **Allow update if role sizes or number of roles changes** check box to enable the update to proceed.</span><span class="sxs-lookup"><span data-stu-id="e45fb-120">If the update changes the number of roles or the size of any role, select the **Allow update if role sizes or number of roles changes** check box to enable the update to proceed.</span></span>

    <span data-ttu-id="e45fb-121">Be aware that if you change the size of a role (that is, the size of a virtual machine that hosts a role instance) or the number of roles, each role instance (virtual machine) must be re-imaged, and any local data will be lost.</span><span class="sxs-lookup"><span data-stu-id="e45fb-121">Be aware that if you change the size of a role (that is, the size of a virtual machine that hosts a role instance) or the number of roles, each role instance (virtual machine) must be re-imaged, and any local data will be lost.</span></span>

7. <span data-ttu-id="e45fb-122">If any service roles have only one role instance, select the **Update even if one or more role contain a single instance check box** to enable the upgrade to proceed.</span><span class="sxs-lookup"><span data-stu-id="e45fb-122">If any service roles have only one role instance, select the **Update even if one or more role contain a single instance check box** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="e45fb-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="e45fb-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="e45fb-124">That enables one virtual machine to process client requests while the other is being updated.</span><span class="sxs-lookup"><span data-stu-id="e45fb-124">That enables one virtual machine to process client requests while the other is being updated.</span></span>

8. <span data-ttu-id="e45fb-125">Click **OK** (checkmark) to begin updating the service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-125">Click **OK** (checkmark) to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="e45fb-126">How to: Swap deployments to promote a staged deployment to production</span><span class="sxs-lookup"><span data-stu-id="e45fb-126">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="e45fb-127">Use **Swap** to promote a staging deployment of a cloud service to production.</span><span class="sxs-lookup"><span data-stu-id="e45fb-127">Use **Swap** to promote a staging deployment of a cloud service to production.</span></span> <span data-ttu-id="e45fb-128">When you decide to deploy a new release of a cloud service, you can stage and test your new release in your cloud service staging environment while your customers are using the current release in production.</span><span class="sxs-lookup"><span data-stu-id="e45fb-128">When you decide to deploy a new release of a cloud service, you can stage and test your new release in your cloud service staging environment while your customers are using the current release in production.</span></span> <span data-ttu-id="e45fb-129">When you're ready to promote the new release to production, you can use **Swap** to switch the URLs by which the two deployments are addressed.</span><span class="sxs-lookup"><span data-stu-id="e45fb-129">When you're ready to promote the new release to production, you can use **Swap** to switch the URLs by which the two deployments are addressed.</span></span>

<span data-ttu-id="e45fb-130">You can swap deployments from the **Cloud Services** page or the dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-130">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="e45fb-131">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-131">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="e45fb-132">In the list of cloud services, click the cloud service to select it.</span><span class="sxs-lookup"><span data-stu-id="e45fb-132">In the list of cloud services, click the cloud service to select it.</span></span>
3. <span data-ttu-id="e45fb-133">Click **Swap**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-133">Click **Swap**.</span></span>

    <span data-ttu-id="e45fb-134">The following confirmation prompt opens.</span><span class="sxs-lookup"><span data-stu-id="e45fb-134">The following confirmation prompt opens.</span></span>

    ![Cloud Services Swap](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. <span data-ttu-id="e45fb-136">After you verify the deployment information, click **Yes** to swap the deployments.</span><span class="sxs-lookup"><span data-stu-id="e45fb-136">After you verify the deployment information, click **Yes** to swap the deployments.</span></span>

    <span data-ttu-id="e45fb-137">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span><span class="sxs-lookup"><span data-stu-id="e45fb-137">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="e45fb-138">To save compute costs, you can delete the deployment in the staging environment when you're sure the new production deployment is performing as expected.</span><span class="sxs-lookup"><span data-stu-id="e45fb-138">To save compute costs, you can delete the deployment in the staging environment when you're sure the new production deployment is performing as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="e45fb-139">Common questions about swapping deployments</span><span class="sxs-lookup"><span data-stu-id="e45fb-139">Common questions about swapping deployments</span></span>

<span data-ttu-id="e45fb-140">**What are the prerequisites for swapping deployments?**</span><span class="sxs-lookup"><span data-stu-id="e45fb-140">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="e45fb-141">There are two key prerequisites for a successful deployment swap:</span><span class="sxs-lookup"><span data-stu-id="e45fb-141">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="e45fb-142">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span><span class="sxs-lookup"><span data-stu-id="e45fb-142">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="e45fb-143">Otherwise, the swap will fail.</span><span class="sxs-lookup"><span data-stu-id="e45fb-143">Otherwise, the swap will fail.</span></span>

- <span data-ttu-id="e45fb-144">All instances of your roles must be running before you can perform the swap.</span><span class="sxs-lookup"><span data-stu-id="e45fb-144">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="e45fb-145">You can check the status of your instances in the Azure classic portal or by using [the Get-AzureRole command in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/servicemanagement/azure.service/v3.1.0/get-azurerole).</span><span class="sxs-lookup"><span data-stu-id="e45fb-145">You can check the status of your instances in the Azure classic portal or by using [the Get-AzureRole command in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/servicemanagement/azure.service/v3.1.0/get-azurerole).</span></span>

<span data-ttu-id="e45fb-146">Note that guest OS updates and service healing operations can also cause deployment swaps to fail.</span><span class="sxs-lookup"><span data-stu-id="e45fb-146">Note that guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="e45fb-147">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="e45fb-147">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span></span>

<span data-ttu-id="e45fb-148">**Does a swap incur downtime for my application? How should I handle it?**</span><span class="sxs-lookup"><span data-stu-id="e45fb-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="e45fb-149">As described in the last section, a deployment swap is typically very fast since it is just a configuration change in the Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="e45fb-149">As described in the last section, a deployment swap is typically very fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="e45fb-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span><span class="sxs-lookup"><span data-stu-id="e45fb-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="e45fb-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="e45fb-152">How to: Link a resource to a cloud service</span><span class="sxs-lookup"><span data-stu-id="e45fb-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="e45fb-153">To show your cloud service's dependencies on other resources, you can link an Azure SQL Database instance or a storage account to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-153">To show your cloud service's dependencies on other resources, you can link an Azure SQL Database instance or a storage account to the cloud service.</span></span> <span data-ttu-id="e45fb-154">You can link and unlink resources on the **Linked Resources** page, and then monitor their usage on the cloud service dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-154">You can link and unlink resources on the **Linked Resources** page, and then monitor their usage on the cloud service dashboard.</span></span> <span data-ttu-id="e45fb-155">If a linked storage account has monitoring turned on, you can monitor Total Requests on the cloud service dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-155">If a linked storage account has monitoring turned on, you can monitor Total Requests on the cloud service dashboard.</span></span>

<span data-ttu-id="e45fb-156">Use **Link** to link a new or existing SQL Database instance or storage account to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-156">Use **Link** to link a new or existing SQL Database instance or storage account to your cloud service.</span></span> <span data-ttu-id="e45fb-157">You can then scale the database along with the cloud service role that is using it on the **Scale** page.</span><span class="sxs-lookup"><span data-stu-id="e45fb-157">You can then scale the database along with the cloud service role that is using it on the **Scale** page.</span></span> <span data-ttu-id="e45fb-158">(A storage account scales automatically as usage increases.) For more information, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-158">(A storage account scales automatically as usage increases.) For more information, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="e45fb-159">You also can monitor, manage, and scale the database in the **Databases** node of the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="e45fb-159">You also can monitor, manage, and scale the database in the **Databases** node of the Azure classic portal.</span></span>

<span data-ttu-id="e45fb-160">"Linking" a resource in this sense doesn't connect your app to the resource.</span><span class="sxs-lookup"><span data-stu-id="e45fb-160">"Linking" a resource in this sense doesn't connect your app to the resource.</span></span> <span data-ttu-id="e45fb-161">If you create a new database using **Link**, you'll need to add the connection strings to your application code and then upgrade the cloud service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-161">If you create a new database using **Link**, you'll need to add the connection strings to your application code and then upgrade the cloud service.</span></span> <span data-ttu-id="e45fb-162">You'll also need to add connection strings if your app uses resources in a linked storage account.</span><span class="sxs-lookup"><span data-stu-id="e45fb-162">You'll also need to add connection strings if your app uses resources in a linked storage account.</span></span>

<span data-ttu-id="e45fb-163">The following procedure describes how to link a new SQL Database instance, deployed on a new SQL Database server, to a cloud service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-163">The following procedure describes how to link a new SQL Database instance, deployed on a new SQL Database server, to a cloud service.</span></span>

### <a name="to-link-a-sql-database-instance-to-a-cloud-service"></a><span data-ttu-id="e45fb-164">To link a SQL Database instance to a cloud service</span><span class="sxs-lookup"><span data-stu-id="e45fb-164">To link a SQL Database instance to a cloud service</span></span>
1. <span data-ttu-id="e45fb-165">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-165">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="e45fb-166">Then click the name of the cloud service to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-166">Then click the name of the cloud service to open the dashboard.</span></span>
2. <span data-ttu-id="e45fb-167">Click **Linked Resources**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-167">Click **Linked Resources**.</span></span>

    <span data-ttu-id="e45fb-168">The **Linked Resources** page opens.</span><span class="sxs-lookup"><span data-stu-id="e45fb-168">The **Linked Resources** page opens.</span></span>

    ![LinkedResourcesPage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. <span data-ttu-id="e45fb-170">Click either **Link a Resource** or **Link**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-170">Click either **Link a Resource** or **Link**.</span></span>

    <span data-ttu-id="e45fb-171">The **Link Resource** wizard starts.</span><span class="sxs-lookup"><span data-stu-id="e45fb-171">The **Link Resource** wizard starts.</span></span>

    ![Link Page1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. <span data-ttu-id="e45fb-173">Click **Create a new resource** or **Link an existing resource**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-173">Click **Create a new resource** or **Link an existing resource**.</span></span>
5. <span data-ttu-id="e45fb-174">Choose the type of resource to link.</span><span class="sxs-lookup"><span data-stu-id="e45fb-174">Choose the type of resource to link.</span></span> <span data-ttu-id="e45fb-175">In the [Azure classic portal](http://manage.windowsazure.com/), click **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-175">In the [Azure classic portal](http://manage.windowsazure.com/), click **SQL Database**.</span></span> <span data-ttu-id="e45fb-176">(The Preview Azure classic portal does not support linking a storage account to a cloud service.)</span><span class="sxs-lookup"><span data-stu-id="e45fb-176">(The Preview Azure classic portal does not support linking a storage account to a cloud service.)</span></span>
6. <span data-ttu-id="e45fb-177">To complete the database configuration, follow instructions in help for the **SQL Databases** area of the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="e45fb-177">To complete the database configuration, follow instructions in help for the **SQL Databases** area of the Azure classic portal.</span></span>

    <span data-ttu-id="e45fb-178">You can follow the progress of the linking operation in the message area.</span><span class="sxs-lookup"><span data-stu-id="e45fb-178">You can follow the progress of the linking operation in the message area.</span></span>

    <span data-ttu-id="e45fb-179">When linking is complete, you can monitor the status of the linked resource on the cloud service dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-179">When linking is complete, you can monitor the status of the linked resource on the cloud service dashboard.</span></span> <span data-ttu-id="e45fb-180">For information about scaling a linked SQL Database, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-180">For information about scaling a linked SQL Database, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

### <a name="to-unlink-a-linked-resource"></a><span data-ttu-id="e45fb-181">To unlink a linked resource</span><span class="sxs-lookup"><span data-stu-id="e45fb-181">To unlink a linked resource</span></span>
1. <span data-ttu-id="e45fb-182">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-182">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="e45fb-183">Then click the name of the cloud service to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="e45fb-183">Then click the name of the cloud service to open the dashboard.</span></span>
2. <span data-ttu-id="e45fb-184">Click **Linked Resources**, and then select the resource.</span><span class="sxs-lookup"><span data-stu-id="e45fb-184">Click **Linked Resources**, and then select the resource.</span></span>
3. <span data-ttu-id="e45fb-185">Click **Unlink**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-185">Click **Unlink**.</span></span> <span data-ttu-id="e45fb-186">Then click **Yes** at the confirmation prompt.</span><span class="sxs-lookup"><span data-stu-id="e45fb-186">Then click **Yes** at the confirmation prompt.</span></span>

    <span data-ttu-id="e45fb-187">Unlinking a SQL Database has no effect on the database or the application's connections to the database.</span><span class="sxs-lookup"><span data-stu-id="e45fb-187">Unlinking a SQL Database has no effect on the database or the application's connections to the database.</span></span> <span data-ttu-id="e45fb-188">You can still manage the database in the **SQL Databases** area of the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="e45fb-188">You can still manage the database in the **SQL Databases** area of the Azure classic portal.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="e45fb-189">How to: Delete deployments and a cloud service</span><span class="sxs-lookup"><span data-stu-id="e45fb-189">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="e45fb-190">Before you can delete a cloud service, you must delete each existing deployment.</span><span class="sxs-lookup"><span data-stu-id="e45fb-190">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="e45fb-191">To save compute costs, you can delete your staging deployment after you verify that your production deployment is working as expected.</span><span class="sxs-lookup"><span data-stu-id="e45fb-191">To save compute costs, you can delete your staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="e45fb-192">You are billed compute costs for role instances even if a cloud service is not running.</span><span class="sxs-lookup"><span data-stu-id="e45fb-192">You are billed compute costs for role instances even if a cloud service is not running.</span></span>

<span data-ttu-id="e45fb-193">Use the following procedure to delete a deployment or your cloud service.</span><span class="sxs-lookup"><span data-stu-id="e45fb-193">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="e45fb-194">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-194">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="e45fb-195">Select the cloud service, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-195">Select the cloud service, and then click **Delete**.</span></span> <span data-ttu-id="e45fb-196">(To select a cloud service without opening the dashboard, click anywhere except the name in the cloud service entry.)</span><span class="sxs-lookup"><span data-stu-id="e45fb-196">(To select a cloud service without opening the dashboard, click anywhere except the name in the cloud service entry.)</span></span>

    <span data-ttu-id="e45fb-197">If you have a deployment in staging or production, you will see a menu of choices similar to the following one at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="e45fb-197">If you have a deployment in staging or production, you will see a menu of choices similar to the following one at the bottom of the window.</span></span> <span data-ttu-id="e45fb-198">Before you can delete the cloud service, you must delete any existing deployments.</span><span class="sxs-lookup"><span data-stu-id="e45fb-198">Before you can delete the cloud service, you must delete any existing deployments.</span></span>

    ![Delete Menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. <span data-ttu-id="e45fb-200">To delete a deployment, click **Delete production deployment** or **Delete staging deployment**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-200">To delete a deployment, click **Delete production deployment** or **Delete staging deployment**.</span></span> <span data-ttu-id="e45fb-201">Then, at the confirmation prompt, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-201">Then, at the confirmation prompt, click **Yes**.</span></span>
4. <span data-ttu-id="e45fb-202">If you plan to delete the cloud service, repeat step 3, if needed, to delete your other deployment.</span><span class="sxs-lookup"><span data-stu-id="e45fb-202">If you plan to delete the cloud service, repeat step 3, if needed, to delete your other deployment.</span></span>
5. <span data-ttu-id="e45fb-203">To delete the cloud service, click **Delete cloud service**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-203">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="e45fb-204">Then, at the confirmation prompt, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="e45fb-204">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> If verbose monitoring is configured for your cloud service, Azure does not delete the monitoring data from your storage account when you delete the cloud service. You will need to delete the data manually. For information about where to find the metrics tables, see "How to: Access verbose monitoring data outside the Azure classic portal" in [How to Monitor Cloud Services](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a><span data-ttu-id="e45fb-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="e45fb-208">Next steps</span></span>
* <span data-ttu-id="e45fb-209">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-209">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="e45fb-210">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-210">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="e45fb-211">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-211">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="e45fb-212">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="e45fb-212">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>





