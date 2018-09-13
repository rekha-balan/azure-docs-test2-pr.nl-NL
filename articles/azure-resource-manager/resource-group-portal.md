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
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 95ce0ee8ce1cc3c343226fb94fa2abfdb22a2c76
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555225"
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="6be14-104">Manage Azure resources through portal</span><span class="sxs-lookup"><span data-stu-id="6be14-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="6be14-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="6be14-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="6be14-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="6be14-111">Currently, not every service supports the portal or Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6be14-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="6be14-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6be14-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="6be14-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="6be14-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="6be14-114">Manage resource groups</span><span class="sxs-lookup"><span data-stu-id="6be14-114">Manage resource groups</span></span>

<span data-ttu-id="6be14-115">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="6be14-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="6be14-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span><span class="sxs-lookup"><span data-stu-id="6be14-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="6be14-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span><span class="sxs-lookup"><span data-stu-id="6be14-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="6be14-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span><span class="sxs-lookup"><span data-stu-id="6be14-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="6be14-119">The resource group stores metadata about the resources.</span><span class="sxs-lookup"><span data-stu-id="6be14-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="6be14-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span><span class="sxs-lookup"><span data-stu-id="6be14-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="6be14-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span><span class="sxs-lookup"><span data-stu-id="6be14-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="6be14-122">To see all the resource groups in your subscription, select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="6be14-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![browse resource groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="6be14-124">To create an empty resource group, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6be14-124">To create an empty resource group, select **Add**.</span></span>
   
    ![add resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="6be14-126">Provide a name and location for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="6be14-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="6be14-127">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="6be14-127">Select **Create**.</span></span>
   
    ![create resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="6be14-129">You may need to select **Refresh** to see the recently created resource group.</span><span class="sxs-lookup"><span data-stu-id="6be14-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![refresh resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="6be14-131">To customize the information displayed for your resource groups, select **Columns**.</span><span class="sxs-lookup"><span data-stu-id="6be14-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![customize columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="6be14-133">Select the columns to add, and then select **Update**.</span><span class="sxs-lookup"><span data-stu-id="6be14-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![add columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="6be14-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="6be14-136">For quick access to a resource group, you can pin the blade to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="6be14-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![pin resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="6be14-138">The dashboard displays the resource group and its resources.</span><span class="sxs-lookup"><span data-stu-id="6be14-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="6be14-139">You can select either the resource groups or any of its resources to navigate to the item.</span><span class="sxs-lookup"><span data-stu-id="6be14-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![pin resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="6be14-141">Tag resources</span><span class="sxs-lookup"><span data-stu-id="6be14-141">Tag resources</span></span>
<span data-ttu-id="6be14-142">You can apply tags to resource groups and resources to logically organize your assets.</span><span class="sxs-lookup"><span data-stu-id="6be14-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="6be14-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="6be14-144">Monitor resources</span><span class="sxs-lookup"><span data-stu-id="6be14-144">Monitor resources</span></span>
<span data-ttu-id="6be14-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span><span class="sxs-lookup"><span data-stu-id="6be14-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="6be14-146">Select a resource and notice the **Monitoring** section.</span><span class="sxs-lookup"><span data-stu-id="6be14-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="6be14-147">It includes graphs that are relevant to the resource type.</span><span class="sxs-lookup"><span data-stu-id="6be14-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="6be14-148">The following image shows the default monitoring data for a storage account.</span><span class="sxs-lookup"><span data-stu-id="6be14-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![show monitoring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="6be14-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span><span class="sxs-lookup"><span data-stu-id="6be14-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="6be14-151">You can also customize the size the section in the blade or remove it completely.</span><span class="sxs-lookup"><span data-stu-id="6be14-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="6be14-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span><span class="sxs-lookup"><span data-stu-id="6be14-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![pin section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="6be14-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6be14-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="6be14-155">And, selecting it immediately takes you to more details about the data.</span><span class="sxs-lookup"><span data-stu-id="6be14-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![view dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="6be14-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span><span class="sxs-lookup"><span data-stu-id="6be14-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="6be14-159">Give your new dashboard a name and drag tiles onto the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6be14-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="6be14-160">The tiles are filtered by different options.</span><span class="sxs-lookup"><span data-stu-id="6be14-160">The tiles are filtered by different options.</span></span>
   
    ![dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="6be14-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="6be14-163">Manage resources</span><span class="sxs-lookup"><span data-stu-id="6be14-163">Manage resources</span></span>
<span data-ttu-id="6be14-164">In the blade for a resource, you see the options for managing the resource.</span><span class="sxs-lookup"><span data-stu-id="6be14-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="6be14-165">The portal presents management options for that particular resource type.</span><span class="sxs-lookup"><span data-stu-id="6be14-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="6be14-166">You see the management commands across the top of the resource blade and on the left side.</span><span class="sxs-lookup"><span data-stu-id="6be14-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![manage resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/manage-resources.png)

<span data-ttu-id="6be14-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6be14-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="6be14-169">Move resources</span><span class="sxs-lookup"><span data-stu-id="6be14-169">Move resources</span></span>
<span data-ttu-id="6be14-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="6be14-171">Lock resources</span><span class="sxs-lookup"><span data-stu-id="6be14-171">Lock resources</span></span>
<span data-ttu-id="6be14-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span><span class="sxs-lookup"><span data-stu-id="6be14-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="6be14-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="6be14-174">View your subscription and costs</span><span class="sxs-lookup"><span data-stu-id="6be14-174">View your subscription and costs</span></span>
<span data-ttu-id="6be14-175">You can view information about your subscription and the rolled-up costs for all your resources.</span><span class="sxs-lookup"><span data-stu-id="6be14-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="6be14-176">Select **Subscriptions** and the subscription you want to see.</span><span class="sxs-lookup"><span data-stu-id="6be14-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="6be14-177">You might only have one subscription to select.</span><span class="sxs-lookup"><span data-stu-id="6be14-177">You might only have one subscription to select.</span></span>

![subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/select-subscription.png)

<span data-ttu-id="6be14-179">Within the subscription blade, you see a burn rate.</span><span class="sxs-lookup"><span data-stu-id="6be14-179">Within the subscription blade, you see a burn rate.</span></span>

![burn rate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/burn-rate.png)

<span data-ttu-id="6be14-181">And, a breakdown of costs by resource type.</span><span class="sxs-lookup"><span data-stu-id="6be14-181">And, a breakdown of costs by resource type.</span></span>

![resource cost](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="6be14-183">Export template</span><span class="sxs-lookup"><span data-stu-id="6be14-183">Export template</span></span>
<span data-ttu-id="6be14-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span><span class="sxs-lookup"><span data-stu-id="6be14-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="6be14-185">Exporting the template offers two benefits:</span><span class="sxs-lookup"><span data-stu-id="6be14-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="6be14-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span><span class="sxs-lookup"><span data-stu-id="6be14-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="6be14-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span><span class="sxs-lookup"><span data-stu-id="6be14-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="6be14-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="6be14-189">Delete resource group or resources</span><span class="sxs-lookup"><span data-stu-id="6be14-189">Delete resource group or resources</span></span>
<span data-ttu-id="6be14-190">Deleting a resource group deletes all the resources contained within it.</span><span class="sxs-lookup"><span data-stu-id="6be14-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="6be14-191">You can also delete individual resources within a resource group.</span><span class="sxs-lookup"><span data-stu-id="6be14-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="6be14-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span><span class="sxs-lookup"><span data-stu-id="6be14-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="6be14-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span><span class="sxs-lookup"><span data-stu-id="6be14-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![delete group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="6be14-195">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6be14-195">Next Steps</span></span>
* <span data-ttu-id="6be14-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="6be14-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="6be14-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="6be14-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="6be14-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6be14-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>



















