---
title: Managing Azure resources with Cloud Explorer | Microsoft Docs
description: Learn how to use Cloud Explorer to browse and manage Azure resources within Visual Studio.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: tarcher
ms.openlocfilehash: 13f52ed73b0b03f84379876d28d5138721b66870
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551191"
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="c5fac-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="c5fac-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="c5fac-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5fac-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="c5fac-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span><span class="sxs-lookup"><span data-stu-id="c5fac-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="c5fac-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="c5fac-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c5fac-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5fac-107">Prerequisites</span></span>
- <span data-ttu-id="c5fac-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="c5fac-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="c5fac-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="c5fac-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="c5fac-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span><span class="sxs-lookup"><span data-stu-id="c5fac-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="c5fac-111">Add an Azure account to Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="c5fac-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="c5fac-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="c5fac-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="c5fac-113">In **Cloud Explorer**, select **Azure account settings**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer Azure account settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="c5fac-115">Select **Add new account**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-115">Select **Add new account**.</span></span> 

    ![Cloud Explorer add-account link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="c5fac-117">Log in to the Azure account whose resources you want to browse.</span><span class="sxs-lookup"><span data-stu-id="c5fac-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="c5fac-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span><span class="sxs-lookup"><span data-stu-id="c5fac-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="c5fac-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: select Azure subscriptions to display](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="c5fac-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="c5fac-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Cloud Explorer resource listing for an Azure account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="c5fac-123">Remove an Azure account from Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="c5fac-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="c5fac-124">In **Cloud Explorer**, select **Azure account settings**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer Azure account settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="c5fac-126">Next to the account you want to remove, select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Cloud Explorer Azure account settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="c5fac-128">View resource types or resource groups</span><span class="sxs-lookup"><span data-stu-id="c5fac-128">View resource types or resource groups</span></span>
<span data-ttu-id="c5fac-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span><span class="sxs-lookup"><span data-stu-id="c5fac-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="c5fac-130">In **Cloud Explorer**, select the resource view dropdown.</span><span class="sxs-lookup"><span data-stu-id="c5fac-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![Cloud Explorer dropdown list to select the desired resources view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="c5fac-132">From the context menu, select the desired view:</span><span class="sxs-lookup"><span data-stu-id="c5fac-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="c5fac-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c5fac-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="c5fac-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span><span class="sxs-lookup"><span data-stu-id="c5fac-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="c5fac-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span><span class="sxs-lookup"><span data-stu-id="c5fac-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="c5fac-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5fac-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="c5fac-137">The following image shows a comparison of the two resource views:</span><span class="sxs-lookup"><span data-stu-id="c5fac-137">The following image shows a comparison of the two resource views:</span></span>

    ![Cloud Explorer resource views comparison](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="c5fac-139">View and navigate resources in Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="c5fac-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="c5fac-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span><span class="sxs-lookup"><span data-stu-id="c5fac-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="c5fac-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="c5fac-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="c5fac-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span><span class="sxs-lookup"><span data-stu-id="c5fac-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="c5fac-143">You can also view these options by right-clicking the resource to view its context menu.</span><span class="sxs-lookup"><span data-stu-id="c5fac-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="c5fac-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span><span class="sxs-lookup"><span data-stu-id="c5fac-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="c5fac-145">The following image shows an example comparison of what you see on each tab for an App Service:</span><span class="sxs-lookup"><span data-stu-id="c5fac-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="c5fac-146">Every resource has the action **Open in portal**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="c5fac-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c5fac-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="c5fac-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span><span class="sxs-lookup"><span data-stu-id="c5fac-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="c5fac-149">Additional actions and property values may also appear based on the Azure resource.</span><span class="sxs-lookup"><span data-stu-id="c5fac-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="c5fac-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span><span class="sxs-lookup"><span data-stu-id="c5fac-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="c5fac-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span><span class="sxs-lookup"><span data-stu-id="c5fac-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="c5fac-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span><span class="sxs-lookup"><span data-stu-id="c5fac-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="c5fac-153">Find resources in Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="c5fac-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="c5fac-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="c5fac-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![Finding resources in Cloud Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="c5fac-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span><span class="sxs-lookup"><span data-stu-id="c5fac-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>










