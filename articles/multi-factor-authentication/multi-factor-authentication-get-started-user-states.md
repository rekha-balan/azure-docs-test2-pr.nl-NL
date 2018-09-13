---
title: Microsoft Azure Multi-Factor Authentication User States
description: Learn about user states in Azure MFA.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: curtand
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: kgremban
ms.openlocfilehash: 0bbd4f7e44630ee2dd3908ad4ff969321512b7f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671141"
---
# <a name="user-states-in-azure-multi-factor-authentication"></a><span data-ttu-id="aa567-103">User States in Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="aa567-103">User States in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="aa567-104">User accounts in Azure Multi-Factor Authentication have the following three distinct states:</span><span class="sxs-lookup"><span data-stu-id="aa567-104">User accounts in Azure Multi-Factor Authentication have the following three distinct states:</span></span>

| <span data-ttu-id="aa567-105">State</span><span class="sxs-lookup"><span data-stu-id="aa567-105">State</span></span> | <span data-ttu-id="aa567-106">Description</span><span class="sxs-lookup"><span data-stu-id="aa567-106">Description</span></span> | <span data-ttu-id="aa567-107">Non-browser apps affected</span><span class="sxs-lookup"><span data-stu-id="aa567-107">Non-browser apps affected</span></span> | 
|:---:|:---:|:---:|
| <span data-ttu-id="aa567-108">Disabled</span><span class="sxs-lookup"><span data-stu-id="aa567-108">Disabled</span></span> |<span data-ttu-id="aa567-109">The default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="aa567-109">The default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span></span> |<span data-ttu-id="aa567-110">No</span><span class="sxs-lookup"><span data-stu-id="aa567-110">No</span></span> |
| <span data-ttu-id="aa567-111">Enabled</span><span class="sxs-lookup"><span data-stu-id="aa567-111">Enabled</span></span> |<span data-ttu-id="aa567-112">The user has been enrolled in Azure MFA, but has not registered.</span><span class="sxs-lookup"><span data-stu-id="aa567-112">The user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="aa567-113">They will be prompted to register the next time they sign in.</span><span class="sxs-lookup"><span data-stu-id="aa567-113">They will be prompted to register the next time they sign in.</span></span> |<span data-ttu-id="aa567-114">No.</span><span class="sxs-lookup"><span data-stu-id="aa567-114">No.</span></span>  <span data-ttu-id="aa567-115">They continue to work until the registration process is completed.</span><span class="sxs-lookup"><span data-stu-id="aa567-115">They continue to work until the registration process is completed.</span></span> |
| <span data-ttu-id="aa567-116">Enforced</span><span class="sxs-lookup"><span data-stu-id="aa567-116">Enforced</span></span> |<span data-ttu-id="aa567-117">The user has been enrolled and has completed the registration process for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="aa567-117">The user has been enrolled and has completed the registration process for Azure MFA.</span></span> |<span data-ttu-id="aa567-118">Yes.</span><span class="sxs-lookup"><span data-stu-id="aa567-118">Yes.</span></span>  <span data-ttu-id="aa567-119">Apps require app passwords.</span><span class="sxs-lookup"><span data-stu-id="aa567-119">Apps require app passwords.</span></span> |

## <a name="changing-a-user-state"></a><span data-ttu-id="aa567-120">Changing a user state</span><span class="sxs-lookup"><span data-stu-id="aa567-120">Changing a user state</span></span>
<span data-ttu-id="aa567-121">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed the registration process.</span><span class="sxs-lookup"><span data-stu-id="aa567-121">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed the registration process.</span></span>

<span data-ttu-id="aa567-122">All users start out *disabled*.</span><span class="sxs-lookup"><span data-stu-id="aa567-122">All users start out *disabled*.</span></span> <span data-ttu-id="aa567-123">When you enroll users in Azure MFA, their state changes *enabled*.</span><span class="sxs-lookup"><span data-stu-id="aa567-123">When you enroll users in Azure MFA, their state changes *enabled*.</span></span> <span data-ttu-id="aa567-124">When enabled users sign in and complete the registration process, their state changes to *enforced*.</span><span class="sxs-lookup"><span data-stu-id="aa567-124">When enabled users sign in and complete the registration process, their state changes to *enforced*.</span></span>  

### <a name="view-user-states"></a><span data-ttu-id="aa567-125">View user states</span><span class="sxs-lookup"><span data-stu-id="aa567-125">View user states</span></span>

<span data-ttu-id="aa567-126">Use the following steps to access the page where you can view and manage user states:</span><span class="sxs-lookup"><span data-stu-id="aa567-126">Use the following steps to access the page where you can view and manage user states:</span></span>

1. <span data-ttu-id="aa567-127">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="aa567-127">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="aa567-128">On the left, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa567-128">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="aa567-129">Select the directory for the user you wish to view.</span><span class="sxs-lookup"><span data-stu-id="aa567-129">Select the directory for the user you wish to view.</span></span>
   <span data-ttu-id="aa567-130">![Select directory - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/directory1.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-130">![Select directory - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/directory1.png)</span></span>
4. <span data-ttu-id="aa567-131">Select **Users**.</span><span class="sxs-lookup"><span data-stu-id="aa567-131">Select **Users**.</span></span>
5. <span data-ttu-id="aa567-132">At the bottom of the page, select **Manage Multi-Factor Auth**. ![Select Manage multi-factor auth - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/manage1.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-132">At the bottom of the page, select **Manage Multi-Factor Auth**. ![Select Manage multi-factor auth - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/manage1.png)</span></span>
6. <span data-ttu-id="aa567-133">A new tab, which displays the user states, opens.</span><span class="sxs-lookup"><span data-stu-id="aa567-133">A new tab, which displays the user states, opens.</span></span>
   <span data-ttu-id="aa567-134">![multi-factor authentication user status - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-user-states/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-134">![multi-factor authentication user status - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-user-states/userstate1.png)</span></span>

### <a name="change-the-state-from-disabled-to-enabled"></a><span data-ttu-id="aa567-135">Change the state from disabled to enabled</span><span class="sxs-lookup"><span data-stu-id="aa567-135">Change the state from disabled to enabled</span></span>

1. <span data-ttu-id="aa567-136">Use the preceding steps to get to the multi-factor authentication users page.</span><span class="sxs-lookup"><span data-stu-id="aa567-136">Use the preceding steps to get to the multi-factor authentication users page.</span></span> 
2. <span data-ttu-id="aa567-137">Find the user that you want to enable for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="aa567-137">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="aa567-138">You may need to change the view at the top.</span><span class="sxs-lookup"><span data-stu-id="aa567-138">You may need to change the view at the top.</span></span> <span data-ttu-id="aa567-139">Ensure that the status is **disabled**.</span><span class="sxs-lookup"><span data-stu-id="aa567-139">Ensure that the status is **disabled**.</span></span>
   <span data-ttu-id="aa567-140">![Find user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-140">![Find user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
3. <span data-ttu-id="aa567-141">Check the box next to their name.</span><span class="sxs-lookup"><span data-stu-id="aa567-141">Check the box next to their name.</span></span>
4. <span data-ttu-id="aa567-142">On the right, under quick steps, click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="aa567-142">On the right, under quick steps, click **Enable**.</span></span>
   <span data-ttu-id="aa567-143">![Enable selected user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-143">![Enable selected user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>
5. <span data-ttu-id="aa567-144">Select **enable multi-factor auth**. ![Enable multi-factor auth - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable2.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-144">Select **enable multi-factor auth**. ![Enable multi-factor auth - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable2.png)</span></span>
6. <span data-ttu-id="aa567-145">Notice the user's state has changed from **disabled** to **enabled**.</span><span class="sxs-lookup"><span data-stu-id="aa567-145">Notice the user's state has changed from **disabled** to **enabled**.</span></span>
   <span data-ttu-id="aa567-146">![See that user is now enabled - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-146">![See that user is now enabled - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user.png)</span></span>

<span data-ttu-id="aa567-147">After you enable users, you should notify them via email.</span><span class="sxs-lookup"><span data-stu-id="aa567-147">After you enable users, you should notify them via email.</span></span> <span data-ttu-id="aa567-148">Include the fact that they'll be asked to register the next time they sign in, and that some non-browser apps may not work with two-step verification.</span><span class="sxs-lookup"><span data-stu-id="aa567-148">Include the fact that they'll be asked to register the next time they sign in, and that some non-browser apps may not work with two-step verification.</span></span> <span data-ttu-id="aa567-149">You can also include a link to our [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) to help them get started.</span><span class="sxs-lookup"><span data-stu-id="aa567-149">You can also include a link to our [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) to help them get started.</span></span> 

### <a name="to-change-the-state-from-enabledenforced-to-disabled"></a><span data-ttu-id="aa567-150">To change the state from enabled/enforced to disabled</span><span class="sxs-lookup"><span data-stu-id="aa567-150">To change the state from enabled/enforced to disabled</span></span>

1. <span data-ttu-id="aa567-151">Use the steps in [View user states](#view-user-states) to get to the multi-factor authentication users page.</span><span class="sxs-lookup"><span data-stu-id="aa567-151">Use the steps in [View user states](#view-user-states) to get to the multi-factor authentication users page.</span></span>
6. <span data-ttu-id="aa567-152">Find the user that you want to disable.</span><span class="sxs-lookup"><span data-stu-id="aa567-152">Find the user that you want to disable.</span></span> <span data-ttu-id="aa567-153">You may need to change the view at the top.</span><span class="sxs-lookup"><span data-stu-id="aa567-153">You may need to change the view at the top.</span></span> <span data-ttu-id="aa567-154">Ensure that the status is either **enabled** or **enforced**.</span><span class="sxs-lookup"><span data-stu-id="aa567-154">Ensure that the status is either **enabled** or **enforced**.</span></span>
7. <span data-ttu-id="aa567-155">Check the box next to their name.</span><span class="sxs-lookup"><span data-stu-id="aa567-155">Check the box next to their name.</span></span>
8. <span data-ttu-id="aa567-156">On the right, under quick steps, click **Disable**.</span><span class="sxs-lookup"><span data-stu-id="aa567-156">On the right, under quick steps, click **Disable**.</span></span>
   <span data-ttu-id="aa567-157">![Disable user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-user-states/userstate2.png)</span><span class="sxs-lookup"><span data-stu-id="aa567-157">![Disable user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-user-states/userstate2.png)</span></span>
9. <span data-ttu-id="aa567-158">You are prompted to confirm the action.</span><span class="sxs-lookup"><span data-stu-id="aa567-158">You are prompted to confirm the action.</span></span> <span data-ttu-id="aa567-159">Click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="aa567-159">Click **Yes**.</span></span>
10. <span data-ttu-id="aa567-160">If the user was successfully disabled, you receive a success message.</span><span class="sxs-lookup"><span data-stu-id="aa567-160">If the user was successfully disabled, you receive a success message.</span></span> <span data-ttu-id="aa567-161">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="aa567-161">Click **Close**.</span></span>









