---
title: How manage user accounts in Azure API Management | Microsoft Docs
description: Learn how to create or invite users in Azure API Management
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7619e32f0c64f503a61b23c346643543ec92c19f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563719"
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="da985-103">How to manage user accounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="da985-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="da985-104">In API Management, developers are the users of the APIs that you expose using API Management.</span><span class="sxs-lookup"><span data-stu-id="da985-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="da985-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="da985-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="da985-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span><span class="sxs-lookup"><span data-stu-id="da985-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="da985-107"><a name="create-developer"> </a>Create a new developer</span><span class="sxs-lookup"><span data-stu-id="da985-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="da985-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="da985-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="da985-109">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="da985-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="da985-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="da985-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Publisher portal][api-management-management-console]

<span data-ttu-id="da985-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span><span class="sxs-lookup"><span data-stu-id="da985-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="da985-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="da985-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="da985-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span><span class="sxs-lookup"><span data-stu-id="da985-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="da985-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span><span class="sxs-lookup"><span data-stu-id="da985-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="da985-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="da985-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="da985-120"><a name="invite-developer"> </a>Invite a developer</span><span class="sxs-lookup"><span data-stu-id="da985-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="da985-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="da985-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="da985-123">Enter the name and email address of the developer, and click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="da985-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="da985-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span><span class="sxs-lookup"><span data-stu-id="da985-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="da985-127">When a developer is invited, an email is sent to the developer.</span><span class="sxs-lookup"><span data-stu-id="da985-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="da985-128">This email is generated using a template and is customizable.</span><span class="sxs-lookup"><span data-stu-id="da985-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="da985-129">For more information, see [Configure email templates][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="da985-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="da985-130">Once the invitation is accepted, the account becomes active.</span><span class="sxs-lookup"><span data-stu-id="da985-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="da985-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span><span class="sxs-lookup"><span data-stu-id="da985-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="da985-132">By default, newly created or invited developer accounts are **Active**.</span><span class="sxs-lookup"><span data-stu-id="da985-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="da985-133">To deactivate a developer account, click **Block**.</span><span class="sxs-lookup"><span data-stu-id="da985-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="da985-134">To reactivate a blocked developer account, click **Activate**.</span><span class="sxs-lookup"><span data-stu-id="da985-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="da985-135">A blocked developer account can not access the developer portal or call any APIs.</span><span class="sxs-lookup"><span data-stu-id="da985-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="da985-136">To delete a user account, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="da985-136">To delete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="da985-138">Reset a user password</span><span class="sxs-lookup"><span data-stu-id="da985-138">Reset a user password</span></span>
<span data-ttu-id="da985-139">To reset the password for a user account, click the name of the account.</span><span class="sxs-lookup"><span data-stu-id="da985-139">To reset the password for a user account, click the name of the account.</span></span>

![Reset password][api-management-view-developer]

<span data-ttu-id="da985-141">Click **Reset password** to send a link to the user to reset their password.</span><span class="sxs-lookup"><span data-stu-id="da985-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Reset password][api-management-reset-password]

<span data-ttu-id="da985-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span><span class="sxs-lookup"><span data-stu-id="da985-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="da985-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span><span class="sxs-lookup"><span data-stu-id="da985-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="da985-145">Pending verification</span><span class="sxs-lookup"><span data-stu-id="da985-145">Pending verification</span></span>
![Pending verification][api-management-pending-verification]

## <span data-ttu-id="da985-147"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="da985-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="da985-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span><span class="sxs-lookup"><span data-stu-id="da985-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="da985-149">For more information, see [How to create and use groups][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="da985-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates










