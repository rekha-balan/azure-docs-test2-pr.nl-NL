---
title: Quickstart Azure AD self-service password reset
description: In this quickstart, you will quickly configure Azure AD self-service password reset to allow users to reset their own passwords
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: quickstart
ms.date: 07/17/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: c40cb3192d514d990ea2a5d66e1484ff204e9b10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864899"
---
# <a name="quickstart-self-service-password-reset"></a><span data-ttu-id="d798f-103">Quickstart: Self-service password reset</span><span class="sxs-lookup"><span data-stu-id="d798f-103">Quickstart: Self-service password reset</span></span>

<span data-ttu-id="d798f-104">In this quickstart, you walk through configuring self-service password reset (SSPR) as a simple means for IT administrators to enable users to reset their passwords or unlock their accounts.</span><span class="sxs-lookup"><span data-stu-id="d798f-104">In this quickstart, you walk through configuring self-service password reset (SSPR) as a simple means for IT administrators to enable users to reset their passwords or unlock their accounts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d798f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d798f-105">Prerequisites</span></span>

* <span data-ttu-id="d798f-106">A working Azure AD tenant with at least a trial license enabled.</span><span class="sxs-lookup"><span data-stu-id="d798f-106">A working Azure AD tenant with at least a trial license enabled.</span></span>
* <span data-ttu-id="d798f-107">An account with Global Administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="d798f-107">An account with Global Administrator privileges.</span></span>
* <span data-ttu-id="d798f-108">A non-administrator test user with a password you know, if you need to create a user see the article [Quickstart: Add new users to Azure Active Directory](../add-users-azure-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d798f-108">A non-administrator test user with a password you know, if you need to create a user see the article [Quickstart: Add new users to Azure Active Directory](../add-users-azure-active-directory.md).</span></span>
* <span data-ttu-id="d798f-109">A pilot group to test with that the non-administrator test user is a member of, if you need to create a group see the article [Create a group and add members in Azure Active Directory](../active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d798f-109">A pilot group to test with that the non-administrator test user is a member of, if you need to create a group see the article [Create a group and add members in Azure Active Directory](../active-directory-groups-create-azure-portal.md).</span></span>

## <a name="enable-self-service-password-reset"></a><span data-ttu-id="d798f-110">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="d798f-110">Enable self-service password reset</span></span>

> [!VIDEO https://www.youtube.com/embed/Pa0eyqjEjvQ]

1. <span data-ttu-id="d798f-111">From your existing Azure AD tenant, on the **Azure portal** under **Azure Active Directory** select **Password reset**.</span><span class="sxs-lookup"><span data-stu-id="d798f-111">From your existing Azure AD tenant, on the **Azure portal** under **Azure Active Directory** select **Password reset**.</span></span>

2. <span data-ttu-id="d798f-112">From the **Properties** page, under the option **Self Service Password Reset Enabled**, choose **Selected**.</span><span class="sxs-lookup"><span data-stu-id="d798f-112">From the **Properties** page, under the option **Self Service Password Reset Enabled**, choose **Selected**.</span></span>
    * <span data-ttu-id="d798f-113">From **Select group**, choose your pilot group created as part of the prerequisites section of this article.</span><span class="sxs-lookup"><span data-stu-id="d798f-113">From **Select group**, choose your pilot group created as part of the prerequisites section of this article.</span></span>
    * <span data-ttu-id="d798f-114">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d798f-114">Click **Save**.</span></span>

3. <span data-ttu-id="d798f-115">From the **Authentication methods** page, make the following choices:</span><span class="sxs-lookup"><span data-stu-id="d798f-115">From the **Authentication methods** page, make the following choices:</span></span>
   * <span data-ttu-id="d798f-116">Number of methods required to reset: **1**</span><span class="sxs-lookup"><span data-stu-id="d798f-116">Number of methods required to reset: **1**</span></span>
   * <span data-ttu-id="d798f-117">Methods available to users:</span><span class="sxs-lookup"><span data-stu-id="d798f-117">Methods available to users:</span></span>
      * <span data-ttu-id="d798f-118">**Mobile phone**</span><span class="sxs-lookup"><span data-stu-id="d798f-118">**Mobile phone**</span></span>
      * <span data-ttu-id="d798f-119">**Office phone**</span><span class="sxs-lookup"><span data-stu-id="d798f-119">**Office phone**</span></span>
   * <span data-ttu-id="d798f-120">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d798f-120">Click **Save**.</span></span>

    <span data-ttu-id="d798f-121">![Authentication][Authentication]</span><span class="sxs-lookup"><span data-stu-id="d798f-121">![Authentication][Authentication]</span></span>

4. <span data-ttu-id="d798f-122">From the **Registration** page, make the following choices:</span><span class="sxs-lookup"><span data-stu-id="d798f-122">From the **Registration** page, make the following choices:</span></span>
   * <span data-ttu-id="d798f-123">Require users to register when they sign in: **Yes**</span><span class="sxs-lookup"><span data-stu-id="d798f-123">Require users to register when they sign in: **Yes**</span></span>
   * <span data-ttu-id="d798f-124">Set the number of days before users are asked to reconfirm their authentication information: **365**</span><span class="sxs-lookup"><span data-stu-id="d798f-124">Set the number of days before users are asked to reconfirm their authentication information: **365**</span></span>

## <a name="test-self-service-password-reset"></a><span data-ttu-id="d798f-125">Test self-service password reset</span><span class="sxs-lookup"><span data-stu-id="d798f-125">Test self-service password reset</span></span>

<span data-ttu-id="d798f-126">Now lets test your SSPR configuration with a test user.</span><span class="sxs-lookup"><span data-stu-id="d798f-126">Now lets test your SSPR configuration with a test user.</span></span> <span data-ttu-id="d798f-127">Since Microsoft enforces strong authentication requirements for Azure administrator accounts, testing using an administrator account may change the outcome.</span><span class="sxs-lookup"><span data-stu-id="d798f-127">Since Microsoft enforces strong authentication requirements for Azure administrator accounts, testing using an administrator account may change the outcome.</span></span> <span data-ttu-id="d798f-128">For more information regarding the administrator password policy, see our [password policy](concept-sspr-policy.md) article.</span><span class="sxs-lookup"><span data-stu-id="d798f-128">For more information regarding the administrator password policy, see our [password policy](concept-sspr-policy.md) article.</span></span>

1. <span data-ttu-id="d798f-129">Open a new browser window in InPrivate or incognito mode, and browse to [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="d798f-129">Open a new browser window in InPrivate or incognito mode, and browse to [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).</span></span>
2. <span data-ttu-id="d798f-130">Sign in with a non-administrator test user, and register your authentication phone.</span><span class="sxs-lookup"><span data-stu-id="d798f-130">Sign in with a non-administrator test user, and register your authentication phone.</span></span>
3. <span data-ttu-id="d798f-131">Once complete, click the button marked **looks good** and close the browser window.</span><span class="sxs-lookup"><span data-stu-id="d798f-131">Once complete, click the button marked **looks good** and close the browser window.</span></span>
4. <span data-ttu-id="d798f-132">Open a new browser window in InPrivate or incognito mode, and browse to [https://aka.ms/sspr](https://aka.ms/sspr).</span><span class="sxs-lookup"><span data-stu-id="d798f-132">Open a new browser window in InPrivate or incognito mode, and browse to [https://aka.ms/sspr](https://aka.ms/sspr).</span></span>
5. <span data-ttu-id="d798f-133">Enter your non-administrator test users' User ID, the characters from the CAPTCHA, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d798f-133">Enter your non-administrator test users' User ID, the characters from the CAPTCHA, and then click **Next**.</span></span>
6. <span data-ttu-id="d798f-134">Follow the verification steps to reset your password</span><span class="sxs-lookup"><span data-stu-id="d798f-134">Follow the verification steps to reset your password</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d798f-135">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d798f-135">Clean up resources</span></span>

<span data-ttu-id="d798f-136">It's easy to disable self-service password reset.</span><span class="sxs-lookup"><span data-stu-id="d798f-136">It's easy to disable self-service password reset.</span></span> <span data-ttu-id="d798f-137">Open your Azure AD tenant and go to **Password Reset** > **Properties**, and then select **None** under **Self Service Password Reset Enabled**.</span><span class="sxs-lookup"><span data-stu-id="d798f-137">Open your Azure AD tenant and go to **Password Reset** > **Properties**, and then select **None** under **Self Service Password Reset Enabled**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d798f-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="d798f-138">Next steps</span></span>

<span data-ttu-id="d798f-139">In this quickstart, you’ve learned how to quickly configure self-service password reset for your cloud-only users.</span><span class="sxs-lookup"><span data-stu-id="d798f-139">In this quickstart, you’ve learned how to quickly configure self-service password reset for your cloud-only users.</span></span> <span data-ttu-id="d798f-140">To find out how to complete a more detailed roll out, continue to our roll out guide.</span><span class="sxs-lookup"><span data-stu-id="d798f-140">To find out how to complete a more detailed roll out, continue to our roll out guide.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d798f-141">Roll out self-service password reset</span><span class="sxs-lookup"><span data-stu-id="d798f-141">Roll out self-service password reset</span></span>](howto-sspr-deployment.md)

[Authentication]: ./media/quickstart-sspr/sspr-authentication-methods.png "Azure AD authentication methods available and the quantity required"
