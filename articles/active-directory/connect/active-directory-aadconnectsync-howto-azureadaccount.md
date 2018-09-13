---
title: 'Azure AD Connect sync: How to manage the Azure AD service account | Microsoft Docs'
description: This topic documents how to restore the Azure AD service account.
services: active-directory
keywords: AADSTS70002, AADSTS50054, How to reset the password for the Azure AD Connect sync Connector service account
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: dfd86805fd2da48b94d776c318b246e62666b978
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671580"
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="797aa-104">Azure AD Connect sync: How to manage the Azure AD service account</span><span class="sxs-lookup"><span data-stu-id="797aa-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="797aa-105">The service account used by the Azure AD Connector is supposed to be service free.</span><span class="sxs-lookup"><span data-stu-id="797aa-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="797aa-106">If you need to reset its credentials, then this topic is for you.</span><span class="sxs-lookup"><span data-stu-id="797aa-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="797aa-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="797aa-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="797aa-108">Reset the credentials</span><span class="sxs-lookup"><span data-stu-id="797aa-108">Reset the credentials</span></span>
<span data-ttu-id="797aa-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span><span class="sxs-lookup"><span data-stu-id="797aa-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="797aa-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span><span class="sxs-lookup"><span data-stu-id="797aa-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="797aa-111">Run `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="797aa-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="797aa-112">![PowerShell cmdlet addadsyncaadserviceaccount](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="797aa-112">![PowerShell cmdlet addadsyncaadserviceaccount](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="797aa-113">Provide Azure AD Global admin credentials.</span><span class="sxs-lookup"><span data-stu-id="797aa-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="797aa-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span><span class="sxs-lookup"><span data-stu-id="797aa-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="797aa-115">Known issues these steps can solve</span><span class="sxs-lookup"><span data-stu-id="797aa-115">Known issues these steps can solve</span></span>
<span data-ttu-id="797aa-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span><span class="sxs-lookup"><span data-stu-id="797aa-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="797aa-117">Event 6900</span><span class="sxs-lookup"><span data-stu-id="797aa-117">Event 6900</span></span>  
<span data-ttu-id="797aa-118">The server encountered an unexpected error while processing a password change notification:</span><span class="sxs-lookup"><span data-stu-id="797aa-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="797aa-119">AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="797aa-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="797aa-120">AADSTS50054: Old password is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="797aa-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="797aa-121">Event 659</span><span class="sxs-lookup"><span data-stu-id="797aa-121">Event 659</span></span>  
<span data-ttu-id="797aa-122">Error while retrieving password policy sync configuration.</span><span class="sxs-lookup"><span data-stu-id="797aa-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="797aa-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="797aa-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="797aa-124">AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="797aa-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="797aa-125">AADSTS50054: Old password is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="797aa-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="797aa-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="797aa-126">Next steps</span></span>
<span data-ttu-id="797aa-127">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="797aa-127">**Overview topics**</span></span>

* [<span data-ttu-id="797aa-128">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="797aa-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="797aa-129">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="797aa-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)


