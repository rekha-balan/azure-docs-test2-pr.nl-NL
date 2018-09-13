---
title: Manage developer accounts using groups in Azure API Management | Microsoft Docs
description: Learn how to manage developer accounts using groups in Azure API Management
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ec04136978cf819e317fe342888356371d4e7f16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661883"
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="e7a2a-103">How to create and use groups to manage developer accounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="e7a2a-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="e7a2a-104">In API Management, groups are used to manage the visibility of products to developers.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="e7a2a-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="e7a2a-106">API Management has the following immutable system groups.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="e7a2a-107">**Administrators** - Azure subscription administrators are members of this group.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="e7a2a-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="e7a2a-109">**Developers** - Authenticated developer portal users fall into this group.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="e7a2a-110">Developers are the customers that build applications using your APIs.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="e7a2a-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="e7a2a-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="e7a2a-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="e7a2a-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="e7a2a-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="e7a2a-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="e7a2a-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="e7a2a-117">A user can be a member of more than one group.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="e7a2a-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a2a-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="e7a2a-120"><a name="create-group"> </a>Create a group</span><span class="sxs-lookup"><span data-stu-id="e7a2a-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="e7a2a-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="e7a2a-122">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-122">This takes you to the API Management publisher portal.</span></span>

![Publisher portal][api-management-management-console]

> <span data-ttu-id="e7a2a-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="e7a2a-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Add new group][api-management-add-group]

<span data-ttu-id="e7a2a-127">Enter a unique name for the group and an optional description, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Add new group][api-management-add-group-window]

<span data-ttu-id="e7a2a-129">The new group is displayed in the groups tab. To edit the **Name** or **Description** of the group, click the name of the group in the list.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-129">The new group is displayed in the groups tab. To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="e7a2a-130">To delete the group, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-130">To delete the group, click **Delete**.</span></span>

![Group added][api-management-new-group]

<span data-ttu-id="e7a2a-132">Now that the group is created, it can be associated with products and developers.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-132">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="e7a2a-133"><a name="associate-group-product"> </a>Associate a group with a product</span><span class="sxs-lookup"><span data-stu-id="e7a2a-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="e7a2a-134">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-134">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Set visibility][api-management-add-group-to-product]

<span data-ttu-id="e7a2a-136">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-136">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="e7a2a-137">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-137">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="e7a2a-139">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="e7a2a-139">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="e7a2a-140">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-140">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="e7a2a-141">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-141">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="e7a2a-142"><a name="associate-group-developer"> </a>Associate groups with developers</span><span class="sxs-lookup"><span data-stu-id="e7a2a-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="e7a2a-143">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-143">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Add developer to group][api-management-add-group-to-developer]

<span data-ttu-id="e7a2a-145">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-145">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="e7a2a-146">Developers can be removed from groups by using the **Remove from Group** drop-down.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-146">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Developers][api-management-add-group-to-developer-saved]

<span data-ttu-id="e7a2a-148">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-148">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="e7a2a-149"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="e7a2a-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="e7a2a-150">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-150">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="e7a2a-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="e7a2a-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="e7a2a-152">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span><span class="sxs-lookup"><span data-stu-id="e7a2a-152">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group








