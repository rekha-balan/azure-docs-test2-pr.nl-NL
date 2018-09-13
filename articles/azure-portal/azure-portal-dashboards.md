---
title: Azure portal dashboards | Microsoft Docs
description: This article explains how to create and edit dashboards in the Azure portal.
services: azure-portal
documentationcenter: ''
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 589ebeb01954a6e4cc6005c02030e3a6cdb8a193
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554425"
---
# <a name="creating-and-sharing-dashboards-in-the-azure-portal"></a><span data-ttu-id="c4fd3-103">Creating and sharing dashboards in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c4fd3-103">Creating and sharing dashboards in the Azure portal</span></span>
<span data-ttu-id="c4fd3-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="c4fd3-105">This post goes through the basics of creating/editing, publishing, and managing access to dashboards.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-105">This post goes through the basics of creating/editing, publishing, and managing access to dashboards.</span></span>

## <a name="customizing-dashboards-versus-blades"></a><span data-ttu-id="c4fd3-106">Customizing dashboards versus blades</span><span class="sxs-lookup"><span data-stu-id="c4fd3-106">Customizing dashboards versus blades</span></span>
<span data-ttu-id="c4fd3-107">Since launching dashboards a few months ago, there has been a steady decline in blade customizations and a rapid increase in dashboard customizations.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-107">Since launching dashboards a few months ago, there has been a steady decline in blade customizations and a rapid increase in dashboard customizations.</span></span> <span data-ttu-id="c4fd3-108">This strong usage trend shows that you prefer customizing dashboards over blades.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-108">This strong usage trend shows that you prefer customizing dashboards over blades.</span></span> <span data-ttu-id="c4fd3-109">To support that trend, we will remove the ability to customize blades and dedicate our efforts to enhancing dashboard functionality.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-109">To support that trend, we will remove the ability to customize blades and dedicate our efforts to enhancing dashboard functionality.</span></span> <span data-ttu-id="c4fd3-110">If you customized a blade, your customization will soon be removed.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-110">If you customized a blade, your customization will soon be removed.</span></span> <span data-ttu-id="c4fd3-111">To preserve that customization, pin the customized tiles to a dashboard.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-111">To preserve that customization, pin the customized tiles to a dashboard.</span></span> <span data-ttu-id="c4fd3-112">Simply right-click the tile and select **Pin to dashboard** as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-112">Simply right-click the tile and select **Pin to dashboard** as shown in the following image.</span></span>

![save customized tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/save-customization.png)

## <a name="create-a-dashboard"></a><span data-ttu-id="c4fd3-114">Create a dashboard</span><span class="sxs-lookup"><span data-stu-id="c4fd3-114">Create a dashboard</span></span>
<span data-ttu-id="c4fd3-115">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-115">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![create dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="c4fd3-117">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-117">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="c4fd3-118">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-118">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="c4fd3-119">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-119">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![customize dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="c4fd3-121">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-121">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="c4fd3-122">There's a new category called **General** for tiles that are not associated with a particular resource.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-122">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="c4fd3-123">In this example, we pin the Markdown tile.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-123">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="c4fd3-124">You use this tile to add custom content to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-124">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="c4fd3-125">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-125">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="c4fd3-126">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span><span class="sxs-lookup"><span data-stu-id="c4fd3-126">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![add markdown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="c4fd3-128">Edit a dashboard</span><span class="sxs-lookup"><span data-stu-id="c4fd3-128">Edit a dashboard</span></span>
<span data-ttu-id="c4fd3-129">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-129">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="c4fd3-130">Let's pin the representation of our resource group.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-130">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="c4fd3-131">You can either pin when browsing the item, or from the resource group blade.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-131">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="c4fd3-132">Both approaches result in pinning the tile representation of the resource group.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-132">Both approaches result in pinning the tile representation of the resource group.</span></span>

![pin to dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="c4fd3-134">After pinning the item, it appears on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-134">After pinning the item, it appears on your dashboard.</span></span>

![view dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="c4fd3-136">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-136">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="c4fd3-137">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-137">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="c4fd3-138">By default, there are two items:</span><span class="sxs-lookup"><span data-stu-id="c4fd3-138">By default, there are two items:</span></span>

1. <span data-ttu-id="c4fd3-139">**Unpin from dashboard** – removes the tile from the dashboard</span><span class="sxs-lookup"><span data-stu-id="c4fd3-139">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="c4fd3-140">**Customize** – enters customize mode</span><span class="sxs-lookup"><span data-stu-id="c4fd3-140">**Customize** – enters customize mode</span></span>

![customize tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="c4fd3-142">By selecting customize, you can resize and reorder tiles.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-142">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="c4fd3-143">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-143">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![resize tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="c4fd3-145">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-145">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![resize tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="c4fd3-147">After resizing tiles, view the dashboard.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-147">After resizing tiles, view the dashboard.</span></span>

![view tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="c4fd3-149">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-149">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="c4fd3-150">Publish a dashboard and manage access control</span><span class="sxs-lookup"><span data-stu-id="c4fd3-150">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="c4fd3-151">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-151">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="c4fd3-152">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-152">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![share dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="c4fd3-154">You are asked to choose a subscription and resource group for your dashboard to be published to.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-154">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="c4fd3-155">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span><span class="sxs-lookup"><span data-stu-id="c4fd3-155">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="c4fd3-156">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd3-156">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="c4fd3-157">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-157">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="c4fd3-158">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-158">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="c4fd3-159">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-159">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="c4fd3-160">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-160">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="c4fd3-161">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-161">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="c4fd3-162">However, they can make a private copy of the dashboard for their own use.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-162">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="c4fd3-163">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-163">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="c4fd3-164">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-164">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![publish dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="c4fd3-166">You can also choose to publish a dashboard to a particular resource group.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-166">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="c4fd3-167">The access control for that dashboard matches the access control for the resource group.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-167">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="c4fd3-168">Users that can manage the resources in that resource group also have access to the dashboards.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-168">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![publish dashboard to resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="c4fd3-170">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-170">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="c4fd3-171">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-171">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="c4fd3-172">You can always get back to this view by selecting **Share**.</span><span class="sxs-lookup"><span data-stu-id="c4fd3-172">You can always get back to this view by selecting **Share**.</span></span>

![manage access control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="c4fd3-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4fd3-174">Next steps</span></span>
* <span data-ttu-id="c4fd3-175">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd3-175">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="c4fd3-176">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd3-176">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>















