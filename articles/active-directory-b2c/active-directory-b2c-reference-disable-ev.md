---
title: 'Azure Active Directory B2C: Disable Email Verification During Consumer Sign-up | Microsoft Docs'
description: A topic demonstrating how to disable email verification during consumer sign-up in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: 5ab121e536479ef5584b222456e127d5bb12e24d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662055"
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="314f6-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span><span class="sxs-lookup"><span data-stu-id="314f6-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="314f6-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span><span class="sxs-lookup"><span data-stu-id="314f6-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="314f6-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span><span class="sxs-lookup"><span data-stu-id="314f6-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="314f6-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span><span class="sxs-lookup"><span data-stu-id="314f6-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="314f6-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span><span class="sxs-lookup"><span data-stu-id="314f6-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="314f6-108">To support this, Azure AD B2C can be configured to disable email verification.</span><span class="sxs-lookup"><span data-stu-id="314f6-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="314f6-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span><span class="sxs-lookup"><span data-stu-id="314f6-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="314f6-110">By default, sign-up policies have email verification turned on.</span><span class="sxs-lookup"><span data-stu-id="314f6-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="314f6-111">Use the following steps to turn it off:</span><span class="sxs-lookup"><span data-stu-id="314f6-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="314f6-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).</span><span class="sxs-lookup"><span data-stu-id="314f6-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).</span></span>
2. <span data-ttu-id="314f6-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span><span class="sxs-lookup"><span data-stu-id="314f6-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="314f6-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span><span class="sxs-lookup"><span data-stu-id="314f6-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="314f6-115">Click **Edit** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="314f6-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="314f6-116">Click **Page UI Customization**.</span><span class="sxs-lookup"><span data-stu-id="314f6-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="314f6-117">Click **Local account sign-up page**.</span><span class="sxs-lookup"><span data-stu-id="314f6-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="314f6-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span><span class="sxs-lookup"><span data-stu-id="314f6-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="314f6-119">Toggle the **Require verification** option to **No**.</span><span class="sxs-lookup"><span data-stu-id="314f6-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="314f6-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span><span class="sxs-lookup"><span data-stu-id="314f6-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="314f6-121">Click **Save** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="314f6-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="314f6-122">You're done!</span><span class="sxs-lookup"><span data-stu-id="314f6-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="314f6-123">Disabling email verification in the sign-up process may lead to spam.</span><span class="sxs-lookup"><span data-stu-id="314f6-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="314f6-124">If you disable the default one, we recommend adding your own verification system.</span><span class="sxs-lookup"><span data-stu-id="314f6-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="314f6-125">We are always open to feedback and suggestions!</span><span class="sxs-lookup"><span data-stu-id="314f6-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="314f6-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="314f6-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="314f6-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="314f6-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>