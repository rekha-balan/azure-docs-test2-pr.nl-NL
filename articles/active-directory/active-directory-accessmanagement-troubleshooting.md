---
title: Troubleshooting dynamic membership for groups | Microsoft Docs
description: Troubleshooting tips for dynamic membership for groups in Azure AD.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 27f8d329c0dddd21cca7e3631594ab326f3610b2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551966"
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="85b13-103">Troubleshooting dynamic memberships for groups</span><span class="sxs-lookup"><span data-stu-id="85b13-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="85b13-104">**I configured a rule on a group but no memberships get updated in the group**</span><span class="sxs-lookup"><span data-stu-id="85b13-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="85b13-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab. You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span><span class="sxs-lookup"><span data-stu-id="85b13-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab. You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="85b13-106">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span><span class="sxs-lookup"><span data-stu-id="85b13-106">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="85b13-107">**I configured a rule, but now the existing members of the rule are removed**</span><span class="sxs-lookup"><span data-stu-id="85b13-107">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="85b13-108">This is expected behavior.</span><span class="sxs-lookup"><span data-stu-id="85b13-108">This is expected behavior.</span></span> <span data-ttu-id="85b13-109">Existing members of the group are removed when a rule is enabled or changed.</span><span class="sxs-lookup"><span data-stu-id="85b13-109">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="85b13-110">The users returned from evaluation of the rule are added as members to the group.</span><span class="sxs-lookup"><span data-stu-id="85b13-110">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="85b13-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span><span class="sxs-lookup"><span data-stu-id="85b13-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="85b13-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span><span class="sxs-lookup"><span data-stu-id="85b13-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="85b13-113">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span><span class="sxs-lookup"><span data-stu-id="85b13-113">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="85b13-114">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span><span class="sxs-lookup"><span data-stu-id="85b13-114">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="85b13-115">Directories with a large number of users can take 30 minutes or longer to populate.</span><span class="sxs-lookup"><span data-stu-id="85b13-115">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="85b13-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="85b13-116">Next steps</span></span>
<span data-ttu-id="85b13-117">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85b13-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="85b13-118">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="85b13-118">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="85b13-119">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85b13-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="85b13-120">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85b13-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="85b13-121">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85b13-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
