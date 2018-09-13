---
title: Manage developer accounts using groups in Azure API Management | Microsoft Docs
description: Learn how to manage developer accounts using groups in Azure API Management
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2018
ms.author: apimpm
ms.openlocfilehash: 3986b07c3568c3dcbb4077361d38f74d658458cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804380"
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="155df-103">How to create and use groups to manage developer accounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="155df-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="155df-104">In API Management, groups are used to manage the visibility of products to developers.</span><span class="sxs-lookup"><span data-stu-id="155df-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="155df-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span><span class="sxs-lookup"><span data-stu-id="155df-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="155df-106">API Management has the following immutable system groups:</span><span class="sxs-lookup"><span data-stu-id="155df-106">API Management has the following immutable system groups:</span></span>

* <span data-ttu-id="155df-107">**Administrators** - Azure subscription administrators are members of this group.</span><span class="sxs-lookup"><span data-stu-id="155df-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="155df-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span><span class="sxs-lookup"><span data-stu-id="155df-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="155df-109">**Developers** - Authenticated developer portal users fall into this group.</span><span class="sxs-lookup"><span data-stu-id="155df-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="155df-110">Developers are the customers that build applications using your APIs.</span><span class="sxs-lookup"><span data-stu-id="155df-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="155df-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="155df-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="155df-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span><span class="sxs-lookup"><span data-stu-id="155df-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="155df-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span><span class="sxs-lookup"><span data-stu-id="155df-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="155df-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="155df-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="155df-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span><span class="sxs-lookup"><span data-stu-id="155df-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="155df-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span><span class="sxs-lookup"><span data-stu-id="155df-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="155df-117">A user can be a member of more than one group.</span><span class="sxs-lookup"><span data-stu-id="155df-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="155df-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span><span class="sxs-lookup"><span data-stu-id="155df-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

<span data-ttu-id="155df-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-group-entity) entity.</span><span class="sxs-lookup"><span data-stu-id="155df-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-group-entity) entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="155df-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="155df-120">Prerequisites</span></span>

<span data-ttu-id="155df-121">Complete tasks in this article: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="155df-121">Complete tasks in this article: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="155df-122"><a name="create-group"> </a>Create a group</span><span class="sxs-lookup"><span data-stu-id="155df-122"><a name="create-group"> </a>Create a group</span></span>

<span data-ttu-id="155df-123">This section shows how to add a new group to your API Management account.</span><span class="sxs-lookup"><span data-stu-id="155df-123">This section shows how to add a new group to your API Management account.</span></span>

1. <span data-ttu-id="155df-124">Select the **Groups** tab to the left of the screen.</span><span class="sxs-lookup"><span data-stu-id="155df-124">Select the **Groups** tab to the left of the screen.</span></span>
2. <span data-ttu-id="155df-125">Click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="155df-125">Click **+Add**.</span></span>
3. <span data-ttu-id="155df-126">Enter a unique name for the group and an optional description.</span><span class="sxs-lookup"><span data-stu-id="155df-126">Enter a unique name for the group and an optional description.</span></span>
4. <span data-ttu-id="155df-127">Press **Create**.</span><span class="sxs-lookup"><span data-stu-id="155df-127">Press **Create**.</span></span>

    ![Add a new group](./media/api-management-howto-create-groups/groups001.png)

<span data-ttu-id="155df-129">Once the group is created, it is added to the **Groups** list.</span><span class="sxs-lookup"><span data-stu-id="155df-129">Once the group is created, it is added to the **Groups** list.</span></span> <br/><span data-ttu-id="155df-130">To edit the **Name** or **Description** of the group, click the name of the group and **Settings**.</span><span class="sxs-lookup"><span data-stu-id="155df-130">To edit the **Name** or **Description** of the group, click the name of the group and **Settings**.</span></span><br/><span data-ttu-id="155df-131">To delete the group, click the name of the group and press **Delete**.</span><span class="sxs-lookup"><span data-stu-id="155df-131">To delete the group, click the name of the group and press **Delete**.</span></span>

<span data-ttu-id="155df-132">Now that the group is created, it can be associated with products and developers.</span><span class="sxs-lookup"><span data-stu-id="155df-132">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="155df-133"><a name="associate-group-product"> </a>Associate a group with a product</span><span class="sxs-lookup"><span data-stu-id="155df-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>

1. <span data-ttu-id="155df-134">Select the **Products** tab to the left.</span><span class="sxs-lookup"><span data-stu-id="155df-134">Select the **Products** tab to the left.</span></span>
2. <span data-ttu-id="155df-135">Click the name of the desired product.</span><span class="sxs-lookup"><span data-stu-id="155df-135">Click the name of the desired product.</span></span>
3. <span data-ttu-id="155df-136">Press **Access control**.</span><span class="sxs-lookup"><span data-stu-id="155df-136">Press **Access control**.</span></span>
4. <span data-ttu-id="155df-137">Click **+ Add group**.</span><span class="sxs-lookup"><span data-stu-id="155df-137">Click **+ Add group**.</span></span>

    ![Associate a group with a product](./media/api-management-howto-create-groups/groups002.png)
5. <span data-ttu-id="155df-139">Select the group you want to add.</span><span class="sxs-lookup"><span data-stu-id="155df-139">Select the group you want to add.</span></span>

    ![Associate a group with a product](./media/api-management-howto-create-groups/groups003.png)

    <span data-ttu-id="155df-141">To remove a group from the product, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="155df-141">To remove a group from the product, click **Delete**.</span></span>

    ![Delete a group](./media/api-management-howto-create-groups/groups004.png)

<span data-ttu-id="155df-143">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span><span class="sxs-lookup"><span data-stu-id="155df-143">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

> [!NOTE]
> <span data-ttu-id="155df-144">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="155df-144">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>

## <span data-ttu-id="155df-145"><a name="associate-group-developer"> </a>Associate groups with developers</span><span class="sxs-lookup"><span data-stu-id="155df-145"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>

<span data-ttu-id="155df-146">This section shows how to associate groups with members.</span><span class="sxs-lookup"><span data-stu-id="155df-146">This section shows how to associate groups with members.</span></span>

1. <span data-ttu-id="155df-147">Select the **Groups** tab to the left of the screen.</span><span class="sxs-lookup"><span data-stu-id="155df-147">Select the **Groups** tab to the left of the screen.</span></span>
2. <span data-ttu-id="155df-148">Select **Members**.</span><span class="sxs-lookup"><span data-stu-id="155df-148">Select **Members**.</span></span>

    ![Add a member](./media/api-management-howto-create-groups/groups005.png)
3. <span data-ttu-id="155df-150">Press **+Add** and select a member.</span><span class="sxs-lookup"><span data-stu-id="155df-150">Press **+Add** and select a member.</span></span>

    ![Add a member](./media/api-management-howto-create-groups/groups006.png)
4. <span data-ttu-id="155df-152">Press **Select**.</span><span class="sxs-lookup"><span data-stu-id="155df-152">Press **Select**.</span></span>

<span data-ttu-id="155df-153">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="155df-153">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="155df-154"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="155df-154"><a name="next-steps"> </a>Next steps</span></span>

* <span data-ttu-id="155df-155">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span><span class="sxs-lookup"><span data-stu-id="155df-155">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="155df-156">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="155df-156">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="155df-157">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-group-entity) entity.</span><span class="sxs-lookup"><span data-stu-id="155df-157">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-group-entity) entity.</span></span>

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: get-started-create-service-instance.md
[Create an API Management service instance]: get-started-create-service-instance.md
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md
