---
title: How manage user accounts in Azure API Management | Microsoft Docs
description: Learn how to create or invite users in Azure API Management
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
ms.openlocfilehash: 3d9a4454a1b3f65b42a46a26e8d483fad83f65f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804016"
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="e02c4-103">How to manage user accounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="e02c4-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="e02c4-104">In API Management, developers are the users of the APIs that you expose using API Management.</span><span class="sxs-lookup"><span data-stu-id="e02c4-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="e02c4-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="e02c4-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="e02c4-106">For information on managing user accounts programmatically, see the [User entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-user-entity) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span><span class="sxs-lookup"><span data-stu-id="e02c4-106">For information on managing user accounts programmatically, see the [User entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-user-entity) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e02c4-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e02c4-107">Prerequisites</span></span>

<span data-ttu-id="e02c4-108">Complete tasks in this article: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="e02c4-108">Complete tasks in this article: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="e02c4-109"><a name="create-developer"> </a>Create a new developer</span><span class="sxs-lookup"><span data-stu-id="e02c4-109"><a name="create-developer"> </a>Create a new developer</span></span>

<span data-ttu-id="e02c4-110">To add a new user, follow the steps in this section:</span><span class="sxs-lookup"><span data-stu-id="e02c4-110">To add a new user, follow the steps in this section:</span></span>

1. <span data-ttu-id="e02c4-111">Select the **Users** tab to the left of the screen.</span><span class="sxs-lookup"><span data-stu-id="e02c4-111">Select the **Users** tab to the left of the screen.</span></span>
2. <span data-ttu-id="e02c4-112">Press **+Add**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-112">Press **+Add**.</span></span>
3. <span data-ttu-id="e02c4-113">Enter appropriate information for the user.</span><span class="sxs-lookup"><span data-stu-id="e02c4-113">Enter appropriate information for the user.</span></span>
4. <span data-ttu-id="e02c4-114">Press **Add**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-114">Press **Add**.</span></span>

    ![Add a new user](./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png)

<span data-ttu-id="e02c4-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span><span class="sxs-lookup"><span data-stu-id="e02c4-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span> <span data-ttu-id="e02c4-117">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span><span class="sxs-lookup"><span data-stu-id="e02c4-117">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="e02c4-118">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="e02c4-118">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="e02c4-119"><a name="invite-developer"> </a>Invite a developer</span><span class="sxs-lookup"><span data-stu-id="e02c4-119"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="e02c4-120">To invite a developer, follow the steps in this section:</span><span class="sxs-lookup"><span data-stu-id="e02c4-120">To invite a developer, follow the steps in this section:</span></span>

1. <span data-ttu-id="e02c4-121">Select the **Users** tab to the left of the screen.</span><span class="sxs-lookup"><span data-stu-id="e02c4-121">Select the **Users** tab to the left of the screen.</span></span>
2. <span data-ttu-id="e02c4-122">Press **+Invite**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-122">Press **+Invite**.</span></span>

<span data-ttu-id="e02c4-123">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span><span class="sxs-lookup"><span data-stu-id="e02c4-123">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

<span data-ttu-id="e02c4-124">When a developer is invited, an email is sent to the developer.</span><span class="sxs-lookup"><span data-stu-id="e02c4-124">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="e02c4-125">This email is generated using a template and is customizable.</span><span class="sxs-lookup"><span data-stu-id="e02c4-125">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="e02c4-126">For more information, see [Configure email templates][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="e02c4-126">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="e02c4-127">Once the invitation is accepted, the account becomes active.</span><span class="sxs-lookup"><span data-stu-id="e02c4-127">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="e02c4-128"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span><span class="sxs-lookup"><span data-stu-id="e02c4-128"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>

<span data-ttu-id="e02c4-129">By default, newly created or invited developer accounts are **Active**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-129">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="e02c4-130">To deactivate a developer account, click **Block**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-130">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="e02c4-131">To reactivate a blocked developer account, click **Activate**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-131">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="e02c4-132">A blocked developer account can't access the developer portal or call any APIs.</span><span class="sxs-lookup"><span data-stu-id="e02c4-132">A blocked developer account can't access the developer portal or call any APIs.</span></span> <span data-ttu-id="e02c4-133">To delete a user account, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-133">To delete a user account, click **Delete**.</span></span>

<span data-ttu-id="e02c4-134">To block a user, follow the following steps.</span><span class="sxs-lookup"><span data-stu-id="e02c4-134">To block a user, follow the following steps.</span></span>

1. <span data-ttu-id="e02c4-135">Select the **Users** tab to the left of the screen.</span><span class="sxs-lookup"><span data-stu-id="e02c4-135">Select the **Users** tab to the left of the screen.</span></span>
2. <span data-ttu-id="e02c4-136">Click on the user that you want to block.</span><span class="sxs-lookup"><span data-stu-id="e02c4-136">Click on the user that you want to block.</span></span>
3. <span data-ttu-id="e02c4-137">Press **Block**.</span><span class="sxs-lookup"><span data-stu-id="e02c4-137">Press **Block**.</span></span>

## <a name="reset-a-user-password"></a><span data-ttu-id="e02c4-138">Reset a user password</span><span class="sxs-lookup"><span data-stu-id="e02c4-138">Reset a user password</span></span>

<span data-ttu-id="e02c4-139">To programmatically work with user accounts, see the [User entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-user-entity) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span><span class="sxs-lookup"><span data-stu-id="e02c4-139">To programmatically work with user accounts, see the [User entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-user-entity) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="e02c4-140">To reset a user account password to a specific value, you can use the [Update a user](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-user-entity#UpdateUser) operation and specify the desired password.</span><span class="sxs-lookup"><span data-stu-id="e02c4-140">To reset a user account password to a specific value, you can use the [Update a user](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-user-entity#UpdateUser) operation and specify the desired password.</span></span>

## <span data-ttu-id="e02c4-141"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="e02c4-141"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="e02c4-142">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span><span class="sxs-lookup"><span data-stu-id="e02c4-142">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="e02c4-143">For more information, see [How to create and use groups][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="e02c4-143">For more information, see [How to create and use groups][How to create and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: get-started-create-service-instance.md
[Create an API Management service instance]: get-started-create-service-instance.md
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
