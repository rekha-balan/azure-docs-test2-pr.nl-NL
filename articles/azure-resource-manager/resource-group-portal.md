---
title: Use Azure portal to manage Azure resources | Microsoft Docs
description: Use Azure portal and Azure Resource Manage to manage your resources. Shows how to work with dashboards to monitor resources.
services: azure-resource-manager,azure-portal
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 11/15/2016
ms.author: tomfitz
ms.openlocfilehash: 7398e01a46b5d296f26905e2063acdb98383f567
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808553"
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="0ee3a-104">Manage Azure resources through portal</span><span class="sxs-lookup"><span data-stu-id="0ee3a-104">Manage Azure resources through portal</span></span>

<span data-ttu-id="0ee3a-105">This article shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-105">This article shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="0ee3a-106">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-106">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

[!INCLUDE [Handle personal data](../../includes/gdpr-intro-sentence.md)]

## <a name="manage-resource-groups"></a><span data-ttu-id="0ee3a-107">Manage resource groups</span><span class="sxs-lookup"><span data-stu-id="0ee3a-107">Manage resource groups</span></span>

<span data-ttu-id="0ee3a-108">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-108">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="0ee3a-109">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-109">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="0ee3a-110">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-110">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="0ee3a-111">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-111">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="0ee3a-112">The resource group stores metadata about the resources.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-112">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="0ee3a-113">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-113">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="0ee3a-114">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-114">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="0ee3a-115">To see all the resource groups in your subscription, select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-115">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![browse resource groups](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="0ee3a-117">To create an empty resource group, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-117">To create an empty resource group, select **Add**.</span></span>
   
    ![add resource group](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="0ee3a-119">Provide a name and location for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-119">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="0ee3a-120">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-120">Select **Create**.</span></span>
   
    ![create resource group](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="0ee3a-122">You may need to select **Refresh** to see the recently created resource group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-122">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![refresh resource group](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="0ee3a-124">To customize the information displayed for your resource groups, select **Columns**.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-124">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![customize columns](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="0ee3a-126">Select the columns to add, and then select **Update**.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-126">Select the columns to add, and then select **Update**.</span></span>
   
    ![add columns](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="0ee3a-128">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-128">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="0ee3a-129">For quick access to a resource group, you can pin the resource group to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-129">For quick access to a resource group, you can pin the resource group to your dashboard.</span></span>
   
    ![pin resource group](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="0ee3a-131">The dashboard displays the resource group and its resources.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-131">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="0ee3a-132">You can select either the resource groups or any of its resources to navigate to the item.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-132">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![pin resource group](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="0ee3a-134">Tag resources</span><span class="sxs-lookup"><span data-stu-id="0ee3a-134">Tag resources</span></span>
<span data-ttu-id="0ee3a-135">You can apply tags to resource groups and resources to logically organize your assets.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-135">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="0ee3a-136">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-136">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="0ee3a-137">Monitor resources</span><span class="sxs-lookup"><span data-stu-id="0ee3a-137">Monitor resources</span></span>
<span data-ttu-id="0ee3a-138">When you select a resource, the portal presents default graphs and tables for monitoring that resource type.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-138">When you select a resource, the portal presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="0ee3a-139">Select a resource and notice the **Monitoring** section.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-139">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="0ee3a-140">It includes graphs that are relevant to the resource type.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-140">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="0ee3a-141">The following image shows the default monitoring data for a storage account.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-141">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![show monitoring](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="0ee3a-143">You can pin a section to your dashboard by selecting the ellipsis (...) above the section.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-143">You can pin a section to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="0ee3a-144">You can also customize the size the section or remove it completely.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-144">You can also customize the size the section or remove it completely.</span></span> <span data-ttu-id="0ee3a-145">The following image shows how to pin, customize, or remove the CPU and Memory section.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-145">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![pin section](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="0ee3a-147">After pinning the section to the dashboard, you will see the summary on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-147">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="0ee3a-148">And, selecting it immediately takes you to more details about the data.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-148">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![view dashboard](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="0ee3a-150">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-150">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="0ee3a-152">Give your new dashboard a name and drag tiles onto the dashboard.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-152">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="0ee3a-153">The tiles are filtered by different options.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-153">The tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="0ee3a-155">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-155">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="0ee3a-156">Manage resources</span><span class="sxs-lookup"><span data-stu-id="0ee3a-156">Manage resources</span></span>
<span data-ttu-id="0ee3a-157">When viewing a resource in the portal, you see the options for managing that particular resource.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-157">When viewing a resource in the portal, you see the options for managing that particular resource.</span></span>

![manage resources](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="0ee3a-159">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-159">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="0ee3a-160">Move resources</span><span class="sxs-lookup"><span data-stu-id="0ee3a-160">Move resources</span></span>
<span data-ttu-id="0ee3a-161">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-161">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="0ee3a-162">Lock resources</span><span class="sxs-lookup"><span data-stu-id="0ee3a-162">Lock resources</span></span>
<span data-ttu-id="0ee3a-163">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-163">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="0ee3a-164">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-164">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="0ee3a-165">View your subscription and costs</span><span class="sxs-lookup"><span data-stu-id="0ee3a-165">View your subscription and costs</span></span>
<span data-ttu-id="0ee3a-166">You can view information about your subscription and the rolled-up costs for all your resources.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-166">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="0ee3a-167">Select **Subscriptions** and the subscription you want to see.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-167">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="0ee3a-168">You might only have one subscription to select.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-168">You might only have one subscription to select.</span></span>

![subscription](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="0ee3a-170">You see the burn rate.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-170">You see the burn rate.</span></span>

![burn rate](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="0ee3a-172">And, a breakdown of costs by resource type.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-172">And, a breakdown of costs by resource type.</span></span>

![resource cost](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="0ee3a-174">Export template</span><span class="sxs-lookup"><span data-stu-id="0ee3a-174">Export template</span></span>
<span data-ttu-id="0ee3a-175">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-175">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="0ee3a-176">Exporting the template offers two benefits:</span><span class="sxs-lookup"><span data-stu-id="0ee3a-176">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="0ee3a-177">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-177">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="0ee3a-178">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-178">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="0ee3a-179">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-179">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="0ee3a-180">Delete resource group or resources</span><span class="sxs-lookup"><span data-stu-id="0ee3a-180">Delete resource group or resources</span></span>
<span data-ttu-id="0ee3a-181">Deleting a resource group deletes all the resources contained within it.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-181">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="0ee3a-182">You can also delete individual resources within a resource group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-182">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="0ee3a-183">Use caution when deleting a resource group.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-183">Use caution when deleting a resource group.</span></span> <span data-ttu-id="0ee3a-184">That resource group might contain resources that resources in other resource groups depend on.</span><span class="sxs-lookup"><span data-stu-id="0ee3a-184">That resource group might contain resources that resources in other resource groups depend on.</span></span>

![delete group](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="0ee3a-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ee3a-186">Next steps</span></span>
* <span data-ttu-id="0ee3a-187">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-187">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="0ee3a-188">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-188">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="0ee3a-189">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-189">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="0ee3a-190">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-190">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../role-based-access-control/role-assignments-portal.md).</span></span>
* <span data-ttu-id="0ee3a-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span><span class="sxs-lookup"><span data-stu-id="0ee3a-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span></span>

