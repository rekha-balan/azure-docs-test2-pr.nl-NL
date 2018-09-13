---
title: Azure Active Directory Reporting Notifications
description: How to use the Azure Active Directory reporting notifications for suspicious sign ins.
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2016
ms.author: dhanyahk;markvi
ms.openlocfilehash: 91b7a9cb1051355904cd44d10ff4ce72fd167020
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553863"
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="adc7b-103">Azure Active Directory Reporting Notifications</span><span class="sxs-lookup"><span data-stu-id="adc7b-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="adc7b-104">What reports generate email notifications</span><span class="sxs-lookup"><span data-stu-id="adc7b-104">What reports generate email notifications</span></span>
<span data-ttu-id="adc7b-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span><span class="sxs-lookup"><span data-stu-id="adc7b-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="adc7b-106">What is an "Irregular Sign in"?</span><span class="sxs-lookup"><span data-stu-id="adc7b-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="adc7b-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span><span class="sxs-lookup"><span data-stu-id="adc7b-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="adc7b-108">This may indicate that a hacker has been trying to sign in using this account.</span><span class="sxs-lookup"><span data-stu-id="adc7b-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="adc7b-109">Who receives the email notifications?</span><span class="sxs-lookup"><span data-stu-id="adc7b-109">Who receives the email notifications?</span></span>
<span data-ttu-id="adc7b-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span><span class="sxs-lookup"><span data-stu-id="adc7b-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="adc7b-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span><span class="sxs-lookup"><span data-stu-id="adc7b-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="adc7b-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span><span class="sxs-lookup"><span data-stu-id="adc7b-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="adc7b-113">How often are these emails sent?</span><span class="sxs-lookup"><span data-stu-id="adc7b-113">How often are these emails sent?</span></span>
<span data-ttu-id="adc7b-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span><span class="sxs-lookup"><span data-stu-id="adc7b-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="adc7b-115">How do I access the report mentioned in the email?</span><span class="sxs-lookup"><span data-stu-id="adc7b-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="adc7b-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="adc7b-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="adc7b-117">In order to access the report, you need to be both:</span><span class="sxs-lookup"><span data-stu-id="adc7b-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="adc7b-118">An admin or co-admin of your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="adc7b-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="adc7b-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span><span class="sxs-lookup"><span data-stu-id="adc7b-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="adc7b-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="adc7b-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="adc7b-121">Can I turn off these emails?</span><span class="sxs-lookup"><span data-stu-id="adc7b-121">Can I turn off these emails?</span></span>
<span data-ttu-id="adc7b-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span><span class="sxs-lookup"><span data-stu-id="adc7b-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="adc7b-123">What's next</span><span class="sxs-lookup"><span data-stu-id="adc7b-123">What's next</span></span>
* <span data-ttu-id="adc7b-124">Curious about what security, audit, and activity reports are available?</span><span class="sxs-lookup"><span data-stu-id="adc7b-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="adc7b-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="adc7b-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="adc7b-126">Getting started with Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="adc7b-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="adc7b-127">Add company branding to your Sign In and Access Panel pages</span><span class="sxs-lookup"><span data-stu-id="adc7b-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

