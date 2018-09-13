---
title: How to remove a user's access to an application | Microsoft Docs
description: Understand how to remove a user's access to an application
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
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: 732a305da377670b45f8b2f95bed741d82b4dae0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866717"
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="807d8-103">How to remove a user's access to an application</span><span class="sxs-lookup"><span data-stu-id="807d8-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="807d8-104">This article helps you to understand how to remove a user's access to an application.</span><span class="sxs-lookup"><span data-stu-id="807d8-104">This article helps you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="807d8-105">I want to remove a specific user’s or group’s assignment to an application</span><span class="sxs-lookup"><span data-stu-id="807d8-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="807d8-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="807d8-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="807d8-107">.## I want to disable all access to an application for every user</span><span class="sxs-lookup"><span data-stu-id="807d8-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="807d8-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="807d8-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="807d8-109">I want to delete an application entirely</span><span class="sxs-lookup"><span data-stu-id="807d8-109">I want to delete an application entirely</span></span>

<span data-ttu-id="807d8-110">To **delete an application**, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="807d8-110">To **delete an application**, follow these instructions:</span></span>

1.  <span data-ttu-id="807d8-111">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="807d8-111">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="807d8-112">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="807d8-112">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="807d8-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="807d8-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="807d8-114">Click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="807d8-114">Click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="807d8-115">Click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="807d8-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="807d8-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="807d8-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="807d8-117">Select the application you want to delete.</span><span class="sxs-lookup"><span data-stu-id="807d8-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="807d8-118">Once the application loads, click **Delete** icon from the top application’s **Overview** pane.</span><span class="sxs-lookup"><span data-stu-id="807d8-118">Once the application loads, click **Delete** icon from the top application’s **Overview** pane.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="807d8-119">I want to disable all future user consent operations to any application</span><span class="sxs-lookup"><span data-stu-id="807d8-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="807d8-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span><span class="sxs-lookup"><span data-stu-id="807d8-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="807d8-121">Administrators can still consent on user’s behalves.</span><span class="sxs-lookup"><span data-stu-id="807d8-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="807d8-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="807d8-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="807d8-123">To **disable all future user consent operations in your entire directory**, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="807d8-123">To **disable all future user consent operations in your entire directory**, follow these instructions:</span></span>

1.  <span data-ttu-id="807d8-124">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="807d8-124">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="807d8-125">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="807d8-125">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="807d8-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="807d8-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="807d8-127">Click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="807d8-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="807d8-128">Click **User settings**.</span><span class="sxs-lookup"><span data-stu-id="807d8-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="807d8-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="807d8-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="807d8-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="807d8-130">Next steps</span></span>
[<span data-ttu-id="807d8-131">Managing access to apps</span><span class="sxs-lookup"><span data-stu-id="807d8-131">Managing access to apps</span></span>](what-is-access-management.md)
