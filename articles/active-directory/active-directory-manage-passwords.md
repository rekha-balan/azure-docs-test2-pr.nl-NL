---
title: Manage passwords in Azure Active Directory | Microsoft Docs
description: How to manage passwords in Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: a7679724-0ed5-4973-92e2-bd1285a6ef93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: fee05b9cfb176714e3313ea2e969958bb4cb19f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550157"
---
# <a name="manage-passwords-in-azure-active-directory"></a><span data-ttu-id="bc70b-103">Manage passwords in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc70b-103">Manage passwords in Azure Active Directory</span></span>
<span data-ttu-id="bc70b-104">If you are an administrator, you can reset a user’s password in Azure Active Directory (Azure AD) in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="bc70b-104">If you are an administrator, you can reset a user’s password in Azure Active Directory (Azure AD) in the Azure classic portal.</span></span> <span data-ttu-id="bc70b-105">Click the name of your directory and on the Users page, click the name of the user and at the bottom of the portal click **Reset Password**.</span><span class="sxs-lookup"><span data-stu-id="bc70b-105">Click the name of your directory and on the Users page, click the name of the user and at the bottom of the portal click **Reset Password**.</span></span>

<span data-ttu-id="bc70b-106">This rest of this topic covers the full set of password management capabilities that Azure AD supports, including:</span><span class="sxs-lookup"><span data-stu-id="bc70b-106">This rest of this topic covers the full set of password management capabilities that Azure AD supports, including:</span></span>

* <span data-ttu-id="bc70b-107">**Self-service password** change allows end users or administrators to change their expired or non-expired passwords without calling an administrator or helpdesk for support.</span><span class="sxs-lookup"><span data-stu-id="bc70b-107">**Self-service password** change allows end users or administrators to change their expired or non-expired passwords without calling an administrator or helpdesk for support.</span></span>
* <span data-ttu-id="bc70b-108">**Self-service password** reset allows end users or administrators to reset their passwords automatically without calling an administrator or helpdesk for support.</span><span class="sxs-lookup"><span data-stu-id="bc70b-108">**Self-service password** reset allows end users or administrators to reset their passwords automatically without calling an administrator or helpdesk for support.</span></span> <span data-ttu-id="bc70b-109">Self-service password reset requires Azure AD Premium or Basic.</span><span class="sxs-lookup"><span data-stu-id="bc70b-109">Self-service password reset requires Azure AD Premium or Basic.</span></span> <span data-ttu-id="bc70b-110">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="bc70b-110">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>
* <span data-ttu-id="bc70b-111">**Administrator-initiated password reset** allows an administrator to reset an end user’s or another administrator’s password from within the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="bc70b-111">**Administrator-initiated password reset** allows an administrator to reset an end user’s or another administrator’s password from within the Azure classic portal.</span></span>
* <span data-ttu-id="bc70b-112">**Password management activity reports** give administrators insights into password reset and registration activity occurring in their organization.</span><span class="sxs-lookup"><span data-stu-id="bc70b-112">**Password management activity reports** give administrators insights into password reset and registration activity occurring in their organization.</span></span>
* <span data-ttu-id="bc70b-113">**Password writeback** allows management of on-premises passwords from the cloud so all of the above scenarios can be performed by, or on the behalf of, federated or password synchronized users.</span><span class="sxs-lookup"><span data-stu-id="bc70b-113">**Password writeback** allows management of on-premises passwords from the cloud so all of the above scenarios can be performed by, or on the behalf of, federated or password synchronized users.</span></span> <span data-ttu-id="bc70b-114">Password writeback requires Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="bc70b-114">Password writeback requires Azure AD Premium.</span></span> <span data-ttu-id="bc70b-115">For more information, see [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="bc70b-115">For more information, see [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bc70b-116">Azure AD Premium is available for Chinese customers using the world wide instance of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc70b-116">Azure AD Premium is available for Chinese customers using the world wide instance of Azure AD.</span></span> <span data-ttu-id="bc70b-117">Azure AD Premium is not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span><span class="sxs-lookup"><span data-stu-id="bc70b-117">Azure AD Premium is not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="bc70b-118">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span><span class="sxs-lookup"><span data-stu-id="bc70b-118">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
>
>

<span data-ttu-id="bc70b-119">Use the following links to jump to the documentation you are most interested in:</span><span class="sxs-lookup"><span data-stu-id="bc70b-119">Use the following links to jump to the documentation you are most interested in:</span></span>

* [<span data-ttu-id="bc70b-120">Overview: password management in Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc70b-120">Overview: password management in Azure AD</span></span>](active-directory-passwords-how-it-works.md)
* [<span data-ttu-id="bc70b-121">Self-service password reset in Azure AD: how to enable, configure, and test self-service password reset</span><span class="sxs-lookup"><span data-stu-id="bc70b-121">Self-service password reset in Azure AD: how to enable, configure, and test self-service password reset</span></span>](active-directory-passwords-getting-started.md#enable-users-to-reset-their-azure-ad-passwords)
* [<span data-ttu-id="bc70b-122">Self-service password reset in Azure AD: how to customize password reset to meet your needs</span><span class="sxs-lookup"><span data-stu-id="bc70b-122">Self-service password reset in Azure AD: how to customize password reset to meet your needs</span></span>](active-directory-passwords-customize.md)
* [<span data-ttu-id="bc70b-123">Self-service password reset in Azure AD: deployment and management best practices</span><span class="sxs-lookup"><span data-stu-id="bc70b-123">Self-service password reset in Azure AD: deployment and management best practices</span></span>](active-directory-passwords-best-practices.md)
* [<span data-ttu-id="bc70b-124">Password management reports in Azure AD: how to view password management activity in your tenant</span><span class="sxs-lookup"><span data-stu-id="bc70b-124">Password management reports in Azure AD: how to view password management activity in your tenant</span></span>](active-directory-passwords-get-insights.md)
* [<span data-ttu-id="bc70b-125">Password writeback: how to configure Azure AD to manage on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="bc70b-125">Password writeback: how to configure Azure AD to manage on-premises passwords</span></span>](active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords)
* [<span data-ttu-id="bc70b-126">Troubleshooting Azure AD password management</span><span class="sxs-lookup"><span data-stu-id="bc70b-126">Troubleshooting Azure AD password management</span></span>](active-directory-passwords-troubleshoot.md)
* [<span data-ttu-id="bc70b-127">FAQ for Azure AD password management</span><span class="sxs-lookup"><span data-stu-id="bc70b-127">FAQ for Azure AD password management</span></span>](active-directory-passwords-faq.md)

## <a name="next-steps"></a><span data-ttu-id="bc70b-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc70b-128">Next steps</span></span>
* [<span data-ttu-id="bc70b-129">Administering Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc70b-129">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="bc70b-130">Create or edit users in Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc70b-130">Create or edit users in Azure AD</span></span>](active-directory-create-users.md)
* [<span data-ttu-id="bc70b-131">Manage groups in Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc70b-131">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)
