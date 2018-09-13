---
title: How to use self-service application access | Microsoft Docs
description: Enable self-service application access to allow users to find their own applications
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
ms.topic: article
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewer: japere,asteen
ms.openlocfilehash: 4936c6a0c7323ff5b607519c6d86c2428d7003bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869859"
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="982dc-103">How to use self-service application access</span><span class="sxs-lookup"><span data-stu-id="982dc-103">How to use self-service application access</span></span>

<span data-ttu-id="982dc-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span><span class="sxs-lookup"><span data-stu-id="982dc-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="982dc-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="982dc-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="982dc-106">Using this feature, you can:</span><span class="sxs-lookup"><span data-stu-id="982dc-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="982dc-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span><span class="sxs-lookup"><span data-stu-id="982dc-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="982dc-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span><span class="sxs-lookup"><span data-stu-id="982dc-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="982dc-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span><span class="sxs-lookup"><span data-stu-id="982dc-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="982dc-110">Optionally configure up to 10 individuals who may approve access to this application.</span><span class="sxs-lookup"><span data-stu-id="982dc-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="982dc-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="982dc-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="982dc-112">Optionally automatically assign self-service assigned users to an application role directly.</span><span class="sxs-lookup"><span data-stu-id="982dc-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="982dc-113">Enable self-service application access to allow users to find their own applications</span><span class="sxs-lookup"><span data-stu-id="982dc-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="982dc-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span><span class="sxs-lookup"><span data-stu-id="982dc-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="982dc-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span><span class="sxs-lookup"><span data-stu-id="982dc-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="982dc-116">To enable self-service application access to an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="982dc-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="982dc-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="982dc-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="982dc-118">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="982dc-118">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="982dc-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="982dc-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="982dc-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="982dc-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="982dc-121">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="982dc-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="982dc-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="982dc-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="982dc-123">Select the application you want to enable Self-service access to from the list.</span><span class="sxs-lookup"><span data-stu-id="982dc-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="982dc-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="982dc-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="982dc-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span><span class="sxs-lookup"><span data-stu-id="982dc-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="982dc-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span><span class="sxs-lookup"><span data-stu-id="982dc-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="982dc-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="982dc-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="982dc-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="982dc-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="982dc-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span><span class="sxs-lookup"><span data-stu-id="982dc-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="982dc-130">Groups are not supported.</span><span class="sxs-lookup"><span data-stu-id="982dc-130">Groups are not supported.</span></span>

13. <span data-ttu-id="982dc-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span><span class="sxs-lookup"><span data-stu-id="982dc-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="982dc-132">Click the **Save** button at the top of the blade to finish.</span><span class="sxs-lookup"><span data-stu-id="982dc-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="982dc-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span><span class="sxs-lookup"><span data-stu-id="982dc-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="982dc-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="982dc-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="982dc-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span><span class="sxs-lookup"><span data-stu-id="982dc-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="982dc-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span><span class="sxs-lookup"><span data-stu-id="982dc-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="982dc-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="982dc-137">Next steps</span></span>
[<span data-ttu-id="982dc-138">Setting up Azure Active Directory for self-service group management</span><span class="sxs-lookup"><span data-stu-id="982dc-138">Setting up Azure Active Directory for self-service group management</span></span>](../users-groups-roles/groups-self-service-management.md)
