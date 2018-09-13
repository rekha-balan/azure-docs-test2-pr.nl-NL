---
title: Azure Active Directory user authentication
description: As an Azure AD Administrator how do I protect user authentication while reducing end-user impact?
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: overview
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry, michmcla
ms.openlocfilehash: 0b232ed8bacfeb896fd5ee6ff9e2a58b71dc1517
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870752"
---
# <a name="what-methods-are-available-for-authentication"></a><span data-ttu-id="6f3e1-103">What methods are available for authentication?</span><span class="sxs-lookup"><span data-stu-id="6f3e1-103">What methods are available for authentication?</span></span>

<span data-ttu-id="6f3e1-104">We hear reports in the news, passwords being stolen, and identities being compromised.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-104">We hear reports in the news, passwords being stolen, and identities being compromised.</span></span> <span data-ttu-id="6f3e1-105">Requiring a second factor in addition to a password immediately increases the security of your organization.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-105">Requiring a second factor in addition to a password immediately increases the security of your organization.</span></span> <span data-ttu-id="6f3e1-106">Microsoft Azure Active Directory (Azure AD) includes features, like Azure Multi-Factor Authentication (Azure MFA) and Azure AD self-service password reset (SSPR), to help administrators protect their organizations and users with additional authentication methods.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-106">Microsoft Azure Active Directory (Azure AD) includes features, like Azure Multi-Factor Authentication (Azure MFA) and Azure AD self-service password reset (SSPR), to help administrators protect their organizations and users with additional authentication methods.</span></span>

<span data-ttu-id="6f3e1-107">When a user needs to access a sensitive application, reset their password, or enable Windows Hello, they may be asked to provide additional verification that they are who they say they are.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-107">When a user needs to access a sensitive application, reset their password, or enable Windows Hello, they may be asked to provide additional verification that they are who they say they are.</span></span>

<span data-ttu-id="6f3e1-108">Additional verification may come in the form of authentication methods such as:</span><span class="sxs-lookup"><span data-stu-id="6f3e1-108">Additional verification may come in the form of authentication methods such as:</span></span>

* <span data-ttu-id="6f3e1-109">A code provided in an email or text message</span><span class="sxs-lookup"><span data-stu-id="6f3e1-109">A code provided in an email or text message</span></span>
* <span data-ttu-id="6f3e1-110">A phone call</span><span class="sxs-lookup"><span data-stu-id="6f3e1-110">A phone call</span></span>
* <span data-ttu-id="6f3e1-111">A notification or code on their phone</span><span class="sxs-lookup"><span data-stu-id="6f3e1-111">A notification or code on their phone</span></span>
* <span data-ttu-id="6f3e1-112">Answers to security questions</span><span class="sxs-lookup"><span data-stu-id="6f3e1-112">Answers to security questions</span></span>

![Example login.microsoftonline.com login page in Chrome](media/overview-authentication/overview-login.png)

<span data-ttu-id="6f3e1-114">Azure MFA and Azure AD self-service password reset give administrators control over configuration, policy, monitoring, and reporting using Azure AD and the Azure portal to protect their organizations.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-114">Azure MFA and Azure AD self-service password reset give administrators control over configuration, policy, monitoring, and reporting using Azure AD and the Azure portal to protect their organizations.</span></span>

## <a name="self-service-password-reset"></a><span data-ttu-id="6f3e1-115">Self-service password reset</span><span class="sxs-lookup"><span data-stu-id="6f3e1-115">Self-service password reset</span></span>

<span data-ttu-id="6f3e1-116">Self-service password reset provides your users the ability to reset their password, with no administrator intervention, when and where they need to.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-116">Self-service password reset provides your users the ability to reset their password, with no administrator intervention, when and where they need to.</span></span>

> [!VIDEO https://www.youtube.com/embed/hc97Yx5PJiM]

<span data-ttu-id="6f3e1-117">Self-service password reset includes:</span><span class="sxs-lookup"><span data-stu-id="6f3e1-117">Self-service password reset includes:</span></span>

* <span data-ttu-id="6f3e1-118">**Password change:** I know my password but want to change it to something new.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-118">**Password change:** I know my password but want to change it to something new.</span></span>
* <span data-ttu-id="6f3e1-119">**Password reset:** I can't sign in and want to reset my password using one or more approved authentication methods.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-119">**Password reset:** I can't sign in and want to reset my password using one or more approved authentication methods.</span></span>
* <span data-ttu-id="6f3e1-120">**Account unlock:** I can't sign in because my account is locked out and I want to unlock using one or more approved authentication methods.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-120">**Account unlock:** I can't sign in because my account is locked out and I want to unlock using one or more approved authentication methods.</span></span>

## <a name="multi-factor-authentication"></a><span data-ttu-id="6f3e1-121">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6f3e1-121">Multi-Factor Authentication</span></span>

<span data-ttu-id="6f3e1-122">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-122">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="6f3e1-123">Using administrator approved authentication methods, Azure MFA helps safeguard your access to data and applications, while meeting the demand for a simple sign-in process.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-123">Using administrator approved authentication methods, Azure MFA helps safeguard your access to data and applications, while meeting the demand for a simple sign-in process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f3e1-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f3e1-124">Next steps</span></span>

<span data-ttu-id="6f3e1-125">The next step is to dive in and configure self-service password reset and Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="6f3e1-125">The next step is to dive in and configure self-service password reset and Azure Multi-Factor Authentication.</span></span>

<span data-ttu-id="6f3e1-126">To get started with self-service password reset, see the [enable SSPR quickstart article](quickstart-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="6f3e1-126">To get started with self-service password reset, see the [enable SSPR quickstart article](quickstart-sspr.md).</span></span>

<span data-ttu-id="6f3e1-127">Learn more about self-service password reset in the article, [How it works: Azure AD self-service password reset](concept-sspr-howitworks.md)</span><span class="sxs-lookup"><span data-stu-id="6f3e1-127">Learn more about self-service password reset in the article, [How it works: Azure AD self-service password reset](concept-sspr-howitworks.md)</span></span>

<span data-ttu-id="6f3e1-128">Learn more about Azure Multi-Factor Authentication in the article, [How it works: Azure Multi-Factor Authentication](concept-mfa-howitworks.md)</span><span class="sxs-lookup"><span data-stu-id="6f3e1-128">Learn more about Azure Multi-Factor Authentication in the article, [How it works: Azure Multi-Factor Authentication](concept-mfa-howitworks.md)</span></span>