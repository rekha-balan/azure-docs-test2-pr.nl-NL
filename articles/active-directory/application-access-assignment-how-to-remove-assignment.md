---
title: How to remove a user's access to an application | Microsoft Docs
description: Understand how to remove a user's access to an application
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 8d4f2cec35a8edfec9b8830a077b8aa65ca0c229
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552611"
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="79ff6-103">How to remove a user's access to an application</span><span class="sxs-lookup"><span data-stu-id="79ff6-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="79ff6-104">This article help you to understand how to remove a user's access to an application.</span><span class="sxs-lookup"><span data-stu-id="79ff6-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="79ff6-105">I want to remove a specific user’s or group’s assignment to an application</span><span class="sxs-lookup"><span data-stu-id="79ff6-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="79ff6-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="79ff6-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="79ff6-107">.## I want to disable all access to an application for every user</span><span class="sxs-lookup"><span data-stu-id="79ff6-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="79ff6-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="79ff6-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="79ff6-109">I want to delete an application entirely</span><span class="sxs-lookup"><span data-stu-id="79ff6-109">I want to delete an application entirely</span></span>

<span data-ttu-id="79ff6-110">To **delete an application**, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="79ff6-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="79ff6-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="79ff6-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="79ff6-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="79ff6-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="79ff6-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="79ff6-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="79ff6-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="79ff6-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="79ff6-115">Click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="79ff6-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="79ff6-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="79ff6-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="79ff6-117">Select the application you want to delete.</span><span class="sxs-lookup"><span data-stu-id="79ff6-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="79ff6-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span><span class="sxs-lookup"><span data-stu-id="79ff6-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="79ff6-119">I want to disable all future user consent operations to any application</span><span class="sxs-lookup"><span data-stu-id="79ff6-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="79ff6-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span><span class="sxs-lookup"><span data-stu-id="79ff6-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="79ff6-121">Administrators can still consent on user’s behalves.</span><span class="sxs-lookup"><span data-stu-id="79ff6-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="79ff6-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="79ff6-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="79ff6-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="79ff6-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="79ff6-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="79ff6-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="79ff6-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="79ff6-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="79ff6-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="79ff6-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="79ff6-127">Click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="79ff6-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="79ff6-128">Click **User settings**.</span><span class="sxs-lookup"><span data-stu-id="79ff6-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="79ff6-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="79ff6-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="79ff6-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="79ff6-130">Next steps</span></span>
[<span data-ttu-id="79ff6-131">Managing access to apps</span><span class="sxs-lookup"><span data-stu-id="79ff6-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
