---
title: Account provisioning notifications | Microsoft Docs
description: Learn how to ensure that you are notified of issues related to user provisioning that require your attention by enabling account provisioning notifications.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 9f01ab7c2da781a8fef990135238b7be2150238f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554779"
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="cc8c2-103">Account Provisioning Notifications</span><span class="sxs-lookup"><span data-stu-id="cc8c2-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="cc8c2-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="cc8c2-105">While this is an automated process, your interaction with this process is from time to time required.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="cc8c2-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="cc8c2-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="cc8c2-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![User Provisioning][1] 

<span data-ttu-id="cc8c2-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Account Provisioning Notifications][2]

<span data-ttu-id="cc8c2-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="cc8c2-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="cc8c2-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span><span class="sxs-lookup"><span data-stu-id="cc8c2-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="cc8c2-115">Related Articles</span><span class="sxs-lookup"><span data-stu-id="cc8c2-115">Related Articles</span></span>
* [<span data-ttu-id="cc8c2-116">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc8c2-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="cc8c2-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="cc8c2-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="cc8c2-118">Customizing Attribute Mappings for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="cc8c2-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="cc8c2-119">Writing Expressions for Attribute Mappings</span><span class="sxs-lookup"><span data-stu-id="cc8c2-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="cc8c2-120">Scoping Filters for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="cc8c2-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="cc8c2-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="cc8c2-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="cc8c2-122">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="cc8c2-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-account-provisioning-notifications/ic766308.png


