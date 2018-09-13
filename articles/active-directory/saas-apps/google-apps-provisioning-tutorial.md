---
title: 'Tutorial: Configure G Suite for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to automatically provision and de-provision user accounts from Azure AD to G Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 924584a77d36ec41488d8c76d9631baf484ff494
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864513"
---
# <a name="tutorial-configure-g-suite-for-automatic-user-provisioning"></a><span data-ttu-id="0f1df-103">Tutorial: Configure G Suite for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="0f1df-103">Tutorial: Configure G Suite for automatic user provisioning</span></span>

<span data-ttu-id="0f1df-104">The objective of this tutorial is to show you how to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-104">The objective of this tutorial is to show you how to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to G Suite.</span></span>

> [!NOTE]
> <span data-ttu-id="0f1df-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="0f1df-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="0f1df-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="0f1df-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f1df-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0f1df-107">Prerequisites</span></span>

<span data-ttu-id="0f1df-108">To configure Azure AD integration with G Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0f1df-108">To configure Azure AD integration with G Suite, you need the following items:</span></span>

- <span data-ttu-id="0f1df-109">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0f1df-109">An Azure AD subscription</span></span>
- <span data-ttu-id="0f1df-110">A G Suite single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0f1df-110">A G Suite single sign-on enabled subscription</span></span>
- <span data-ttu-id="0f1df-111">A Google Apps subscription or Google Cloud Platform subscription.</span><span class="sxs-lookup"><span data-stu-id="0f1df-111">A Google Apps subscription or Google Cloud Platform subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0f1df-112">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0f1df-112">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f1df-113">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0f1df-113">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f1df-114">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0f1df-114">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f1df-115">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f1df-115">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-to-g-suite"></a><span data-ttu-id="0f1df-116">Assign users to G Suite</span><span class="sxs-lookup"><span data-stu-id="0f1df-116">Assign users to G Suite</span></span>

<span data-ttu-id="0f1df-117">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="0f1df-117">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0f1df-118">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="0f1df-118">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="0f1df-119">Before you configure and enable the provisioning service, you need to decide which users or groups in Azure AD need access to your app.</span><span class="sxs-lookup"><span data-stu-id="0f1df-119">Before you configure and enable the provisioning service, you need to decide which users or groups in Azure AD need access to your app.</span></span> <span data-ttu-id="0f1df-120">After you've made this decision, you can assign these users to your app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0f1df-120">After you've made this decision, you can assign these users to your app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f1df-121">We recommend  that a single Azure AD user be assigned to G Suite to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="0f1df-121">We recommend  that a single Azure AD user be assigned to G Suite to test the provisioning configuration.</span></span> <span data-ttu-id="0f1df-122">You can assign additional users and groups later.</span><span class="sxs-lookup"><span data-stu-id="0f1df-122">You can assign additional users and groups later.</span></span>

> <span data-ttu-id="0f1df-123">When you assign a user to G Suite, select the **User** or **Group** role in the assignment dialog box.</span><span class="sxs-lookup"><span data-stu-id="0f1df-123">When you assign a user to G Suite, select the **User** or **Group** role in the assignment dialog box.</span></span> <span data-ttu-id="0f1df-124">The **Default Access** role doesn't work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="0f1df-124">The **Default Access** role doesn't work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0f1df-125">Enable automated user provisioning</span><span class="sxs-lookup"><span data-stu-id="0f1df-125">Enable automated user provisioning</span></span>

<span data-ttu-id="0f1df-126">This section guides you through the process of connecting your Azure AD to the user account provisioning API of G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-126">This section guides you through the process of connecting your Azure AD to the user account provisioning API of G Suite.</span></span> <span data-ttu-id="0f1df-127">It also helps you configure the provisioning service to create, update, and disable assigned user accounts in G Suite based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f1df-127">It also helps you configure the provisioning service to create, update, and disable assigned user accounts in G Suite based on user and group assignment in Azure AD.</span></span>

>[!TIP]
><span data-ttu-id="0f1df-128">You might also choose to enable SAML-based single sign-on for G Suites, by following the instructions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f1df-128">You might also choose to enable SAML-based single sign-on for G Suites, by following the instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0f1df-129">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="0f1df-129">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="0f1df-130">Configure automatic user account provisioning</span><span class="sxs-lookup"><span data-stu-id="0f1df-130">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="0f1df-131">Another viable option for automating user provisioning to G Suite is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en).</span><span class="sxs-lookup"><span data-stu-id="0f1df-131">Another viable option for automating user provisioning to G Suite is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en).</span></span> <span data-ttu-id="0f1df-132">GADS provisions your on-premises Active Directory identities to G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-132">GADS provisions your on-premises Active Directory identities to G Suite.</span></span> <span data-ttu-id="0f1df-133">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and email-enabled groups to G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-133">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and email-enabled groups to G Suite.</span></span> 

1. <span data-ttu-id="0f1df-134">Sign in to the [Google Apps Admin console](http://admin.google.com/) with your administrator account, and then select **Security**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-134">Sign in to the [Google Apps Admin console](http://admin.google.com/) with your administrator account, and then select **Security**.</span></span> <span data-ttu-id="0f1df-135">If you don't see the link, it might be hidden under the **More Controls** menu at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="0f1df-135">If you don't see the link, it might be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Select security.][10]

1. <span data-ttu-id="0f1df-137">On the **Security** page, select **API Reference**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-137">On the **Security** page, select **API Reference**.</span></span>
   
    ![Select API Reference.][15]

1. <span data-ttu-id="0f1df-139">Select **Enable API access**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-139">Select **Enable API access**.</span></span>
   
    ![Select API Reference.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="0f1df-141">For every user that you intend to provision to G Suite, their user name in Azure Active Directory *must* be tied to a custom domain.</span><span class="sxs-lookup"><span data-stu-id="0f1df-141">For every user that you intend to provision to G Suite, their user name in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="0f1df-142">For example, user names that look like bob@contoso.onmicrosoft.com are not accepted by G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-142">For example, user names that look like bob@contoso.onmicrosoft.com are not accepted by G Suite.</span></span> <span data-ttu-id="0f1df-143">On the other hand, bob@contoso.com is accepted.</span><span class="sxs-lookup"><span data-stu-id="0f1df-143">On the other hand, bob@contoso.com is accepted.</span></span> <span data-ttu-id="0f1df-144">You can change an existing user's domain by editing their properties in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f1df-144">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="0f1df-145">We've included instructions for how to set a custom domain for both Azure Active Directory and G Suite in the following steps.</span><span class="sxs-lookup"><span data-stu-id="0f1df-145">We've included instructions for how to set a custom domain for both Azure Active Directory and G Suite in the following steps.</span></span>
      
1. <span data-ttu-id="0f1df-146">If you haven't added a custom domain name to your Azure Active Directory yet, then take the following steps:</span><span class="sxs-lookup"><span data-stu-id="0f1df-146">If you haven't added a custom domain name to your Azure Active Directory yet, then take the following steps:</span></span>
  
    <span data-ttu-id="0f1df-147">a.</span><span class="sxs-lookup"><span data-stu-id="0f1df-147">a.</span></span> <span data-ttu-id="0f1df-148">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-148">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select **Active Directory**.</span></span> <span data-ttu-id="0f1df-149">In the directory list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="0f1df-149">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="0f1df-150">b.</span><span class="sxs-lookup"><span data-stu-id="0f1df-150">b.</span></span> <span data-ttu-id="0f1df-151">Select **Domain name** on the left navigation pane, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-151">Select **Domain name** on the left navigation pane, and then select **Add**.</span></span>
     
     ![Domain](./media/google-apps-provisioning-tutorial/domain_1.png)

     ![Domain add](./media/google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="0f1df-154">c.</span><span class="sxs-lookup"><span data-stu-id="0f1df-154">c.</span></span> <span data-ttu-id="0f1df-155">Type your domain name into the **Domain name** field.</span><span class="sxs-lookup"><span data-stu-id="0f1df-155">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="0f1df-156">This domain name should be the same domain name that you intend to use for G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-156">This domain name should be the same domain name that you intend to use for G Suite.</span></span> <span data-ttu-id="0f1df-157">Then select the **Add Domain** button.</span><span class="sxs-lookup"><span data-stu-id="0f1df-157">Then select the **Add Domain** button.</span></span>
     
     ![Domain name](./media/google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="0f1df-159">d.</span><span class="sxs-lookup"><span data-stu-id="0f1df-159">d.</span></span> <span data-ttu-id="0f1df-160">Select **Next** to go to the verification page.</span><span class="sxs-lookup"><span data-stu-id="0f1df-160">Select **Next** to go to the verification page.</span></span> <span data-ttu-id="0f1df-161">To verify that you own this domain, edit the domain's DNS records according to the values that are provided on this page.</span><span class="sxs-lookup"><span data-stu-id="0f1df-161">To verify that you own this domain, edit the domain's DNS records according to the values that are provided on this page.</span></span> <span data-ttu-id="0f1df-162">You might choose to verify by using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span><span class="sxs-lookup"><span data-stu-id="0f1df-162">You might choose to verify by using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> 
    
    <span data-ttu-id="0f1df-163">For more comprehensive instructions on how to verify domain names with Azure AD, see [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0f1df-163">For more comprehensive instructions on how to verify domain names with Azure AD, see [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Domain](./media/google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="0f1df-165">e.</span><span class="sxs-lookup"><span data-stu-id="0f1df-165">e.</span></span> <span data-ttu-id="0f1df-166">Repeat the preceding steps for all the domains that you intend to add to your directory.</span><span class="sxs-lookup"><span data-stu-id="0f1df-166">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

    > [!NOTE]
    <span data-ttu-id="0f1df-167">For user provisioning, the custom domain must match the domain name of the source Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f1df-167">For user provisioning, the custom domain must match the domain name of the source Azure AD.</span></span> <span data-ttu-id="0f1df-168">If they do not match, you may be able to solve the problem by implementing attribute mapping customization.</span><span class="sxs-lookup"><span data-stu-id="0f1df-168">If they do not match, you may be able to solve the problem by implementing attribute mapping customization.</span></span>


1. <span data-ttu-id="0f1df-169">Now that you have verified all your domains with Azure AD, you must verify them again with Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f1df-169">Now that you have verified all your domains with Azure AD, you must verify them again with Google Apps.</span></span> <span data-ttu-id="0f1df-170">For each domain that isn't already registered with Google, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="0f1df-170">For each domain that isn't already registered with Google, take the following steps:</span></span>
   
    <span data-ttu-id="0f1df-171">a.</span><span class="sxs-lookup"><span data-stu-id="0f1df-171">a.</span></span> <span data-ttu-id="0f1df-172">In the [Google Apps Admin Console](http://admin.google.com/), select **Domains**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-172">In the [Google Apps Admin Console](http://admin.google.com/), select **Domains**.</span></span>
     
     ![Select Domains][20]

    <span data-ttu-id="0f1df-174">b.</span><span class="sxs-lookup"><span data-stu-id="0f1df-174">b.</span></span> <span data-ttu-id="0f1df-175">Select **Add a domain or a domain alias**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-175">Select **Add a domain or a domain alias**.</span></span>
     
     ![Add a new domain][21]

    <span data-ttu-id="0f1df-177">c.</span><span class="sxs-lookup"><span data-stu-id="0f1df-177">c.</span></span> <span data-ttu-id="0f1df-178">Select **Add another domain**, and then type in the name of the domain that you want to add.</span><span class="sxs-lookup"><span data-stu-id="0f1df-178">Select **Add another domain**, and then type in the name of the domain that you want to add.</span></span>
     
     ![Type in your domain name][22]

    <span data-ttu-id="0f1df-180">d.</span><span class="sxs-lookup"><span data-stu-id="0f1df-180">d.</span></span> <span data-ttu-id="0f1df-181">Select **Continue and verify domain ownership**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-181">Select **Continue and verify domain ownership**.</span></span> <span data-ttu-id="0f1df-182">Then follow the steps to verify that you own the domain name.</span><span class="sxs-lookup"><span data-stu-id="0f1df-182">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="0f1df-183">For comprehensive instructions on how to verify your domain with Google, see [Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="0f1df-183">For comprehensive instructions on how to verify your domain with Google, see [Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="0f1df-184">e.</span><span class="sxs-lookup"><span data-stu-id="0f1df-184">e.</span></span> <span data-ttu-id="0f1df-185">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f1df-185">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="0f1df-186">If you change the primary domain for your G Suite tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step 2: Enable single sign-on](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0f1df-186">If you change the primary domain for your G Suite tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step 2: Enable single sign-on](#step-two-enable-single-sign-on).</span></span>
       
1. <span data-ttu-id="0f1df-187">In the [Google Apps Admin console](http://admin.google.com/), select **Admin Roles**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-187">In the [Google Apps Admin console](http://admin.google.com/), select **Admin Roles**.</span></span>
   
     ![Select Google Apps][26]

1. <span data-ttu-id="0f1df-189">Determine which admin account you want to use to manage user provisioning.</span><span class="sxs-lookup"><span data-stu-id="0f1df-189">Determine which admin account you want to use to manage user provisioning.</span></span> <span data-ttu-id="0f1df-190">For the **admin role** of that account, edit the **Privileges** for that role.</span><span class="sxs-lookup"><span data-stu-id="0f1df-190">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="0f1df-191">Make sure to enable all **Admin API Privileges** so that this account can be used for provisioning.</span><span class="sxs-lookup"><span data-stu-id="0f1df-191">Make sure to enable all **Admin API Privileges** so that this account can be used for provisioning.</span></span>
   
     ![Select Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="0f1df-193">If you are configuring a production environment, the best practice is to create an admin account in G Suite specifically for this step.</span><span class="sxs-lookup"><span data-stu-id="0f1df-193">If you are configuring a production environment, the best practice is to create an admin account in G Suite specifically for this step.</span></span> <span data-ttu-id="0f1df-194">These accounts must have an admin role associated with them that has the necessary API privileges.</span><span class="sxs-lookup"><span data-stu-id="0f1df-194">These accounts must have an admin role associated with them that has the necessary API privileges.</span></span>
     
1. <span data-ttu-id="0f1df-195">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span><span class="sxs-lookup"><span data-stu-id="0f1df-195">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

1. <span data-ttu-id="0f1df-196">If you have already configured G Suite for single sign-on, search for your instance of G Suite by using the search field.</span><span class="sxs-lookup"><span data-stu-id="0f1df-196">If you have already configured G Suite for single sign-on, search for your instance of G Suite by using the search field.</span></span> <span data-ttu-id="0f1df-197">Otherwise, select **Add**, and then search for **G Suite** or **Google Apps** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="0f1df-197">Otherwise, select **Add**, and then search for **G Suite** or **Google Apps** in the application gallery.</span></span> <span data-ttu-id="0f1df-198">Select your app from the search results, and then add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="0f1df-198">Select your app from the search results, and then add it to your list of applications.</span></span>

1. <span data-ttu-id="0f1df-199">Select your instance of G Suite, and then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="0f1df-199">Select your instance of G Suite, and then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="0f1df-200">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-200">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![Provisioning](./media/google-apps-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="0f1df-202">Under the **Admin Credentials** section, select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-202">Under the **Admin Credentials** section, select **Authorize**.</span></span> <span data-ttu-id="0f1df-203">It opens a Google authorization dialog box in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="0f1df-203">It opens a Google authorization dialog box in a new browser window.</span></span>

1. <span data-ttu-id="0f1df-204">Confirm that you want to give Azure Active Directory permission to make changes to your G Suite tenant.</span><span class="sxs-lookup"><span data-stu-id="0f1df-204">Confirm that you want to give Azure Active Directory permission to make changes to your G Suite tenant.</span></span> <span data-ttu-id="0f1df-205">Select **Accept**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-205">Select **Accept**.</span></span>
    
     ![Confirm permissions.][28]

1. <span data-ttu-id="0f1df-207">In the Azure portal, select **Test Connection** to ensure that Azure AD can connect to your app.</span><span class="sxs-lookup"><span data-stu-id="0f1df-207">In the Azure portal, select **Test Connection** to ensure that Azure AD can connect to your app.</span></span> <span data-ttu-id="0f1df-208">If the connection fails, ensure that your G Suite account has Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="0f1df-208">If the connection fails, ensure that your G Suite account has Team Admin permissions.</span></span> <span data-ttu-id="0f1df-209">Then try the **Authorize** step again.</span><span class="sxs-lookup"><span data-stu-id="0f1df-209">Then try the **Authorize** step again.</span></span>

1. <span data-ttu-id="0f1df-210">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field.</span><span class="sxs-lookup"><span data-stu-id="0f1df-210">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field.</span></span> <span data-ttu-id="0f1df-211">Then select the check box.</span><span class="sxs-lookup"><span data-stu-id="0f1df-211">Then select the check box.</span></span>

1. <span data-ttu-id="0f1df-212">Select **Save.**</span><span class="sxs-lookup"><span data-stu-id="0f1df-212">Select **Save.**</span></span>

1. <span data-ttu-id="0f1df-213">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-213">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Google Apps**.</span></span>

1. <span data-ttu-id="0f1df-214">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to G Suite.</span><span class="sxs-lookup"><span data-stu-id="0f1df-214">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to G Suite.</span></span> <span data-ttu-id="0f1df-215">The attributes that are **Matching** properties are used to match the user accounts in G Suite for update operations.</span><span class="sxs-lookup"><span data-stu-id="0f1df-215">The attributes that are **Matching** properties are used to match the user accounts in G Suite for update operations.</span></span> <span data-ttu-id="0f1df-216">Select **Save** to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="0f1df-216">Select **Save** to commit any changes.</span></span>

1. <span data-ttu-id="0f1df-217">To enable the Azure AD provisioning service for G Suite, change the **Provisioning Status** to **On** in **Settings**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-217">To enable the Azure AD provisioning service for G Suite, change the **Provisioning Status** to **On** in **Settings**.</span></span>

1. <span data-ttu-id="0f1df-218">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="0f1df-218">Select **Save**.</span></span>

<span data-ttu-id="0f1df-219">This process starts the initial synchronization of any users or groups that are assigned to G Suite in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="0f1df-219">This process starts the initial synchronization of any users or groups that are assigned to G Suite in the Users and Groups section.</span></span> <span data-ttu-id="0f1df-220">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes while the service is running.</span><span class="sxs-lookup"><span data-stu-id="0f1df-220">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes while the service is running.</span></span> <span data-ttu-id="0f1df-221">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs.</span><span class="sxs-lookup"><span data-stu-id="0f1df-221">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs.</span></span> <span data-ttu-id="0f1df-222">These logs describe all actions that are performed by the provisioning service  on your app.</span><span class="sxs-lookup"><span data-stu-id="0f1df-222">These logs describe all actions that are performed by the provisioning service  on your app.</span></span>

<span data-ttu-id="0f1df-223">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="0f1df-223">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f1df-224">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0f1df-224">Additional resources</span></span>

* [<span data-ttu-id="0f1df-225">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="0f1df-225">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="0f1df-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0f1df-226">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="0f1df-227">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="0f1df-227">Configure single sign-on</span></span>](google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/google-apps-provisioning-tutorial/gapps-auth.png
