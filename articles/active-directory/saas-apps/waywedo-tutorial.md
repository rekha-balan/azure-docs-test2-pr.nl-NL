---
title: 'Tutorial: Azure Active Directory integration with Way We Do | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Way We Do.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 84fc4f36-ecd1-42c6-8a70-cb0f3dc15655
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2018
ms.author: jeedes
ms.openlocfilehash: bc415ec7c577e221a1ab5af585dff5b4fc9ab7dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855784"
---
# <a name="tutorial-azure-active-directory-integration-with-way-we-do"></a><span data-ttu-id="e9dc3-103">Tutorial: Azure Active Directory integration with Way We Do</span><span class="sxs-lookup"><span data-stu-id="e9dc3-103">Tutorial: Azure Active Directory integration with Way We Do</span></span>

<span data-ttu-id="e9dc3-104">In this tutorial, you learn how to integrate Way We Do with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9dc3-104">In this tutorial, you learn how to integrate Way We Do with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9dc3-105">Integrating Way We Do with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-105">Integrating Way We Do with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9dc3-106">You can control in Azure AD who has access to Way We Do.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-106">You can control in Azure AD who has access to Way We Do.</span></span>
- <span data-ttu-id="e9dc3-107">You can enable your users to automatically get signed-on to Way We Do (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-107">You can enable your users to automatically get signed-on to Way We Do (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e9dc3-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e9dc3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e9dc3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9dc3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9dc3-110">Prerequisites</span></span>

<span data-ttu-id="e9dc3-111">To configure Azure AD integration with Way We Do, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-111">To configure Azure AD integration with Way We Do, you need the following items:</span></span>

- <span data-ttu-id="e9dc3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e9dc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9dc3-113">A Way We Do single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e9dc3-113">A Way We Do single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9dc3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9dc3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9dc3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9dc3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9dc3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9dc3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e9dc3-118">Scenario description</span></span>
<span data-ttu-id="e9dc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9dc3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9dc3-121">Adding Way We Do from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9dc3-121">Adding Way We Do from the gallery</span></span>
2. <span data-ttu-id="e9dc3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9dc3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-way-we-do-from-the-gallery"></a><span data-ttu-id="e9dc3-123">Adding Way We Do from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9dc3-123">Adding Way We Do from the gallery</span></span>
<span data-ttu-id="e9dc3-124">To configure the integration of Way We Do into Azure AD, you need to add Way We Do from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-124">To configure the integration of Way We Do into Azure AD, you need to add Way We Do from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9dc3-125">**To add Way We Do from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9dc3-125">**To add Way We Do from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9dc3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="e9dc3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9dc3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="e9dc3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="e9dc3-133">In the search box, type **Way We Do**, select **Way We Do** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-133">In the search box, type **Way We Do**, select **Way We Do** from result panel then click **Add** button to add the application.</span></span>

    ![Way We Do in the results list](./media/waywedo-tutorial/tutorial_waywedo_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e9dc3-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9dc3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e9dc3-136">In this section, you configure and test Azure AD single sign-on with Way We Do based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9dc3-136">In this section, you configure and test Azure AD single sign-on with Way We Do based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9dc3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Way We Do is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Way We Do is to a user in Azure AD.</span></span> <span data-ttu-id="e9dc3-138">In other words, a link relationship between an Azure AD user and the related user in Way We Do needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-138">In other words, a link relationship between an Azure AD user and the related user in Way We Do needs to be established.</span></span>

<span data-ttu-id="e9dc3-139">To configure and test Azure AD single sign-on with Way We Do, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-139">To configure and test Azure AD single sign-on with Way We Do, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9dc3-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9dc3-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9dc3-142">**[Create a Way We Do test user](#create-a-way-we-do-test-user)** - to have a counterpart of Britta Simon in Way We Do that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-142">**[Create a Way We Do test user](#create-a-way-we-do-test-user)** - to have a counterpart of Britta Simon in Way We Do that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9dc3-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9dc3-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e9dc3-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9dc3-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e9dc3-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Way We Do application.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Way We Do application.</span></span>

<span data-ttu-id="e9dc3-147">**To configure Azure AD single sign-on with Way We Do, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9dc3-147">**To configure Azure AD single sign-on with Way We Do, perform the following steps:**</span></span>

1. <span data-ttu-id="e9dc3-148">In the Azure portal, on the **Way We Do** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-148">In the Azure portal, on the **Way We Do** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="e9dc3-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/waywedo-tutorial/tutorial_waywedo_samlbase.png)

3. <span data-ttu-id="e9dc3-152">On the **Way We Do Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-152">On the **Way We Do Domain and URLs** section, perform the following steps:</span></span>

    ![Way We Do Domain and URLs single sign-on information](./media/waywedo-tutorial/tutorial_waywedo_url.png)

    <span data-ttu-id="e9dc3-154">a.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-154">a.</span></span> <span data-ttu-id="e9dc3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.waywedo.com/Authentication/ExternalSignIn`</span><span class="sxs-lookup"><span data-stu-id="e9dc3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.waywedo.com/Authentication/ExternalSignIn`</span></span>

    <span data-ttu-id="e9dc3-156">b.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-156">b.</span></span> <span data-ttu-id="e9dc3-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.waywedo.com`</span><span class="sxs-lookup"><span data-stu-id="e9dc3-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.waywedo.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9dc3-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-158">These values are not real.</span></span> <span data-ttu-id="e9dc3-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e9dc3-160">Contact [Way We Do Client support team](mailto:support@waywedo.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-160">Contact [Way We Do Client support team](mailto:support@waywedo.com) to get these values.</span></span> 
 
4. <span data-ttu-id="e9dc3-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/waywedo-tutorial/tutorial_waywedo_certificate.png) 

5. <span data-ttu-id="e9dc3-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/waywedo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9dc3-165">On the **Way We Do Configuration** section, click **Configure Way We Do** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-165">On the **Way We Do Configuration** section, click **Configure Way We Do** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e9dc3-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e9dc3-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Way We Do Configuration](./media/waywedo-tutorial/tutorial_waywedo_configure.png) 

7. <span data-ttu-id="e9dc3-168">In a different web browser window, login to Way We Do as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-168">In a different web browser window, login to Way We Do as a Security Administrator.</span></span>

8. <span data-ttu-id="e9dc3-169">Click the **person icon** in the top right corner of any page in Way We Do, then click **Account** in the dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-169">Click the **person icon** in the top right corner of any page in Way We Do, then click **Account** in the dropdown menu.</span></span>

    ![Way We Do account](./media/waywedo-tutorial/tutorial_waywedo_account.png) 

9. <span data-ttu-id="e9dc3-171">Click the **menu icon** to open the push navigation menu and Click **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-171">Click the **menu icon** to open the push navigation menu and Click **Single Sign On**.</span></span>

    ![Way We Do single](./media/waywedo-tutorial/tutorial_waywedo_single.png)

10. <span data-ttu-id="e9dc3-173">On the **Single sign-on setup** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-173">On the **Single sign-on setup** page, perform the following steps:</span></span>

    ![Way We Do save](./media/waywedo-tutorial/tutorial_waywedo_save.png)

    <span data-ttu-id="e9dc3-175">a.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-175">a.</span></span> <span data-ttu-id="e9dc3-176">Click the **Turn on single sign-on** toggle to **Yes** to enable Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-176">Click the **Turn on single sign-on** toggle to **Yes** to enable Single Sign-On.</span></span>

    <span data-ttu-id="e9dc3-177">b.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-177">b.</span></span> <span data-ttu-id="e9dc3-178">In the **Single sign-on name** textbox, enter your name.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-178">In the **Single sign-on name** textbox, enter your name.</span></span>

    <span data-ttu-id="e9dc3-179">c.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-179">c.</span></span> <span data-ttu-id="e9dc3-180">In the **Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-180">In the **Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="e9dc3-181">d.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-181">d.</span></span> <span data-ttu-id="e9dc3-182">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-182">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="e9dc3-183">e.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-183">e.</span></span> <span data-ttu-id="e9dc3-184">Upload the certificate by clicking the **select** button next to **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-184">Upload the certificate by clicking the **select** button next to **Certificate**.</span></span>

    <span data-ttu-id="e9dc3-185">f.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-185">f.</span></span> <span data-ttu-id="e9dc3-186">**Optional Settings** -</span><span class="sxs-lookup"><span data-stu-id="e9dc3-186">**Optional Settings** -</span></span>
    
    * <span data-ttu-id="e9dc3-187">Enable Passwords - When this option is disabled, the regular password functions for Way We Do so that users can only use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-187">Enable Passwords - When this option is disabled, the regular password functions for Way We Do so that users can only use single sign-on.</span></span>

    * <span data-ttu-id="e9dc3-188">Enable Auto-provisioning - When this is enabled, the email address used to sign-on will be automatically compared to the list of users in Way We Do.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-188">Enable Auto-provisioning - When this is enabled, the email address used to sign-on will be automatically compared to the list of users in Way We Do.</span></span> <span data-ttu-id="e9dc3-189">If the email address does not match an active user in Way We Do, it automatically adds a new user account for the person signing in, requesting any missing information.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-189">If the email address does not match an active user in Way We Do, it automatically adds a new user account for the person signing in, requesting any missing information.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e9dc3-190">Users added through single sign-on are added as general users and are not assigned a role in the system.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-190">Users added through single sign-on are added as general users and are not assigned a role in the system.</span></span> <span data-ttu-id="e9dc3-191">An Administrator is able to go in and modify their security role as an editor or administrator and can also assign one or several Org Chart roles.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-191">An Administrator is able to go in and modify their security role as an editor or administrator and can also assign one or several Org Chart roles.</span></span> 

    <span data-ttu-id="e9dc3-192">g.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-192">g.</span></span> <span data-ttu-id="e9dc3-193">Click **Save** to persist your settings.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-193">Click **Save** to persist your settings.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e9dc3-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9dc3-194">Create an Azure AD test user</span></span>

<span data-ttu-id="e9dc3-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e9dc3-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9dc3-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9dc3-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/waywedo-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e9dc3-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/waywedo-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e9dc3-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/waywedo-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e9dc3-204">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9dc3-204">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/waywedo-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e9dc3-206">a.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-206">a.</span></span> <span data-ttu-id="e9dc3-207">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9dc3-208">b.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-208">b.</span></span> <span data-ttu-id="e9dc3-209">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e9dc3-210">c.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-210">c.</span></span> <span data-ttu-id="e9dc3-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e9dc3-212">d.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-212">d.</span></span> <span data-ttu-id="e9dc3-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-213">Click **Create**.</span></span>
 
### <a name="create-a-way-we-do-test-user"></a><span data-ttu-id="e9dc3-214">Create a Way We Do test user</span><span class="sxs-lookup"><span data-stu-id="e9dc3-214">Create a Way We Do test user</span></span>

<span data-ttu-id="e9dc3-215">The objective of this section is to create a user called Britta Simon in Way We Do.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-215">The objective of this section is to create a user called Britta Simon in Way We Do.</span></span> <span data-ttu-id="e9dc3-216">Way We Do supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-216">Way We Do supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="e9dc3-217">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-217">There is no action item for you in this section.</span></span> <span data-ttu-id="e9dc3-218">A new user is created during an attempt to access Way We Do if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-218">A new user is created during an attempt to access Way We Do if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="e9dc3-219">If you need to create a user manually, contact [Way We Do Client support team](mailto:support@waywedo.com).</span><span class="sxs-lookup"><span data-stu-id="e9dc3-219">If you need to create a user manually, contact [Way We Do Client support team](mailto:support@waywedo.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e9dc3-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9dc3-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="e9dc3-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Way We Do.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Way We Do.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e9dc3-223">**To assign Britta Simon to Way We Do, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9dc3-223">**To assign Britta Simon to Way We Do, perform the following steps:**</span></span>

1. <span data-ttu-id="e9dc3-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="e9dc3-226">In the applications list, select **Way We Do**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-226">In the applications list, select **Way We Do**.</span></span>

    ![The Way We Do link in the Applications list](./media/waywedo-tutorial/tutorial_waywedo_app.png)  

3. <span data-ttu-id="e9dc3-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-228">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="e9dc3-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-230">Click **Add** button.</span></span> <span data-ttu-id="e9dc3-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="e9dc3-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9dc3-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9dc3-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e9dc3-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9dc3-236">Test single sign-on</span></span>

<span data-ttu-id="e9dc3-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9dc3-238">When you click the Way We Do tile in the Access Panel, you should get automatically signed-on to your Way We Do application.</span><span class="sxs-lookup"><span data-stu-id="e9dc3-238">When you click the Way We Do tile in the Access Panel, you should get automatically signed-on to your Way We Do application.</span></span>
<span data-ttu-id="e9dc3-239">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9dc3-239">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9dc3-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e9dc3-240">Additional resources</span></span>

* [<span data-ttu-id="e9dc3-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9dc3-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e9dc3-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9dc3-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/waywedo-tutorial/tutorial_general_01.png
[2]: ./media/waywedo-tutorial/tutorial_general_02.png
[3]: ./media/waywedo-tutorial/tutorial_general_03.png
[4]: ./media/waywedo-tutorial/tutorial_general_04.png

[100]: ./media/waywedo-tutorial/tutorial_general_100.png

[200]: ./media/waywedo-tutorial/tutorial_general_200.png
[201]: ./media/waywedo-tutorial/tutorial_general_201.png
[202]: ./media/waywedo-tutorial/tutorial_general_202.png
[203]: ./media/waywedo-tutorial/tutorial_general_203.png

