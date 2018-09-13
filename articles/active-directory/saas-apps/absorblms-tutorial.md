---
title: 'Tutorial: Azure Active Directory integration with Absorb LMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Absorb LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jeedes
ms.openlocfilehash: 066ae92056e4b80b6627b371d6ebeb3235b2781d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868460"
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="75205-103">Tutorial: Azure Active Directory integration with Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="75205-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="75205-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75205-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75205-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="75205-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75205-106">You can control in Azure AD who has access to Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="75205-106">You can control in Azure AD who has access to Absorb LMS.</span></span>
- <span data-ttu-id="75205-107">You can enable your users to automatically sign in to Absorb LMS (via single sign-on) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="75205-107">You can enable your users to automatically sign in to Absorb LMS (via single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="75205-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75205-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="75205-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="75205-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75205-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="75205-110">Prerequisites</span></span>

<span data-ttu-id="75205-111">To configure Azure AD integration with Absorb LMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="75205-111">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="75205-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="75205-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75205-113">An Absorb LMS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="75205-113">An Absorb LMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75205-114">We recommend not using a production environment for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="75205-114">We recommend not using a production environment for this tutorial.</span></span>

<span data-ttu-id="75205-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="75205-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="75205-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="75205-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75205-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75205-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75205-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="75205-118">Scenario description</span></span>
<span data-ttu-id="75205-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="75205-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75205-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="75205-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="75205-121">Adding Absorb LMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="75205-121">Adding Absorb LMS from the gallery</span></span>
* <span data-ttu-id="75205-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="75205-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-absorb-lms-from-the-gallery"></a><span data-ttu-id="75205-123">Add Absorb LMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="75205-123">Add Absorb LMS from the gallery</span></span>
<span data-ttu-id="75205-124">To configure the integration of Absorb LMS into Azure AD, add Absorb LMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="75205-124">To configure the integration of Absorb LMS into Azure AD, add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75205-125">To add Absorb LMS from the gallery, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-125">To add Absorb LMS from the gallery, do the following:</span></span>

1. <span data-ttu-id="75205-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="75205-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="75205-128">Go to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="75205-128">Go to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications pane][2]
    
3. <span data-ttu-id="75205-130">To add an application, select the **New application** button.</span><span class="sxs-lookup"><span data-stu-id="75205-130">To add an application, select the **New application** button.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="75205-132">In the search box, type **Absorb LMS**, select **Absorb LMS** in result panel, and then select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="75205-132">In the search box, type **Absorb LMS**, select **Absorb LMS** in result panel, and then select the **Add** button.</span></span>

    ![Absorb LMS in the results list](./media/absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="75205-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="75205-134">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="75205-135">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75205-135">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called Britta Simon.</span></span>

<span data-ttu-id="75205-136">For single sign-on to work, Azure AD needs to know what the Absorb LMS counterpart user is in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75205-136">For single sign-on to work, Azure AD needs to know what the Absorb LMS counterpart user is in Azure AD.</span></span> <span data-ttu-id="75205-137">In other words, you must establish a link relationship between a user in Azure AD and the corresponding user in Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="75205-137">In other words, you must establish a link relationship between a user in Azure AD and the corresponding user in Absorb LMS.</span></span>

<span data-ttu-id="75205-138">You establish this link relationship by assigning the *user name* value in Azure AD as the *Username* value in Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="75205-138">You establish this link relationship by assigning the *user name* value in Azure AD as the *Username* value in Absorb LMS.</span></span>

<span data-ttu-id="75205-139">To configure and test Azure AD single sign-on with Absorb LMS, complete the building blocks in the next five sections.</span><span class="sxs-lookup"><span data-stu-id="75205-139">To configure and test Azure AD single sign-on with Absorb LMS, complete the building blocks in the next five sections.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="75205-140">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="75205-140">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="75205-141">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span><span class="sxs-lookup"><span data-stu-id="75205-141">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="75205-142">To configure Azure AD single sign-on with Absorb LMS, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-142">To configure Azure AD single sign-on with Absorb LMS, do the following:</span></span>

1. <span data-ttu-id="75205-143">In the Azure portal, on the **Absorb LMS** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="75205-143">In the Azure portal, on the **Absorb LMS** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="75205-145">In the **Single sign-on** dialog box, In the **Mode** box, select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75205-145">In the **Single sign-on** dialog box, In the **Mode** box, select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="75205-147">In the **Absorb LMS Domain and URLs** section, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-147">In the **Absorb LMS Domain and URLs** section, do the following:</span></span>

    ![Absorb LMS Domain and URLs single sign-on information](./media/absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="75205-149">a.</span><span class="sxs-lookup"><span data-stu-id="75205-149">a.</span></span> <span data-ttu-id="75205-150">In the **Identifier** box, type a URL that uses the following syntax: `https://<subdomain>.myabsorb.com/Account/SAML`.</span><span class="sxs-lookup"><span data-stu-id="75205-150">In the **Identifier** box, type a URL that uses the following syntax: `https://<subdomain>.myabsorb.com/Account/SAML`.</span></span>

    <span data-ttu-id="75205-151">b.</span><span class="sxs-lookup"><span data-stu-id="75205-151">b.</span></span> <span data-ttu-id="75205-152">In the **Reply URL** box, type a URL that uses the following syntax: `https://<subdomain>.myabsorb.com/Account/SAML`.</span><span class="sxs-lookup"><span data-stu-id="75205-152">In the **Reply URL** box, type a URL that uses the following syntax: `https://<subdomain>.myabsorb.com/Account/SAML`.</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="75205-153">These URLs are not the real values.</span><span class="sxs-lookup"><span data-stu-id="75205-153">These URLs are not the real values.</span></span> <span data-ttu-id="75205-154">Update them with the actual Identifier and Reply URLs.</span><span class="sxs-lookup"><span data-stu-id="75205-154">Update them with the actual Identifier and Reply URLs.</span></span> <span data-ttu-id="75205-155">To obtain these values, contact the [Absorb LMS client support team](https://www.absorblms.com/support).</span><span class="sxs-lookup"><span data-stu-id="75205-155">To obtain these values, contact the [Absorb LMS client support team](https://www.absorblms.com/support).</span></span> 

4. <span data-ttu-id="75205-156">In the **SAML Signing Certificate** section, in the **Download** column, select **Metadata XML**, and then save the metadata file to your computer.</span><span class="sxs-lookup"><span data-stu-id="75205-156">In the **SAML Signing Certificate** section, in the **Download** column, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![The signing certificate download link](./media/absorblms-tutorial/tutorial_absorblms_certificate.png) 

5. <span data-ttu-id="75205-158">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="75205-158">Select **Save**.</span></span>

    ![Configure Single Sign-On Save button](./media/absorblms-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="75205-160">In the **Absorb LMS Configuration** section, select **Configure Absorb LMS** to open **Configure sign-on** window, and then copy the **Sign-Out URL** in the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="75205-160">In the **Absorb LMS Configuration** section, select **Configure Absorb LMS** to open **Configure sign-on** window, and then copy the **Sign-Out URL** in the **Quick Reference section.**</span></span>

    ![The Absorb LMS Configuration pane](./media/absorblms-tutorial/tutorial_absorblms_configure.png) 

7. <span data-ttu-id="75205-162">In a new web browser window, sign in to your Absorb LMS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="75205-162">In a new web browser window, sign in to your Absorb LMS company site as an administrator.</span></span>

8. <span data-ttu-id="75205-163">Select the **Account** button at the top right.</span><span class="sxs-lookup"><span data-stu-id="75205-163">Select the **Account** button at the top right.</span></span> 

    ![The Account button](./media/absorblms-tutorial/1.png)

9. <span data-ttu-id="75205-165">In the Account pane, select **Portal Settings**.</span><span class="sxs-lookup"><span data-stu-id="75205-165">In the Account pane, select **Portal Settings**.</span></span>

    ![The Portal Settings link](./media/absorblms-tutorial/2.png)
    
10. <span data-ttu-id="75205-167">Select the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="75205-167">Select the **Users** tab.</span></span>

    ![The Users tab](./media/absorblms-tutorial/3.png)

11. <span data-ttu-id="75205-169">On the single sign-on configuration page, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-169">On the single sign-on configuration page, do the following:</span></span>

    ![The single sign-on configuration page](./media/absorblms-tutorial/4.png)

    <span data-ttu-id="75205-171">a.</span><span class="sxs-lookup"><span data-stu-id="75205-171">a.</span></span> <span data-ttu-id="75205-172">In the **Mode** box, select **Identity Provider Initiated**.</span><span class="sxs-lookup"><span data-stu-id="75205-172">In the **Mode** box, select **Identity Provider Initiated**.</span></span>

    <span data-ttu-id="75205-173">b.</span><span class="sxs-lookup"><span data-stu-id="75205-173">b.</span></span> <span data-ttu-id="75205-174">In Notepad, open the certificate that you downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75205-174">In Notepad, open the certificate that you downloaded from the Azure portal.</span></span> <span data-ttu-id="75205-175">Remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tags.</span><span class="sxs-lookup"><span data-stu-id="75205-175">Remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tags.</span></span> <span data-ttu-id="75205-176">Then, in the **Key** box, paste the remaining content.</span><span class="sxs-lookup"><span data-stu-id="75205-176">Then, in the **Key** box, paste the remaining content.</span></span>
    
    <span data-ttu-id="75205-177">c.</span><span class="sxs-lookup"><span data-stu-id="75205-177">c.</span></span> <span data-ttu-id="75205-178">In the **Id Property** box, select the attribute that you configured as the user identifier in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75205-178">In the **Id Property** box, select the attribute that you configured as the user identifier in Azure AD.</span></span> <span data-ttu-id="75205-179">For example, if *userPrincipalName* is selected in Azure AD, select **Username**.</span><span class="sxs-lookup"><span data-stu-id="75205-179">For example, if *userPrincipalName* is selected in Azure AD, select **Username**.</span></span>

    <span data-ttu-id="75205-180">d.</span><span class="sxs-lookup"><span data-stu-id="75205-180">d.</span></span> <span data-ttu-id="75205-181">In the **Login URL** box, paste the **User Access URL** from the application's **Properties** page of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75205-181">In the **Login URL** box, paste the **User Access URL** from the application's **Properties** page of the Azure portal.</span></span>

    <span data-ttu-id="75205-182">e.</span><span class="sxs-lookup"><span data-stu-id="75205-182">e.</span></span> <span data-ttu-id="75205-183">In the **Logout URL**, paste the **Sign-Out URL** value that you copied from the **Configure sign-on** window of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75205-183">In the **Logout URL**, paste the **Sign-Out URL** value that you copied from the **Configure sign-on** window of the Azure portal.</span></span>

12. <span data-ttu-id="75205-184">Toggle **Only Allow SSO Login** to **On**.</span><span class="sxs-lookup"><span data-stu-id="75205-184">Toggle **Only Allow SSO Login** to **On**.</span></span>

    ![The Only Allow SSO Login toggle](./media/absorblms-tutorial/5.png)

13. <span data-ttu-id="75205-186">Select **Save.**</span><span class="sxs-lookup"><span data-stu-id="75205-186">Select **Save.**</span></span>

> [!TIP]
> <span data-ttu-id="75205-187">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span><span class="sxs-lookup"><span data-stu-id="75205-187">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="75205-188">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="75205-188">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="75205-189">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="75205-189">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75205-190">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="75205-190">Create an Azure AD test user</span></span>

<span data-ttu-id="75205-191">In this section, you create test user Britta Simon in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75205-191">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="75205-193">To create a test user in Azure AD, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-193">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="75205-194">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75205-194">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory button](./media/absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75205-196">To display the list of users, select **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="75205-196">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75205-198">At the top of the dialog box, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="75205-198">At the top of the dialog box, select **Add**.</span></span>
 
    ![The Add button](./media/absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75205-200">In the **User** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-200">In the **User** dialog box, do the following:</span></span>
 
    ![The User dialog box](./media/absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75205-202">a.</span><span class="sxs-lookup"><span data-stu-id="75205-202">a.</span></span> <span data-ttu-id="75205-203">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75205-203">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75205-204">b.</span><span class="sxs-lookup"><span data-stu-id="75205-204">b.</span></span> <span data-ttu-id="75205-205">In the **User name** textbox, type the email address of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75205-205">In the **User name** textbox, type the email address of Britta Simon.</span></span>

    <span data-ttu-id="75205-206">c.</span><span class="sxs-lookup"><span data-stu-id="75205-206">c.</span></span> <span data-ttu-id="75205-207">Select the **Show Password** check box, and then note the value in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="75205-207">Select the **Show Password** check box, and then note the value in the **Password** box.</span></span>

    <span data-ttu-id="75205-208">d.</span><span class="sxs-lookup"><span data-stu-id="75205-208">d.</span></span> <span data-ttu-id="75205-209">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75205-209">Select **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="75205-210">Create an Absorb LMS test user</span><span class="sxs-lookup"><span data-stu-id="75205-210">Create an Absorb LMS test user</span></span>

<span data-ttu-id="75205-211">For Azure AD users to sign in to Absorb LMS, they must be set up in Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="75205-211">For Azure AD users to sign in to Absorb LMS, they must be set up in Absorb LMS.</span></span>  

<span data-ttu-id="75205-212">For Absorb LMS, setup is a manual task.</span><span class="sxs-lookup"><span data-stu-id="75205-212">For Absorb LMS, setup is a manual task.</span></span>

<span data-ttu-id="75205-213">To set up a user account, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-213">To set up a user account, do the following:</span></span>

1. <span data-ttu-id="75205-214">Sign in to your Absorb LMS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="75205-214">Sign in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="75205-215">In the left pane, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="75205-215">In the left pane, select **Users**.</span></span>

    ![The Absorb LMS Users link](./media/absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="75205-217">In the **Users** pane, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="75205-217">In the **Users** pane, select **Users**.</span></span>

    ![The Users link](./media/absorblms-tutorial/absorblms_userssub.png)

4. <span data-ttu-id="75205-219">In the **Add New** drop-down list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="75205-219">In the **Add New** drop-down list, select **User**.</span></span>

    ![The Add New drop-down list](./media/absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="75205-221">On the **Add User** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-221">On the **Add User** page, do the following:</span></span>

    ![The Add User page](./media/absorblms-tutorial/user.png)

    <span data-ttu-id="75205-223">a.</span><span class="sxs-lookup"><span data-stu-id="75205-223">a.</span></span> <span data-ttu-id="75205-224">In the **First Name** box, type the first name, such as **Britta**.</span><span class="sxs-lookup"><span data-stu-id="75205-224">In the **First Name** box, type the first name, such as **Britta**.</span></span>

    <span data-ttu-id="75205-225">b.</span><span class="sxs-lookup"><span data-stu-id="75205-225">b.</span></span> <span data-ttu-id="75205-226">In the **Last Name** box, type the last name, such as **Simon**.</span><span class="sxs-lookup"><span data-stu-id="75205-226">In the **Last Name** box, type the last name, such as **Simon**.</span></span>
    
    <span data-ttu-id="75205-227">c.</span><span class="sxs-lookup"><span data-stu-id="75205-227">c.</span></span> <span data-ttu-id="75205-228">In the **Username** box, type a full name, such as **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="75205-228">In the **Username** box, type a full name, such as **Britta Simon**.</span></span>

    <span data-ttu-id="75205-229">d.</span><span class="sxs-lookup"><span data-stu-id="75205-229">d.</span></span> <span data-ttu-id="75205-230">In the **Password** box, type Britta Simon's password.</span><span class="sxs-lookup"><span data-stu-id="75205-230">In the **Password** box, type Britta Simon's password.</span></span>

    <span data-ttu-id="75205-231">e.</span><span class="sxs-lookup"><span data-stu-id="75205-231">e.</span></span> <span data-ttu-id="75205-232">In the **Confirm Password** box, retype the password.</span><span class="sxs-lookup"><span data-stu-id="75205-232">In the **Confirm Password** box, retype the password.</span></span>
    
    <span data-ttu-id="75205-233">f.</span><span class="sxs-lookup"><span data-stu-id="75205-233">f.</span></span> <span data-ttu-id="75205-234">Set the **Is Active** toggle to **Active**.</span><span class="sxs-lookup"><span data-stu-id="75205-234">Set the **Is Active** toggle to **Active**.</span></span>  

6. <span data-ttu-id="75205-235">Select **Save.**</span><span class="sxs-lookup"><span data-stu-id="75205-235">Select **Save.**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="75205-236">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="75205-236">Assign the Azure AD test user</span></span>

<span data-ttu-id="75205-237">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="75205-237">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Assign the user role][200]

<span data-ttu-id="75205-239">To assign user Britta Simon to Absorb LMS, do the following:</span><span class="sxs-lookup"><span data-stu-id="75205-239">To assign user Britta Simon to Absorb LMS, do the following:</span></span>

1. <span data-ttu-id="75205-240">In the Azure portal, open the applications view, go to the directory view, and then select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="75205-240">In the Azure portal, open the applications view, go to the directory view, and then select **Enterprise applications** > **All applications**.</span></span>

    ![The "All applications" link][201] 

2. <span data-ttu-id="75205-242">In the **Applications** list, select **Absorb LMS**.</span><span class="sxs-lookup"><span data-stu-id="75205-242">In the **Applications** list, select **Absorb LMS**.</span></span>

    ![The Absorb LMS link in the Applications list](./media/absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="75205-244">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="75205-244">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

4. <span data-ttu-id="75205-246">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="75205-246">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="75205-248">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="75205-248">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="75205-249">In the **Users and groups** dialog box, select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="75205-249">In the **Users and groups** dialog box, select the **Select** button.</span></span>

7. <span data-ttu-id="75205-250">In the **Add Assignment** dialog box, select the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="75205-250">In the **Add Assignment** dialog box, select the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="75205-251">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="75205-251">Test single sign-on</span></span>

<span data-ttu-id="75205-252">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="75205-252">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="75205-253">In the Access Panel, selecting the **Absorb LMS** tile automatically signs you in to your Absorb LMS application.</span><span class="sxs-lookup"><span data-stu-id="75205-253">In the Access Panel, selecting the **Absorb LMS** tile automatically signs you in to your Absorb LMS application.</span></span> <span data-ttu-id="75205-254">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="75205-254">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75205-255">Additional resources</span><span class="sxs-lookup"><span data-stu-id="75205-255">Additional resources</span></span>

* [<span data-ttu-id="75205-256">List of tutorials on how to integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75205-256">List of tutorials on how to integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="75205-257">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75205-257">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/absorblms-tutorial/tutorial_general_01.png
[2]: ./media/absorblms-tutorial/tutorial_general_02.png
[3]: ./media/absorblms-tutorial/tutorial_general_03.png
[4]: ./media/absorblms-tutorial/tutorial_general_04.png

[100]: ./media/absorblms-tutorial/tutorial_general_100.png

[200]: ./media/absorblms-tutorial/tutorial_general_200.png
[201]: ./media/absorblms-tutorial/tutorial_general_201.png
[202]: ./media/absorblms-tutorial/tutorial_general_202.png
[203]: ./media/absorblms-tutorial/tutorial_general_203.png
