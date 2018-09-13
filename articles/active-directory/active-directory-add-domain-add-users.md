---
title: Assign users to a custom domain in Azure Active Directory | Microsoft Docs
description: How to populate a custom domain in Azure Active Directory with user accounts.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: curtand
ms.openlocfilehash: ae9af9d97f2cc61cb39645772b964ab62d01dac0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662143"
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="624e7-103">Assign users to a custom domain</span><span class="sxs-lookup"><span data-stu-id="624e7-103">Assign users to a custom domain</span></span>
<span data-ttu-id="624e7-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span><span class="sxs-lookup"><span data-stu-id="624e7-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

## <a name="users-synced-in-from-a-directory-on-your-corporate-network"></a><span data-ttu-id="624e7-105">Users synced in from a directory on your corporate network</span><span class="sxs-lookup"><span data-stu-id="624e7-105">Users synced in from a directory on your corporate network</span></span>
<span data-ttu-id="624e7-106">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span><span class="sxs-lookup"><span data-stu-id="624e7-106">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="624e7-107">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="624e7-107">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="624e7-108">Users added and managed in the cloud</span><span class="sxs-lookup"><span data-stu-id="624e7-108">Users added and managed in the cloud</span></span>
<span data-ttu-id="624e7-109">To change the domain for an existing user account:</span><span class="sxs-lookup"><span data-stu-id="624e7-109">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="624e7-110">Open the Azure classic portal using an account that is a global admin or a user admin.</span><span class="sxs-lookup"><span data-stu-id="624e7-110">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="624e7-111">Open your directory.</span><span class="sxs-lookup"><span data-stu-id="624e7-111">Open your directory.</span></span>
3. <span data-ttu-id="624e7-112">Select the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="624e7-112">Select the **Users** tab.</span></span>
4. <span data-ttu-id="624e7-113">Select the user from the list.</span><span class="sxs-lookup"><span data-stu-id="624e7-113">Select the user from the list.</span></span>
5. <span data-ttu-id="624e7-114">Change the domain for the user, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="624e7-114">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="624e7-115">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="624e7-115">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="624e7-116">Select a custom domain when creating a new user</span><span class="sxs-lookup"><span data-stu-id="624e7-116">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="624e7-117">Open the Azure classic portal using an account that is a global admin or a user admin.</span><span class="sxs-lookup"><span data-stu-id="624e7-117">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="624e7-118">Open your directory.</span><span class="sxs-lookup"><span data-stu-id="624e7-118">Open your directory.</span></span>
3. <span data-ttu-id="624e7-119">Select the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="624e7-119">Select the **Users** tab.</span></span>
4. <span data-ttu-id="624e7-120">In the command bar, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="624e7-120">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="624e7-121">When you add the user name, choose the custom domain from the domain list.</span><span class="sxs-lookup"><span data-stu-id="624e7-121">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="624e7-122">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="624e7-122">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="624e7-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="624e7-123">Next steps</span></span>
* [<span data-ttu-id="624e7-124">Using custom domain names to simplify the sign-in experience for your users</span><span class="sxs-lookup"><span data-stu-id="624e7-124">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="624e7-125">Manage custom domain names</span><span class="sxs-lookup"><span data-stu-id="624e7-125">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="624e7-126">Learn about domain management concepts in Azure AD</span><span class="sxs-lookup"><span data-stu-id="624e7-126">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

