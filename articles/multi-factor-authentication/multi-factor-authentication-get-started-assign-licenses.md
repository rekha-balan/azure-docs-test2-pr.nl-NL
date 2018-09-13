---
title: Assign icenses for Azure MFA | Microsoft Docs
description: Learn how to assign user licenses for Microsoft Azure Multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/13/2017
ms.author: kgremban
ROBOTS: NOINDEX
ms.openlocfilehash: 566d268d682b7471ea5162a436397122430095c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562748"
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="231a1-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span><span class="sxs-lookup"><span data-stu-id="231a1-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="231a1-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span><span class="sxs-lookup"><span data-stu-id="231a1-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="231a1-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span><span class="sxs-lookup"><span data-stu-id="231a1-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="231a1-106">To assign a license</span><span class="sxs-lookup"><span data-stu-id="231a1-106">To assign a license</span></span>
1. <span data-ttu-id="231a1-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="231a1-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="231a1-108">On the left, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="231a1-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="231a1-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span><span class="sxs-lookup"><span data-stu-id="231a1-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="231a1-110">At the top of the directory page, select **Licenses**.</span><span class="sxs-lookup"><span data-stu-id="231a1-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="231a1-111">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="231a1-111">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="231a1-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="231a1-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="231a1-113">If you only have one, then it should be selected automatically.</span><span class="sxs-lookup"><span data-stu-id="231a1-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="231a1-114">At the bottom of the page, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="231a1-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="231a1-115">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="231a1-115">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="231a1-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span><span class="sxs-lookup"><span data-stu-id="231a1-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="231a1-117">You should see a green check mark appear.</span><span class="sxs-lookup"><span data-stu-id="231a1-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="231a1-118">Click the check mark icon to save the changes.</span><span class="sxs-lookup"><span data-stu-id="231a1-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="231a1-119">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="231a1-119">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="231a1-120">You should see a message saying how many licenses were assigned and how many may have failed.</span><span class="sxs-lookup"><span data-stu-id="231a1-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="231a1-121">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="231a1-121">Click **Ok**.</span></span>
   <span data-ttu-id="231a1-122">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="231a1-122">![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="231a1-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="231a1-123">Next steps</span></span>

- <span data-ttu-id="231a1-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="231a1-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>



