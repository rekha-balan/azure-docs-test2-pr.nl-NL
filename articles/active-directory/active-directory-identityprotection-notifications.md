---
title: Azure Active Directory Identity Protection notifications| Microsoft Docs
description: Learn how notifications support your investigation activities.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/09/2017
ms.author: markvi
ms.openlocfilehash: e1c99798f58a7d434116103b30652a098edd7aa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553815"
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="062b0-104">Azure Active Directory Identity Protection notifications</span><span class="sxs-lookup"><span data-stu-id="062b0-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="062b0-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span><span class="sxs-lookup"><span data-stu-id="062b0-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="062b0-106">User compromised alert email</span><span class="sxs-lookup"><span data-stu-id="062b0-106">User compromised alert email</span></span>
* <span data-ttu-id="062b0-107">Weekly digest email</span><span class="sxs-lookup"><span data-stu-id="062b0-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="062b0-108">User compromised alert email</span><span class="sxs-lookup"><span data-stu-id="062b0-108">User compromised alert email</span></span>
<span data-ttu-id="062b0-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span><span class="sxs-lookup"><span data-stu-id="062b0-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="062b0-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span><span class="sxs-lookup"><span data-stu-id="062b0-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="062b0-111">We recommend that you immediately investigate notifications of compromised accounts.</span><span class="sxs-lookup"><span data-stu-id="062b0-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="062b0-112">Weekly digest email</span><span class="sxs-lookup"><span data-stu-id="062b0-112">Weekly digest email</span></span>
<span data-ttu-id="062b0-113">The weekly digest email contains a summary of new risk events.</span><span class="sxs-lookup"><span data-stu-id="062b0-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="062b0-114">It includes:</span><span class="sxs-lookup"><span data-stu-id="062b0-114">It includes:</span></span>

* <span data-ttu-id="062b0-115">Users at risk</span><span class="sxs-lookup"><span data-stu-id="062b0-115">Users at risk</span></span>
* <span data-ttu-id="062b0-116">Suspicious activities</span><span class="sxs-lookup"><span data-stu-id="062b0-116">Suspicious activities</span></span>
* <span data-ttu-id="062b0-117">Detected vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="062b0-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="062b0-118">Links to the related reports in Identity Protection</span><span class="sxs-lookup"><span data-stu-id="062b0-118">Links to the related reports in Identity Protection</span></span>

<br>
<span data-ttu-id="062b0-119">![Remediation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/400.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="062b0-119">![Remediation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/400.png "Remediation")</span></span>
<br>

<span data-ttu-id="062b0-120">You can switch sending a weekly digest email off.</span><span class="sxs-lookup"><span data-stu-id="062b0-120">You can switch sending a weekly digest email off.</span></span>
<br><br>
<span data-ttu-id="062b0-121">![User risks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/62.png "User risks")</span><span class="sxs-lookup"><span data-stu-id="062b0-121">![User risks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/62.png "User risks")</span></span>
<br>

<span data-ttu-id="062b0-122">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="062b0-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="062b0-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="062b0-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br>
   <span data-ttu-id="062b0-124">![User risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/401.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="062b0-124">![User risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/401.png "User risk policy")</span></span>
   <br>
2. <span data-ttu-id="062b0-125">In the **General** section, click **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="062b0-125">In the **General** section, click **Notifications**.</span></span>
   <br><br>
   <span data-ttu-id="062b0-126">![User risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/405.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="062b0-126">![User risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/405.png "User risk policy")</span></span>
   <br>

## <a name="see-also"></a><span data-ttu-id="062b0-127">See also</span><span class="sxs-lookup"><span data-stu-id="062b0-127">See also</span></span>
* [<span data-ttu-id="062b0-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="062b0-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)




