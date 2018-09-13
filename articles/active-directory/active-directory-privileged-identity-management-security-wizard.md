---
title: The Azure AD Privileged Identity Management security wizard
description: The first time you use the Azure Active Directory Privileged Identity Management extension, you will be presented with a security wizard. This article describes the steps for using the wizard.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba06eb7e9f3f09e2d1d04cb4118dd81b9e66853e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563913"
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="040ac-104">Using the security wizard in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="040ac-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="040ac-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span><span class="sxs-lookup"><span data-stu-id="040ac-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="040ac-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span><span class="sxs-lookup"><span data-stu-id="040ac-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="040ac-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span><span class="sxs-lookup"><span data-stu-id="040ac-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="040ac-108">What to expect</span><span class="sxs-lookup"><span data-stu-id="040ac-108">What to expect</span></span>
<span data-ttu-id="040ac-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span><span class="sxs-lookup"><span data-stu-id="040ac-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="040ac-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span><span class="sxs-lookup"><span data-stu-id="040ac-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="040ac-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span><span class="sxs-lookup"><span data-stu-id="040ac-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="040ac-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span><span class="sxs-lookup"><span data-stu-id="040ac-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="040ac-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span><span class="sxs-lookup"><span data-stu-id="040ac-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="040ac-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span><span class="sxs-lookup"><span data-stu-id="040ac-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="040ac-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="040ac-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="040ac-116">If you plan to require MFA for activation for that role, that user will be locked out.</span><span class="sxs-lookup"><span data-stu-id="040ac-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="040ac-117">After you have made changes, the wizard will no longer show up.</span><span class="sxs-lookup"><span data-stu-id="040ac-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="040ac-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span><span class="sxs-lookup"><span data-stu-id="040ac-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="040ac-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="040ac-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="040ac-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="040ac-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="040ac-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="040ac-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

