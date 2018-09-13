---
title: Problem saving administrator credentials while configuring user provisioning to an Azure AD Gallery application | Microsoft Docs
description: How to troubleshoot common issues faced when configuring user provisioning to an application already listed in the Azure AD Application Gallery
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: barbkess
ms.reviewer: asmalser
ms.openlocfilehash: fe96ecc0ba6904819f0262a2f470e37203a7952e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858005"
---
# <a name="problem-saving-administrator-credentials-while-configuring-user-provisioning-to-an-azure-active-directory-gallery-application"></a><span data-ttu-id="e83e0-103">Problem saving administrator credentials while configuring user provisioning to an Azure Active Directory Gallery application</span><span class="sxs-lookup"><span data-stu-id="e83e0-103">Problem saving administrator credentials while configuring user provisioning to an Azure Active Directory Gallery application</span></span> 

<span data-ttu-id="e83e0-104">When using the Azure portal to configure [automatic user provisioning](user-provisioning.md) for an enterprise application, you may encounter a situation where:</span><span class="sxs-lookup"><span data-stu-id="e83e0-104">When using the Azure portal to configure [automatic user provisioning](user-provisioning.md) for an enterprise application, you may encounter a situation where:</span></span>

* <span data-ttu-id="e83e0-105">The **Admin Credentials** entered for the application are valid, and the **Test Connection** button works.</span><span class="sxs-lookup"><span data-stu-id="e83e0-105">The **Admin Credentials** entered for the application are valid, and the **Test Connection** button works.</span></span> <span data-ttu-id="e83e0-106">However, the credentials cannot be saved, and the Azure portal returns a generic error message.</span><span class="sxs-lookup"><span data-stu-id="e83e0-106">However, the credentials cannot be saved, and the Azure portal returns a generic error message.</span></span>

<span data-ttu-id="e83e0-107">If SAML-based single sign-on is also configured for the same application, the most likely cause of the error is that Azure AD's internal, per-application storage limit for certificates and credentials has been exceeded.</span><span class="sxs-lookup"><span data-stu-id="e83e0-107">If SAML-based single sign-on is also configured for the same application, the most likely cause of the error is that Azure AD's internal, per-application storage limit for certificates and credentials has been exceeded.</span></span>

<span data-ttu-id="e83e0-108">Azure AD currently has a maximum storage capacity of one kilobyte for all certificates, secret tokens, credentials, and related configuration data associated with a single instance of an application (also known as a service principal record in Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e83e0-108">Azure AD currently has a maximum storage capacity of one kilobyte for all certificates, secret tokens, credentials, and related configuration data associated with a single instance of an application (also known as a service principal record in Azure AD).</span></span>

<span data-ttu-id="e83e0-109">When SAML-based single sign-on is configured, the certificate used to sign the SAML tokens is stored here, and often consumes over 50% percent of the space.</span><span class="sxs-lookup"><span data-stu-id="e83e0-109">When SAML-based single sign-on is configured, the certificate used to sign the SAML tokens is stored here, and often consumes over 50% percent of the space.</span></span>

<span data-ttu-id="e83e0-110">Any secret tokens, URIs, notification email addresses, user names, and passwords that get entered during setup of user provisioning can cause the storage limit to be exceeded.</span><span class="sxs-lookup"><span data-stu-id="e83e0-110">Any secret tokens, URIs, notification email addresses, user names, and passwords that get entered during setup of user provisioning can cause the storage limit to be exceeded.</span></span>

## <a name="how-to-work-around-this-issue"></a><span data-ttu-id="e83e0-111">How to work around this issue</span><span class="sxs-lookup"><span data-stu-id="e83e0-111">How to work around this issue</span></span> 

<span data-ttu-id="e83e0-112">There are two possible ways to work around this issue today:</span><span class="sxs-lookup"><span data-stu-id="e83e0-112">There are two possible ways to work around this issue today:</span></span>

1. <span data-ttu-id="e83e0-113">**Use two gallery application instances, one for single sign-on and one for user provisioning** - Taking the gallery application [LinkedIn Elevate](../saas-apps/linkedinelevate-tutorial.md) as an example, you can add LinkedIn Elevate from the gallery and configure it for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e83e0-113">**Use two gallery application instances, one for single sign-on and one for user provisioning** - Taking the gallery application [LinkedIn Elevate](../saas-apps/linkedinelevate-tutorial.md) as an example, you can add LinkedIn Elevate from the gallery and configure it for single sign-on.</span></span> <span data-ttu-id="e83e0-114">For provisioning, add another instance of LinkedIn Elevate from the Azure AD app gallery, and name it "LinkedIn Elevate (Provisioning)."</span><span class="sxs-lookup"><span data-stu-id="e83e0-114">For provisioning, add another instance of LinkedIn Elevate from the Azure AD app gallery, and name it "LinkedIn Elevate (Provisioning)."</span></span> <span data-ttu-id="e83e0-115">For this second instance, configure [provisioning](../saas-apps/linkedinelevate-provisioning-tutorial.md), but not single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e83e0-115">For this second instance, configure [provisioning](../saas-apps/linkedinelevate-provisioning-tutorial.md), but not single sign-on.</span></span> <span data-ttu-id="e83e0-116">When using this workaround, the same users and groups need to be [assigned](assign-user-or-group-access-portal.md) to both applications.</span><span class="sxs-lookup"><span data-stu-id="e83e0-116">When using this workaround, the same users and groups need to be [assigned](assign-user-or-group-access-portal.md) to both applications.</span></span> 

2. <span data-ttu-id="e83e0-117">**Reduce the amount of configuration data stored** - All data entered in the [Admin credentials](user-provisioning.md#how-do-i-set-up-automatic-provisioning-to-an-application) section of the provisioning tab is stored in the same place as the SAML certificate.</span><span class="sxs-lookup"><span data-stu-id="e83e0-117">**Reduce the amount of configuration data stored** - All data entered in the [Admin credentials](user-provisioning.md#how-do-i-set-up-automatic-provisioning-to-an-application) section of the provisioning tab is stored in the same place as the SAML certificate.</span></span> <span data-ttu-id="e83e0-118">While it may not be possible to reduce the length of all of this data, some optional configuration fields like the **Notification Email** can be removed.</span><span class="sxs-lookup"><span data-stu-id="e83e0-118">While it may not be possible to reduce the length of all of this data, some optional configuration fields like the **Notification Email** can be removed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e83e0-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="e83e0-119">Next steps</span></span>
[<span data-ttu-id="e83e0-120">Configure user provisioning and de-provisioning to SaaS applications</span><span class="sxs-lookup"><span data-stu-id="e83e0-120">Configure user provisioning and de-provisioning to SaaS applications</span></span>](user-provisioning.md)
