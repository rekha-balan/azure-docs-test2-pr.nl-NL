---
title: 'Azure AD Connect sync: How to manage the Azure AD service account | Microsoft Docs'
description: This topic documents how to restore the Azure AD service account.
services: active-directory
keywords: AADSTS70002, AADSTS50054, How to reset the password for the Azure AD Connect sync Connector service account
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 8f201f2478e2883289a6cc4b435e2c3218950b1d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830778"
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="c0eba-104">Azure AD Connect sync: How to manage the Azure AD service account</span><span class="sxs-lookup"><span data-stu-id="c0eba-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="c0eba-105">The service account used by the Azure AD Connector is supposed to be service free.</span><span class="sxs-lookup"><span data-stu-id="c0eba-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="c0eba-106">If you need to reset its credentials, then this topic is for you.</span><span class="sxs-lookup"><span data-stu-id="c0eba-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="c0eba-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0eba-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="c0eba-108">Reset the credentials</span><span class="sxs-lookup"><span data-stu-id="c0eba-108">Reset the credentials</span></span>
<span data-ttu-id="c0eba-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span><span class="sxs-lookup"><span data-stu-id="c0eba-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="c0eba-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0eba-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="c0eba-111">Run `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="c0eba-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="c0eba-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="c0eba-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="c0eba-113">Provide Azure AD Global admin credentials.</span><span class="sxs-lookup"><span data-stu-id="c0eba-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="c0eba-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span><span class="sxs-lookup"><span data-stu-id="c0eba-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="c0eba-115">Known issues these steps can solve</span><span class="sxs-lookup"><span data-stu-id="c0eba-115">Known issues these steps can solve</span></span>
<span data-ttu-id="c0eba-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span><span class="sxs-lookup"><span data-stu-id="c0eba-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="c0eba-117">Event 6900</span><span class="sxs-lookup"><span data-stu-id="c0eba-117">Event 6900</span></span>  
<span data-ttu-id="c0eba-118">The server encountered an unexpected error while processing a password change notification:</span><span class="sxs-lookup"><span data-stu-id="c0eba-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="c0eba-119">AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="c0eba-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="c0eba-120">AADSTS50054: Old password is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="c0eba-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="c0eba-121">Event 659</span><span class="sxs-lookup"><span data-stu-id="c0eba-121">Event 659</span></span>  
<span data-ttu-id="c0eba-122">Error while retrieving password policy sync configuration.</span><span class="sxs-lookup"><span data-stu-id="c0eba-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="c0eba-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="c0eba-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="c0eba-124">AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="c0eba-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="c0eba-125">AADSTS50054: Old password is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="c0eba-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0eba-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0eba-126">Next steps</span></span>
<span data-ttu-id="c0eba-127">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="c0eba-127">**Overview topics**</span></span>

* [<span data-ttu-id="c0eba-128">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="c0eba-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="c0eba-129">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0eba-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

