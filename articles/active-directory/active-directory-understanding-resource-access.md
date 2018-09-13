---
title: Understanding resource access in Azure | Microsoft Docs
description: This topic explains concepts about using subscription administrators to control resource access in the full Azure portal.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: curtand
ms.openlocfilehash: 8fd6e575e458b7a87f22c12170e5441214320221
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564439"
---
# <a name="understanding-resource-access-in-azure"></a><span data-ttu-id="d0b2a-103">Understanding resource access in Azure</span><span class="sxs-lookup"><span data-stu-id="d0b2a-103">Understanding resource access in Azure</span></span>
> [!NOTE]
> <span data-ttu-id="d0b2a-104">This topic explains concepts about using subscription administrators to control resource access in the full Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-104">This topic explains concepts about using subscription administrators to control resource access in the full Azure portal.</span></span> <span data-ttu-id="d0b2a-105">As an alternative, the Azure Preview portal provides [role-based access control](role-based-access-control-configure.md) so Azure resources can be managed more precisely.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-105">As an alternative, the Azure Preview portal provides [role-based access control](role-based-access-control-configure.md) so Azure resources can be managed more precisely.</span></span>
> 
> 

<span data-ttu-id="d0b2a-106">In October 2013, the Azure classic portal and Service Management APIs were integrated with Azure Active Directory in order to lay the groundwork for improving the user experience for managing access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-106">In October 2013, the Azure classic portal and Service Management APIs were integrated with Azure Active Directory in order to lay the groundwork for improving the user experience for managing access to Azure resources.</span></span> <span data-ttu-id="d0b2a-107">Azure Active Directory already provides great capabilities such as user management, on-premises directory sync, multi-factor authentication, and application access control.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-107">Azure Active Directory already provides great capabilities such as user management, on-premises directory sync, multi-factor authentication, and application access control.</span></span> <span data-ttu-id="d0b2a-108">Naturally, these should also be made available for managing Azure resources across-the-board.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-108">Naturally, these should also be made available for managing Azure resources across-the-board.</span></span>

<span data-ttu-id="d0b2a-109">Access control in Azure starts from a billing perspective.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-109">Access control in Azure starts from a billing perspective.</span></span> <span data-ttu-id="d0b2a-110">The owner of an Azure account, accessed by visiting the  [Azure Accounts Center](https://account.windowsazure.com/subscriptions), is the Account Administrator (AA).</span><span class="sxs-lookup"><span data-stu-id="d0b2a-110">The owner of an Azure account, accessed by visiting the  [Azure Accounts Center](https://account.windowsazure.com/subscriptions), is the Account Administrator (AA).</span></span> <span data-ttu-id="d0b2a-111">Subscriptions are a container for billing, but they also act as a security boundary: each subscription has a Service Administrator (SA) who can add, remove, and modify Azure resources in that subscription by using the [Azure classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="d0b2a-111">Subscriptions are a container for billing, but they also act as a security boundary: each subscription has a Service Administrator (SA) who can add, remove, and modify Azure resources in that subscription by using the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="d0b2a-112">The default SA of a new subscription is the AA, but the AA can change the SA in the Azure Accounts Center.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-112">The default SA of a new subscription is the AA, but the AA can change the SA in the Azure Accounts Center.</span></span>

<br><br>![Azure Accounts][1]

<span data-ttu-id="d0b2a-114">Subscriptions also have an association with a directory.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-114">Subscriptions also have an association with a directory.</span></span> <span data-ttu-id="d0b2a-115">The directory defines a set of users.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-115">The directory defines a set of users.</span></span> <span data-ttu-id="d0b2a-116">These can be users from the work or school that created the directory or they can be external users (that is, Microsoft Accounts).</span><span class="sxs-lookup"><span data-stu-id="d0b2a-116">These can be users from the work or school that created the directory or they can be external users (that is, Microsoft Accounts).</span></span> <span data-ttu-id="d0b2a-117">Subscriptions are accessible by a subset of those directory users who have been assigned as either Service Administrator (SA) or Co-Administrator (CA); the only exception is that, for legacy reasons, Microsoft Accounts (formerly Windows Live ID) can be assigned as SA or CA without being present in the directory.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-117">Subscriptions are accessible by a subset of those directory users who have been assigned as either Service Administrator (SA) or Co-Administrator (CA); the only exception is that, for legacy reasons, Microsoft Accounts (formerly Windows Live ID) can be assigned as SA or CA without being present in the directory.</span></span>

<br><br>![Access Control in Azure][2]

<span data-ttu-id="d0b2a-119">Functionality within the Azure classic portal enables SAs that are signed in using a Microsoft Account to change the directory that a subscription is associated with by using the **Edit Directory** command on the **Subscriptions** page in **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-119">Functionality within the Azure classic portal enables SAs that are signed in using a Microsoft Account to change the directory that a subscription is associated with by using the **Edit Directory** command on the **Subscriptions** page in **Settings**.</span></span> <span data-ttu-id="d0b2a-120">Note that this operation has implications on the access control of that subscription.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-120">Note that this operation has implications on the access control of that subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d0b2a-121">The **Edit Directory** command in the Azure classic portal is not available to users who are signed in using a work or school account because those accounts can sign in only to the directory to which they belong.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-121">The **Edit Directory** command in the Azure classic portal is not available to users who are signed in using a work or school account because those accounts can sign in only to the directory to which they belong.</span></span>
> 
> 

<br><br>![Simple User Login Flow][3]

<span data-ttu-id="d0b2a-123">In the simple case, an organization (such as Contoso) will enforce billing and access control across the same set of subscriptions.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-123">In the simple case, an organization (such as Contoso) will enforce billing and access control across the same set of subscriptions.</span></span> <span data-ttu-id="d0b2a-124">That is, the directory is associated to subscriptions that are owned by a single Azure Account.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-124">That is, the directory is associated to subscriptions that are owned by a single Azure Account.</span></span> <span data-ttu-id="d0b2a-125">Upon successful login to the Azure classic portal, users see two collections of resources (depicted in orange in the previous illustration):</span><span class="sxs-lookup"><span data-stu-id="d0b2a-125">Upon successful login to the Azure classic portal, users see two collections of resources (depicted in orange in the previous illustration):</span></span>

* <span data-ttu-id="d0b2a-126">Directories where their user account exists (sourced or added as a foreign principal).</span><span class="sxs-lookup"><span data-stu-id="d0b2a-126">Directories where their user account exists (sourced or added as a foreign principal).</span></span> <span data-ttu-id="d0b2a-127">Note that the directory used for login isn’t relevant to this computation, so your directories will always be shown regardless of where you logged in.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-127">Note that the directory used for login isn’t relevant to this computation, so your directories will always be shown regardless of where you logged in.</span></span>
* <span data-ttu-id="d0b2a-128">Resources that are part of subscriptions that are associated with the directory used for login AND which the user can access (where they are an SA or CA).</span><span class="sxs-lookup"><span data-stu-id="d0b2a-128">Resources that are part of subscriptions that are associated with the directory used for login AND which the user can access (where they are an SA or CA).</span></span>

<br><br>![User with Multiple Subscriptions and Directories][4]

<span data-ttu-id="d0b2a-130">Users with subscriptions across multiple directories have the ability to switch the current context of the Azure classic portal by using the subscription filter.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-130">Users with subscriptions across multiple directories have the ability to switch the current context of the Azure classic portal by using the subscription filter.</span></span> <span data-ttu-id="d0b2a-131">Under the covers, this results in a separate login to a different directory, but this is accomplished seamlessly using single sign-on (SSO).</span><span class="sxs-lookup"><span data-stu-id="d0b2a-131">Under the covers, this results in a separate login to a different directory, but this is accomplished seamlessly using single sign-on (SSO).</span></span>

<span data-ttu-id="d0b2a-132">Operations such as moving resources between subscriptions can be more difficult as a result of this single directory view of subscriptions.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-132">Operations such as moving resources between subscriptions can be more difficult as a result of this single directory view of subscriptions.</span></span> <span data-ttu-id="d0b2a-133">To perform the resource transfer, it may be necessary to first use the **Edit Directory** command on the Subscriptions page in **Settings** to associate the subscriptions to the same directory.</span><span class="sxs-lookup"><span data-stu-id="d0b2a-133">To perform the resource transfer, it may be necessary to first use the **Edit Directory** command on the Subscriptions page in **Settings** to associate the subscriptions to the same directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0b2a-134">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d0b2a-134">Next Steps</span></span>
* <span data-ttu-id="d0b2a-135">To learn more about how to change administrators for an Azure subscription, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md)</span><span class="sxs-lookup"><span data-stu-id="d0b2a-135">To learn more about how to change administrators for an Azure subscription, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md)</span></span>
* <span data-ttu-id="d0b2a-136">For more information on how Azure Active Directory relates to your Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)</span><span class="sxs-lookup"><span data-stu-id="d0b2a-136">For more information on how Azure Active Directory relates to your Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)</span></span>
* <span data-ttu-id="d0b2a-137">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="d0b2a-137">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-understanding-resource-access/IC707931.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-understanding-resource-access/IC707932.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-understanding-resource-access/IC707933.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-understanding-resource-access/IC707934.png




