---
title: Enabling an Azure AD SSPR pilot
description: In this tutorial, you will enable Azure AD self-service password reset for a pilot group of users
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: a86547ad3eddb57328a2a0358ac453c979b84d37
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966564"
---
# <a name="tutorial-complete-an-azure-ad-self-service-password-reset-pilot-roll-out"></a><span data-ttu-id="46e6d-103">Tutorial: Complete an Azure AD self-service password reset pilot roll out</span><span class="sxs-lookup"><span data-stu-id="46e6d-103">Tutorial: Complete an Azure AD self-service password reset pilot roll out</span></span>

<span data-ttu-id="46e6d-104">In this tutorial, you will enable a pilot roll out of Azure AD self-service password reset (SSPR) in your organization and test using a non-administrator account.</span><span class="sxs-lookup"><span data-stu-id="46e6d-104">In this tutorial, you will enable a pilot roll out of Azure AD self-service password reset (SSPR) in your organization and test using a non-administrator account.</span></span>

<span data-ttu-id="46e6d-105">It is important that any testing of self-service password reset be done with non-administrator accounts.</span><span class="sxs-lookup"><span data-stu-id="46e6d-105">It is important that any testing of self-service password reset be done with non-administrator accounts.</span></span> <span data-ttu-id="46e6d-106">Microsoft manages the password reset policy for administrator accounts and requires the use of stronger authentication methods.</span><span class="sxs-lookup"><span data-stu-id="46e6d-106">Microsoft manages the password reset policy for administrator accounts and requires the use of stronger authentication methods.</span></span> <span data-ttu-id="46e6d-107">This policy does not allow the use of security questions and answers, and requires the use of two methods for reset.</span><span class="sxs-lookup"><span data-stu-id="46e6d-107">This policy does not allow the use of security questions and answers, and requires the use of two methods for reset.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46e6d-108">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="46e6d-108">Enable self-service password reset</span></span>
> * <span data-ttu-id="46e6d-109">Test SSPR as a user</span><span class="sxs-lookup"><span data-stu-id="46e6d-109">Test SSPR as a user</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46e6d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="46e6d-110">Prerequisites</span></span>

* <span data-ttu-id="46e6d-111">A Global Administrator account</span><span class="sxs-lookup"><span data-stu-id="46e6d-111">A Global Administrator account</span></span>

## <a name="enable-self-service-password-reset"></a><span data-ttu-id="46e6d-112">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="46e6d-112">Enable self-service password reset</span></span>

1. <span data-ttu-id="46e6d-113">Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.</span><span class="sxs-lookup"><span data-stu-id="46e6d-113">Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.</span></span>
1. <span data-ttu-id="46e6d-114">Browse to **Azure Active Directory** and select **Password reset**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-114">Browse to **Azure Active Directory** and select **Password reset**.</span></span>
1. <span data-ttu-id="46e6d-115">Start with a pilot group by enabling self-service password for a subset of users in your organization.</span><span class="sxs-lookup"><span data-stu-id="46e6d-115">Start with a pilot group by enabling self-service password for a subset of users in your organization.</span></span>
   * <span data-ttu-id="46e6d-116">From the **Properties** page, under the option **Self Service Password Reset Enabled**, choose **Selected** and pick a pilot group.</span><span class="sxs-lookup"><span data-stu-id="46e6d-116">From the **Properties** page, under the option **Self Service Password Reset Enabled**, choose **Selected** and pick a pilot group.</span></span>
      * <span data-ttu-id="46e6d-117">Only members of the specific Azure AD group that you choose can use the SSPR functionality.</span><span class="sxs-lookup"><span data-stu-id="46e6d-117">Only members of the specific Azure AD group that you choose can use the SSPR functionality.</span></span> <span data-ttu-id="46e6d-118">We recommend that you define a group of users and use this setting when you deploy this functionality for a proof of concept.</span><span class="sxs-lookup"><span data-stu-id="46e6d-118">We recommend that you define a group of users and use this setting when you deploy this functionality for a proof of concept.</span></span> <span data-ttu-id="46e6d-119">Nesting of security groups is supported here.</span><span class="sxs-lookup"><span data-stu-id="46e6d-119">Nesting of security groups is supported here.</span></span>
      * <span data-ttu-id="46e6d-120">Ensure the users in the group you picked have been appropriately licensed.</span><span class="sxs-lookup"><span data-stu-id="46e6d-120">Ensure the users in the group you picked have been appropriately licensed.</span></span>
   * <span data-ttu-id="46e6d-121">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="46e6d-121">Click **Save**</span></span>
1. <span data-ttu-id="46e6d-122">On the **Authentication methods** page</span><span class="sxs-lookup"><span data-stu-id="46e6d-122">On the **Authentication methods** page</span></span>
   * <span data-ttu-id="46e6d-123">Set the **Number of methods required to reset** to **2**</span><span class="sxs-lookup"><span data-stu-id="46e6d-123">Set the **Number of methods required to reset** to **2**</span></span>
   * <span data-ttu-id="46e6d-124">Choose which **Methods available to users** your organization wants to allow.</span><span class="sxs-lookup"><span data-stu-id="46e6d-124">Choose which **Methods available to users** your organization wants to allow.</span></span> <span data-ttu-id="46e6d-125">For this tutorial check the boxes to enable **Email**, **Mobile phone**, and **Office phone**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-125">For this tutorial check the boxes to enable **Email**, **Mobile phone**, and **Office phone**.</span></span>
   * <span data-ttu-id="46e6d-126">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="46e6d-126">Click **Save**</span></span>
1. <span data-ttu-id="46e6d-127">On the **Registration** page</span><span class="sxs-lookup"><span data-stu-id="46e6d-127">On the **Registration** page</span></span>
   * <span data-ttu-id="46e6d-128">Select **Yes** for **Require users to register when signing in**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-128">Select **Yes** for **Require users to register when signing in**.</span></span>
   * <span data-ttu-id="46e6d-129">Set **Number of days before users are asked to reconfirm their authentication information** to **180**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-129">Set **Number of days before users are asked to reconfirm their authentication information** to **180**.</span></span>
   * <span data-ttu-id="46e6d-130">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="46e6d-130">Click **Save**</span></span>
1. <span data-ttu-id="46e6d-131">On the **Notifications** page</span><span class="sxs-lookup"><span data-stu-id="46e6d-131">On the **Notifications** page</span></span>
   * <span data-ttu-id="46e6d-132">Set **Notify users on password resets** option to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-132">Set **Notify users on password resets** option to **Yes**.</span></span>
   * <span data-ttu-id="46e6d-133">Set **Notify all admins when other admins reset their password** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-133">Set **Notify all admins when other admins reset their password** to **Yes**.</span></span>
1. <span data-ttu-id="46e6d-134">On the **Customization** page</span><span class="sxs-lookup"><span data-stu-id="46e6d-134">On the **Customization** page</span></span>
   * <span data-ttu-id="46e6d-135">Microsoft recommends that you set **Customize helpdesk link** to **Yes** and provide either an email address or web page URL where your users can get additional help from your organization in the **Custom helpdesk email or URL** field.</span><span class="sxs-lookup"><span data-stu-id="46e6d-135">Microsoft recommends that you set **Customize helpdesk link** to **Yes** and provide either an email address or web page URL where your users can get additional help from your organization in the **Custom helpdesk email or URL** field.</span></span>
   * <span data-ttu-id="46e6d-136">For this tutorial we will leave **Customize helpdesk link** set to **No**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-136">For this tutorial we will leave **Customize helpdesk link** set to **No**.</span></span>

<span data-ttu-id="46e6d-137">Self-service password reset is now configured for cloud users in your pilot group.</span><span class="sxs-lookup"><span data-stu-id="46e6d-137">Self-service password reset is now configured for cloud users in your pilot group.</span></span>

## <a name="test-sspr-as-a-user"></a><span data-ttu-id="46e6d-138">Test SSPR as a user</span><span class="sxs-lookup"><span data-stu-id="46e6d-138">Test SSPR as a user</span></span>

<span data-ttu-id="46e6d-139">Test self-service password reset using a non-administrator test user that is a member of your pilot group.</span><span class="sxs-lookup"><span data-stu-id="46e6d-139">Test self-service password reset using a non-administrator test user that is a member of your pilot group.</span></span> <span data-ttu-id="46e6d-140">**Be aware that if you use an account that has any administrator roles assigned to it the authentication methods and number may be different than what you selected as Microsoft manages the administrator policy.**</span><span class="sxs-lookup"><span data-stu-id="46e6d-140">**Be aware that if you use an account that has any administrator roles assigned to it the authentication methods and number may be different than what you selected as Microsoft manages the administrator policy.**</span></span>

1. <span data-ttu-id="46e6d-141">Open a new InPrivate or incognito mode browser window.</span><span class="sxs-lookup"><span data-stu-id="46e6d-141">Open a new InPrivate or incognito mode browser window.</span></span>
1. <span data-ttu-id="46e6d-142">Using a test user register for self-service password reset using the registration portal located at [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="46e6d-142">Using a test user register for self-service password reset using the registration portal located at [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).</span></span>
1. <span data-ttu-id="46e6d-143">Using the same test user browse to the self-service password reset portal [https://aka.ms/sspr](https://aka.ms/sspr) and attempt to reset your password using the information you provided in the previous step.</span><span class="sxs-lookup"><span data-stu-id="46e6d-143">Using the same test user browse to the self-service password reset portal [https://aka.ms/sspr](https://aka.ms/sspr) and attempt to reset your password using the information you provided in the previous step.</span></span>
1. <span data-ttu-id="46e6d-144">You should be able to successfully reset your password.</span><span class="sxs-lookup"><span data-stu-id="46e6d-144">You should be able to successfully reset your password.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="46e6d-145">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="46e6d-145">Clean up resources</span></span>

<span data-ttu-id="46e6d-146">If you decide you no longer want to use the functionality you have configured as part of this tutorial, make the following change.</span><span class="sxs-lookup"><span data-stu-id="46e6d-146">If you decide you no longer want to use the functionality you have configured as part of this tutorial, make the following change.</span></span>

1. <span data-ttu-id="46e6d-147">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46e6d-147">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="46e6d-148">Browse to **Azure Active Directory** and select **Password reset**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-148">Browse to **Azure Active Directory** and select **Password reset**.</span></span>
1. <span data-ttu-id="46e6d-149">From the **Properties** page, under the option **Self Service Password Reset Enabled**, choose **None**.</span><span class="sxs-lookup"><span data-stu-id="46e6d-149">From the **Properties** page, under the option **Self Service Password Reset Enabled**, choose **None**.</span></span>
1. <span data-ttu-id="46e6d-150">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="46e6d-150">Click **Save**</span></span>

## <a name="next-steps"></a><span data-ttu-id="46e6d-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="46e6d-151">Next steps</span></span>

<span data-ttu-id="46e6d-152">In this tutorial, you have enabled Azure AD self-service password reset.</span><span class="sxs-lookup"><span data-stu-id="46e6d-152">In this tutorial, you have enabled Azure AD self-service password reset.</span></span> <span data-ttu-id="46e6d-153">Continue on to the next tutorial to see how an on-premises Active Directory Domain Services infrastructure can be integrated into the self-service password reset experience.</span><span class="sxs-lookup"><span data-stu-id="46e6d-153">Continue on to the next tutorial to see how an on-premises Active Directory Domain Services infrastructure can be integrated into the self-service password reset experience.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46e6d-154">Enable SSPR on-premises writeback integration</span><span class="sxs-lookup"><span data-stu-id="46e6d-154">Enable SSPR on-premises writeback integration</span></span>](tutorial-enable-writeback.md)
