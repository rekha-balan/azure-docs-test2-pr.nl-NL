---
title: Troubleshoot creating tenants in Azure Active Directory B2C | Microsoft Docs
description: Issues and resolutions for creating an Azure Active Directory or Azure Active Directory B2C tenant.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 12/06/2016
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 009f7ac2f7e614b7e07623e41888973f1a2b254d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826007"
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="bed00-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span><span class="sxs-lookup"><span data-stu-id="bed00-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="bed00-104">Create an Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="bed00-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="bed00-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span><span class="sxs-lookup"><span data-stu-id="bed00-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="bed00-106">If the problem persists, contact Azure Support.</span><span class="sxs-lookup"><span data-stu-id="bed00-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="bed00-107">Create an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="bed00-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="bed00-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span><span class="sxs-lookup"><span data-stu-id="bed00-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="bed00-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span><span class="sxs-lookup"><span data-stu-id="bed00-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="bed00-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span><span class="sxs-lookup"><span data-stu-id="bed00-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="bed00-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="bed00-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="bed00-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span><span class="sxs-lookup"><span data-stu-id="bed00-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="bed00-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span><span class="sxs-lookup"><span data-stu-id="bed00-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="bed00-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span><span class="sxs-lookup"><span data-stu-id="bed00-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="bed00-115">If these resolutions don't work, contact Azure Support.</span><span class="sxs-lookup"><span data-stu-id="bed00-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="bed00-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="bed00-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

