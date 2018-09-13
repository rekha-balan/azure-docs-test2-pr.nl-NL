---
title: Enabling an Azure Multi-Factor Authentication pilot
description: In this tutorial, you will enable Azure AD Multi-Factor Authentication for a pilot group of users
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: 098973e2ece3477ec87b154c0304c4ca7e0246d1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869713"
---
# <a name="tutorial-complete-an-azure-multi-factor-authentication-pilot-roll-out"></a><span data-ttu-id="15478-103">Tutorial: Complete an Azure Multi-Factor Authentication pilot roll out</span><span class="sxs-lookup"><span data-stu-id="15478-103">Tutorial: Complete an Azure Multi-Factor Authentication pilot roll out</span></span>

<span data-ttu-id="15478-104">In this tutorial, you walk you through configuring a conditional access policy enabling Azure Multi-Factor Authentication (Azure MFA) when logging in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15478-104">In this tutorial, you walk you through configuring a conditional access policy enabling Azure Multi-Factor Authentication (Azure MFA) when logging in to the Azure portal.</span></span> <span data-ttu-id="15478-105">The policy is deployed to and tested on a specific group of pilot users.</span><span class="sxs-lookup"><span data-stu-id="15478-105">The policy is deployed to and tested on a specific group of pilot users.</span></span> <span data-ttu-id="15478-106">Deployment of Azure MFA using conditional access provides significant flexibility for organizations and administrators compared to the traditional enforced method.</span><span class="sxs-lookup"><span data-stu-id="15478-106">Deployment of Azure MFA using conditional access provides significant flexibility for organizations and administrators compared to the traditional enforced method.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="15478-107">Enable Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="15478-107">Enable Azure Multi-Factor Authentication</span></span>
> * <span data-ttu-id="15478-108">Test Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="15478-108">Test Azure Multi-Factor Authentication</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15478-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15478-109">Prerequisites</span></span>

* <span data-ttu-id="15478-110">A working Azure AD tenant with at least a trial license enabled.</span><span class="sxs-lookup"><span data-stu-id="15478-110">A working Azure AD tenant with at least a trial license enabled.</span></span>
* <span data-ttu-id="15478-111">An account with Global Administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="15478-111">An account with Global Administrator privileges.</span></span>
* <span data-ttu-id="15478-112">A non-administrator test user with a password you know for testing, if you need to create a user see the article [Quickstart: Add new users to Azure Active Directory](../add-users-azure-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="15478-112">A non-administrator test user with a password you know for testing, if you need to create a user see the article [Quickstart: Add new users to Azure Active Directory](../add-users-azure-active-directory.md).</span></span>
* <span data-ttu-id="15478-113">A pilot group to test with that the non-administrator user is a member of, if you need to create a group see the article [Create a group and add members in Azure Active Directory](../active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15478-113">A pilot group to test with that the non-administrator user is a member of, if you need to create a group see the article [Create a group and add members in Azure Active Directory](../active-directory-groups-create-azure-portal.md).</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="15478-114">Enable Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="15478-114">Enable Azure Multi-Factor Authentication</span></span>

1. <span data-ttu-id="15478-115">Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.</span><span class="sxs-lookup"><span data-stu-id="15478-115">Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.</span></span>
1. <span data-ttu-id="15478-116">Browse to **Azure Active Directory**, **Conditional access**</span><span class="sxs-lookup"><span data-stu-id="15478-116">Browse to **Azure Active Directory**, **Conditional access**</span></span>
1. <span data-ttu-id="15478-117">Select **New policy**</span><span class="sxs-lookup"><span data-stu-id="15478-117">Select **New policy**</span></span>
1. <span data-ttu-id="15478-118">Name your policy **MFA Pilot**</span><span class="sxs-lookup"><span data-stu-id="15478-118">Name your policy **MFA Pilot**</span></span>
1. <span data-ttu-id="15478-119">Under **users and groups**, select the **Select users and groups** radio button</span><span class="sxs-lookup"><span data-stu-id="15478-119">Under **users and groups**, select the **Select users and groups** radio button</span></span>
    * <span data-ttu-id="15478-120">Select your pilot group created as part of the prerequisites section of this article</span><span class="sxs-lookup"><span data-stu-id="15478-120">Select your pilot group created as part of the prerequisites section of this article</span></span>
    * <span data-ttu-id="15478-121">Click **Done**</span><span class="sxs-lookup"><span data-stu-id="15478-121">Click **Done**</span></span>
1. <span data-ttu-id="15478-122">Under **Cloud apps**, select the **Select apps** radio button</span><span class="sxs-lookup"><span data-stu-id="15478-122">Under **Cloud apps**, select the **Select apps** radio button</span></span>
    * <span data-ttu-id="15478-123">The cloud app for the Azure portal is **Microsoft Azure Management**</span><span class="sxs-lookup"><span data-stu-id="15478-123">The cloud app for the Azure portal is **Microsoft Azure Management**</span></span>
    * <span data-ttu-id="15478-124">Click **Select**</span><span class="sxs-lookup"><span data-stu-id="15478-124">Click **Select**</span></span>
    * <span data-ttu-id="15478-125">Click **Done**</span><span class="sxs-lookup"><span data-stu-id="15478-125">Click **Done**</span></span>
1. <span data-ttu-id="15478-126">Skip the **Conditions** section</span><span class="sxs-lookup"><span data-stu-id="15478-126">Skip the **Conditions** section</span></span>
1. <span data-ttu-id="15478-127">Under **Grant**, make sure the **Grant access** radio button is selected</span><span class="sxs-lookup"><span data-stu-id="15478-127">Under **Grant**, make sure the **Grant access** radio button is selected</span></span>
    * <span data-ttu-id="15478-128">Check the box for **Require multi-factor authentication**</span><span class="sxs-lookup"><span data-stu-id="15478-128">Check the box for **Require multi-factor authentication**</span></span>
    * <span data-ttu-id="15478-129">Click **Select**</span><span class="sxs-lookup"><span data-stu-id="15478-129">Click **Select**</span></span>
1. <span data-ttu-id="15478-130">Skip the **Session** section</span><span class="sxs-lookup"><span data-stu-id="15478-130">Skip the **Session** section</span></span>
1. <span data-ttu-id="15478-131">Set the **Enable policy** toggle to **On**</span><span class="sxs-lookup"><span data-stu-id="15478-131">Set the **Enable policy** toggle to **On**</span></span>
1. <span data-ttu-id="15478-132">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="15478-132">Click **Create**</span></span>

## <a name="test-azure-multi-factor-authentication"></a><span data-ttu-id="15478-133">Test Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="15478-133">Test Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="15478-134">To prove that your conditional access policy works, you test logging in to a resource that should not require MFA and then to the Azure portal that requires MFA.</span><span class="sxs-lookup"><span data-stu-id="15478-134">To prove that your conditional access policy works, you test logging in to a resource that should not require MFA and then to the Azure portal that requires MFA.</span></span>

1. <span data-ttu-id="15478-135">Open a new browser window in InPrivate or incognito mode and browse to [https://account.activedirectory.windowsazure.com](https://account.activedirectory.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="15478-135">Open a new browser window in InPrivate or incognito mode and browse to [https://account.activedirectory.windowsazure.com](https://account.activedirectory.windowsazure.com).</span></span>
   * <span data-ttu-id="15478-136">Log in with the test user created as part of the prerequisites section of this article and note that it should not ask you to complete MFA.</span><span class="sxs-lookup"><span data-stu-id="15478-136">Log in with the test user created as part of the prerequisites section of this article and note that it should not ask you to complete MFA.</span></span>
   * <span data-ttu-id="15478-137">Close the browser window.</span><span class="sxs-lookup"><span data-stu-id="15478-137">Close the browser window.</span></span>
2. <span data-ttu-id="15478-138">Open a new browser window in InPrivate or incognito mode and browse to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15478-138">Open a new browser window in InPrivate or incognito mode and browse to [https://portal.azure.com](https://portal.azure.com).</span></span>
   * <span data-ttu-id="15478-139">Log in with the test user created as part of the prerequisites section of this article and note that you should now be required to register for and use Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="15478-139">Log in with the test user created as part of the prerequisites section of this article and note that you should now be required to register for and use Azure Multi-Factor Authentication.</span></span>
   * <span data-ttu-id="15478-140">Close the browser window.</span><span class="sxs-lookup"><span data-stu-id="15478-140">Close the browser window.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="15478-141">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="15478-141">Clean up resources</span></span>

<span data-ttu-id="15478-142">If you decide you no longer want to use the functionality you have configured as part of this tutorial, make the following change.</span><span class="sxs-lookup"><span data-stu-id="15478-142">If you decide you no longer want to use the functionality you have configured as part of this tutorial, make the following change.</span></span>

1. <span data-ttu-id="15478-143">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15478-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="15478-144">Browse to **Azure Active Directory**, **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="15478-144">Browse to **Azure Active Directory**, **Conditional access**.</span></span>
1. <span data-ttu-id="15478-145">Select the conditional access policy you created.</span><span class="sxs-lookup"><span data-stu-id="15478-145">Select the conditional access policy you created.</span></span>
1. <span data-ttu-id="15478-146">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="15478-146">Click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15478-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="15478-147">Next steps</span></span>

<span data-ttu-id="15478-148">In this tutorial, you have enabled Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="15478-148">In this tutorial, you have enabled Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="15478-149">Continue on to the next tutorial to see how Azure Identity Protection can be integrated into the self-service password reset and Multi-Factor Authentication experiences.</span><span class="sxs-lookup"><span data-stu-id="15478-149">Continue on to the next tutorial to see how Azure Identity Protection can be integrated into the self-service password reset and Multi-Factor Authentication experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15478-150">Evaluate risk at sign in</span><span class="sxs-lookup"><span data-stu-id="15478-150">Evaluate risk at sign in</span></span>](tutorial-risk-based-sspr-mfa.md)