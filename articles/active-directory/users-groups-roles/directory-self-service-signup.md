---
title: Self-service or trial signup in Azure Active Directory | Microsoft Docs
description: Use self-service signup in an Azure Active Directory (Azure AD) tenant
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: users-groups-roles
ms.topic: article
ms.workload: identity
ms.date: 01/28/2018
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: it-pro
ms.openlocfilehash: 99c5e99fa3bd33ef42e8df6ceba5be4be2cd1249
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968695"
---
# <a name="what-is-self-service-signup-for-azure-active-directory"></a><span data-ttu-id="9517f-103">What is self-service signup for Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9517f-103">What is self-service signup for Azure Active Directory?</span></span>
<span data-ttu-id="9517f-104">This article explains self-service signup and how to support it in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9517f-104">This article explains self-service signup and how to support it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9517f-105">If you want to take over a domain name from an unmanaged Azure AD tenant, see [Take over an unmanaged directory as administrator](domains-admin-takeover.md).</span><span class="sxs-lookup"><span data-stu-id="9517f-105">If you want to take over a domain name from an unmanaged Azure AD tenant, see [Take over an unmanaged directory as administrator](domains-admin-takeover.md).</span></span>

## <a name="why-use-self-service-signup"></a><span data-ttu-id="9517f-106">Why use self-service signup?</span><span class="sxs-lookup"><span data-stu-id="9517f-106">Why use self-service signup?</span></span>
* <span data-ttu-id="9517f-107">Get customers to services they want faster</span><span class="sxs-lookup"><span data-stu-id="9517f-107">Get customers to services they want faster</span></span>
* <span data-ttu-id="9517f-108">Create email-based offers for a service</span><span class="sxs-lookup"><span data-stu-id="9517f-108">Create email-based offers for a service</span></span>
* <span data-ttu-id="9517f-109">Create email-based signup flows that quickly allow users to create identities using their easy-to-remember work email aliases</span><span class="sxs-lookup"><span data-stu-id="9517f-109">Create email-based signup flows that quickly allow users to create identities using their easy-to-remember work email aliases</span></span>
* <span data-ttu-id="9517f-110">A self-service-created Azure AD directory can be turned into a managed directory that can be used for other services</span><span class="sxs-lookup"><span data-stu-id="9517f-110">A self-service-created Azure AD directory can be turned into a managed directory that can be used for other services</span></span>

## <a name="terms-and-definitions"></a><span data-ttu-id="9517f-111">Terms and definitions</span><span class="sxs-lookup"><span data-stu-id="9517f-111">Terms and definitions</span></span>
* <span data-ttu-id="9517f-112">**Self-service signup**: This is the method by which a user signs up for a cloud service and has an identity automatically created for them in Azure AD based on their email domain.</span><span class="sxs-lookup"><span data-stu-id="9517f-112">**Self-service signup**: This is the method by which a user signs up for a cloud service and has an identity automatically created for them in Azure AD based on their email domain.</span></span>
* <span data-ttu-id="9517f-113">**Unmanaged Azure AD directory**: This is the directory where that identity is created.</span><span class="sxs-lookup"><span data-stu-id="9517f-113">**Unmanaged Azure AD directory**: This is the directory where that identity is created.</span></span> <span data-ttu-id="9517f-114">An unmanaged directory is a directory that has no global administrator.</span><span class="sxs-lookup"><span data-stu-id="9517f-114">An unmanaged directory is a directory that has no global administrator.</span></span>
* <span data-ttu-id="9517f-115">**Email-verified user**: This is a type of user account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9517f-115">**Email-verified user**: This is a type of user account in Azure AD.</span></span> <span data-ttu-id="9517f-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span><span class="sxs-lookup"><span data-stu-id="9517f-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span></span> <span data-ttu-id="9517f-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span><span class="sxs-lookup"><span data-stu-id="9517f-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span></span>

## <a name="how-do-i-control-self-service-settings"></a><span data-ttu-id="9517f-118">How do I control self-service settings?</span><span class="sxs-lookup"><span data-stu-id="9517f-118">How do I control self-service settings?</span></span>
<span data-ttu-id="9517f-119">Admins have two self-service controls today.</span><span class="sxs-lookup"><span data-stu-id="9517f-119">Admins have two self-service controls today.</span></span> <span data-ttu-id="9517f-120">They can control whether:</span><span class="sxs-lookup"><span data-stu-id="9517f-120">They can control whether:</span></span>

* <span data-ttu-id="9517f-121">Users can join the directory via email.</span><span class="sxs-lookup"><span data-stu-id="9517f-121">Users can join the directory via email.</span></span>
* <span data-ttu-id="9517f-122">Users can license themselves for applications and services.</span><span class="sxs-lookup"><span data-stu-id="9517f-122">Users can license themselves for applications and services.</span></span>

### <a name="how-can-i-control-these-capabilities"></a><span data-ttu-id="9517f-123">How can I control these capabilities?</span><span class="sxs-lookup"><span data-stu-id="9517f-123">How can I control these capabilities?</span></span>
<span data-ttu-id="9517f-124">An admin can configure these capabilities using the following Azure AD cmdlet Set-MsolCompanySettings parameters:</span><span class="sxs-lookup"><span data-stu-id="9517f-124">An admin can configure these capabilities using the following Azure AD cmdlet Set-MsolCompanySettings parameters:</span></span>

* <span data-ttu-id="9517f-125">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span><span class="sxs-lookup"><span data-stu-id="9517f-125">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span></span> <span data-ttu-id="9517f-126">If you set that parameter to $false, no email-verified users can join the directory.</span><span class="sxs-lookup"><span data-stu-id="9517f-126">If you set that parameter to $false, no email-verified users can join the directory.</span></span>
* <span data-ttu-id="9517f-127">**AllowAdHocSubscriptions** controls the ability for users to perform self-service signup.</span><span class="sxs-lookup"><span data-stu-id="9517f-127">**AllowAdHocSubscriptions** controls the ability for users to perform self-service signup.</span></span> <span data-ttu-id="9517f-128">If you set that parameter to $false, no users can perform self-service signup.</span><span class="sxs-lookup"><span data-stu-id="9517f-128">If you set that parameter to $false, no users can perform self-service signup.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="9517f-129">Flow and PowerApps trial signups are not controlled by the **AllowAdHocSubscriptions** setting.</span><span class="sxs-lookup"><span data-stu-id="9517f-129">Flow and PowerApps trial signups are not controlled by the **AllowAdHocSubscriptions** setting.</span></span> <span data-ttu-id="9517f-130">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="9517f-130">For more information, see the following articles:</span></span>
  > * [<span data-ttu-id="9517f-131">How can I prevent my existing users from starting to use Power BI?</span><span class="sxs-lookup"><span data-stu-id="9517f-131">How can I prevent my existing users from starting to use Power BI?</span></span>](https://support.office.com/article/Power-BI-in-your-Organization-d7941332-8aec-4e5e-87e8-92073ce73dc5#bkmk_preventjoining)
  > * [<span data-ttu-id="9517f-132">Flow in your organization Q&A</span><span class="sxs-lookup"><span data-stu-id="9517f-132">Flow in your organization Q&A</span></span>](https://docs.microsoft.com/flow/organization-q-and-a)

### <a name="how-do-the-controls-work-together"></a><span data-ttu-id="9517f-133">How do the controls work together?</span><span class="sxs-lookup"><span data-stu-id="9517f-133">How do the controls work together?</span></span>
<span data-ttu-id="9517f-134">These two parameters can be used in conjunction to define more precise control over self-service signup.</span><span class="sxs-lookup"><span data-stu-id="9517f-134">These two parameters can be used in conjunction to define more precise control over self-service signup.</span></span> <span data-ttu-id="9517f-135">For example, the following command will allow users to perform self-service signup, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account to be created first cannot perform self-service signup):</span><span class="sxs-lookup"><span data-stu-id="9517f-135">For example, the following command will allow users to perform self-service signup, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account to be created first cannot perform self-service signup):</span></span>

````
    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true
````
<span data-ttu-id="9517f-136">The following flowchart explains the different combinations for these parameters and the resulting conditions for the directory and self-service signup.</span><span class="sxs-lookup"><span data-stu-id="9517f-136">The following flowchart explains the different combinations for these parameters and the resulting conditions for the directory and self-service signup.</span></span>

![][1]

<span data-ttu-id="9517f-137">For more information and examples of how to use these parameters, see [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="9517f-137">For more information and examples of how to use these parameters, see [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9517f-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="9517f-138">Next steps</span></span>
* [<span data-ttu-id="9517f-139">Add a custom domain name to Azure AD</span><span class="sxs-lookup"><span data-stu-id="9517f-139">Add a custom domain name to Azure AD</span></span>](../fundamentals/add-custom-domain.md)
* [<span data-ttu-id="9517f-140">How to install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9517f-140">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="9517f-141">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9517f-141">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="9517f-142">Azure Cmdlet Reference</span><span class="sxs-lookup"><span data-stu-id="9517f-142">Azure Cmdlet Reference</span></span>](/powershell/azure/get-started-azureps)
* [<span data-ttu-id="9517f-143">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="9517f-143">Set-MsolCompanySettings</span></span>](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/directory-self-service-signup/SelfServiceSignUpControls.png
