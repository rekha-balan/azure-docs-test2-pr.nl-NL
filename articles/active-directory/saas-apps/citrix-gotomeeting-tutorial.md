---
title: 'Tutorial: Azure Active Directory integration with GoToMeeting | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bcaf19f2-5809-4e1c-acbc-21a8d3498ccf
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/02/2018
ms.author: jeedes
ms.openlocfilehash: b62b3b7f9f3bfd55237ed4d894954a0bde48e7fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967870"
---
# <a name="tutorial-azure-active-directory-integration-with-gotomeeting"></a><span data-ttu-id="5e9c5-103">Tutorial: Azure Active Directory integration with GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="5e9c5-103">Tutorial: Azure Active Directory integration with GoToMeeting</span></span>

<span data-ttu-id="5e9c5-104">In this tutorial, you learn how to integrate GoToMeeting with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e9c5-104">In this tutorial, you learn how to integrate GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e9c5-105">Integrating GoToMeeting with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-105">Integrating GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5e9c5-106">You can control in Azure AD who has access to GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-106">You can control in Azure AD who has access to GoToMeeting.</span></span>
- <span data-ttu-id="5e9c5-107">You can enable your users to automatically get signed-on to GoToMeeting (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-107">You can enable your users to automatically get signed-on to GoToMeeting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5e9c5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5e9c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5e9c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e9c5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5e9c5-110">Prerequisites</span></span>

<span data-ttu-id="5e9c5-111">To configure Azure AD integration with GoToMeeting, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-111">To configure Azure AD integration with GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="5e9c5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5e9c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e9c5-113">A GoToMeeting single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5e9c5-113">A GoToMeeting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e9c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e9c5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e9c5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e9c5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e9c5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e9c5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5e9c5-118">Scenario description</span></span>
<span data-ttu-id="5e9c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e9c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e9c5-121">Adding GoToMeeting from the gallery</span><span class="sxs-lookup"><span data-stu-id="5e9c5-121">Adding GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="5e9c5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gotomeeting-from-the-gallery"></a><span data-ttu-id="5e9c5-123">Adding GoToMeeting from the gallery</span><span class="sxs-lookup"><span data-stu-id="5e9c5-123">Adding GoToMeeting from the gallery</span></span>
<span data-ttu-id="5e9c5-124">To configure the integration of GoToMeeting into Azure AD, you need to add GoToMeeting from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-124">To configure the integration of GoToMeeting into Azure AD, you need to add GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5e9c5-125">**To add GoToMeeting from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9c5-125">**To add GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="5e9c5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5e9c5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="5e9c5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="5e9c5-133">In the search box, type **GoToMeeting**, select **GoToMeeting** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-133">In the search box, type **GoToMeeting**, select **GoToMeeting** from result panel then click **Add** button to add the application.</span></span>

    ![GoToMeeting in the results list](./media/citrix-gotomeeting-tutorial/tutorial_gotomeeting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5e9c5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9c5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5e9c5-136">In this section, you configure and test Azure AD single sign-on with GoToMeeting based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5e9c5-136">In this section, you configure and test Azure AD single sign-on with GoToMeeting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5e9c5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in GoToMeeting is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="5e9c5-138">In other words, a link relationship between an Azure AD user and the related user in GoToMeeting needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-138">In other words, a link relationship between an Azure AD user and the related user in GoToMeeting needs to be established.</span></span>

<span data-ttu-id="5e9c5-139">In GoToMeeting, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-139">In GoToMeeting, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5e9c5-140">To configure and test Azure AD single sign-on with GoToMeeting, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-140">To configure and test Azure AD single sign-on with GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5e9c5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5e9c5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e9c5-143">**[Create a GoToMeeting test user](#create-a-gotomeeting-test-user)** - to have a counterpart of Britta Simon in GoToMeeting that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-143">**[Create a GoToMeeting test user](#create-a-gotomeeting-test-user)** - to have a counterpart of Britta Simon in GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e9c5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e9c5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5e9c5-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9c5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5e9c5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GoToMeeting application.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GoToMeeting application.</span></span>

<span data-ttu-id="5e9c5-148">**To configure Azure AD single sign-on with GoToMeeting, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9c5-148">**To configure Azure AD single sign-on with GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9c5-149">In the Azure portal, on the **GoToMeeting** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-149">In the Azure portal, on the **GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="5e9c5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/citrix-gotomeeting-tutorial/tutorial_gotomeeting_samlbase.png)

3. <span data-ttu-id="5e9c5-153">On the **GoToMeeting Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-153">On the **GoToMeeting Domain and URLs** section, perform the following steps:</span></span>

    ![GoToMeeting Domain and URLs single sign-on information](./media/citrix-gotomeeting-tutorial/tutorial_gotomeeting_url.png)

    <span data-ttu-id="5e9c5-155">In the **Identifier** textbox, type the URL: `https://authentication.logmeininc.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="5e9c5-155">In the **Identifier** textbox, type the URL: `https://authentication.logmeininc.com/saml/sp`</span></span>

4. <span data-ttu-id="5e9c5-156">Click **Show Advanced URL configuration** and configure the below URLs</span><span class="sxs-lookup"><span data-stu-id="5e9c5-156">Click **Show Advanced URL configuration** and configure the below URLs</span></span>

    <span data-ttu-id="5e9c5-157">**Sign on URL** (keep this blank)</span><span class="sxs-lookup"><span data-stu-id="5e9c5-157">**Sign on URL** (keep this blank)</span></span>
    
    <span data-ttu-id="5e9c5-158">**Reply URL**: `https://authentication.logmeininc.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="5e9c5-158">**Reply URL**: `https://authentication.logmeininc.com/saml/acs`</span></span>
    
    <span data-ttu-id="5e9c5-159">**RelayState**:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-159">**RelayState**:</span></span>
    
    - <span data-ttu-id="5e9c5-160">For GoToMeeting App, use `https://global.gotomeeting.com`</span><span class="sxs-lookup"><span data-stu-id="5e9c5-160">For GoToMeeting App, use `https://global.gotomeeting.com`</span></span>
    
    - <span data-ttu-id="5e9c5-161">For GoToTraining, use `https://global.gototraining.com`</span><span class="sxs-lookup"><span data-stu-id="5e9c5-161">For GoToTraining, use `https://global.gototraining.com`</span></span>
    
    - <span data-ttu-id="5e9c5-162">For GoToWebinar, use `https://global.gotowebinar.com`</span><span class="sxs-lookup"><span data-stu-id="5e9c5-162">For GoToWebinar, use `https://global.gotowebinar.com`</span></span> 
    
    - <span data-ttu-id="5e9c5-163">For GoToAssist, use `https://app.gotoassist.com`</span><span class="sxs-lookup"><span data-stu-id="5e9c5-163">For GoToAssist, use `https://app.gotoassist.com`</span></span>
    
5. <span data-ttu-id="5e9c5-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/citrix-gotomeeting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e9c5-166">In a different browser window, log in to your [GoToMeeting Organization Center](https://organization.logmeininc.com/).</span><span class="sxs-lookup"><span data-stu-id="5e9c5-166">In a different browser window, log in to your [GoToMeeting Organization Center](https://organization.logmeininc.com/).</span></span> <span data-ttu-id="5e9c5-167">You will be prompted to confirm that the IdP has been updated</span><span class="sxs-lookup"><span data-stu-id="5e9c5-167">You will be prompted to confirm that the IdP has been updated</span></span>

7. <span data-ttu-id="5e9c5-168">Enable the "My Identity Provider has been updated with the new domain" checkbox.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-168">Enable the "My Identity Provider has been updated with the new domain" checkbox.</span></span> <span data-ttu-id="5e9c5-169">Click **Done** when finished.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-169">Click **Done** when finished.</span></span>


> [!TIP]
> <span data-ttu-id="5e9c5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="5e9c5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5e9c5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5e9c5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e9c5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5e9c5-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5e9c5-173">Create an Azure AD test user</span></span>

<span data-ttu-id="5e9c5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="5e9c5-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9c5-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9c5-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/citrix-gotomeeting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5e9c5-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/citrix-gotomeeting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5e9c5-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/citrix-gotomeeting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5e9c5-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9c5-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/citrix-gotomeeting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5e9c5-185">a.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-185">a.</span></span> <span data-ttu-id="5e9c5-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e9c5-187">b.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-187">b.</span></span> <span data-ttu-id="5e9c5-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5e9c5-189">c.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-189">c.</span></span> <span data-ttu-id="5e9c5-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5e9c5-191">d.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-191">d.</span></span> <span data-ttu-id="5e9c5-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-192">Click **Create**.</span></span>
 
### <a name="create-a-gotomeeting-test-user"></a><span data-ttu-id="5e9c5-193">Create a GoToMeeting test user</span><span class="sxs-lookup"><span data-stu-id="5e9c5-193">Create a GoToMeeting test user</span></span>

<span data-ttu-id="5e9c5-194">In this section, a user called Britta Simon is created in GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-194">In this section, a user called Britta Simon is created in GoToMeeting.</span></span> <span data-ttu-id="5e9c5-195">GoToMeeting supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-195">GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="5e9c5-196">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-196">There is no action item for you in this section.</span></span> <span data-ttu-id="5e9c5-197">If a user doesn't already exist in GoToMeeting, a new one is created when you attempt to access GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-197">If a user doesn't already exist in GoToMeeting, a new one is created when you attempt to access GoToMeeting.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9c5-198">If you need to create a user manually, Contact [GoToMeeting support team](https://support.logmeininc.com/gotomeeting).</span><span class="sxs-lookup"><span data-stu-id="5e9c5-198">If you need to create a user manually, Contact [GoToMeeting support team](https://support.logmeininc.com/gotomeeting).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5e9c5-199">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5e9c5-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="5e9c5-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GoToMeeting.</span></span>

![Assign the user role][200] 

<span data-ttu-id="5e9c5-202">**To assign Britta Simon to GoToMeeting, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9c5-202">**To assign Britta Simon to GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9c5-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="5e9c5-205">In the applications list, select **GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-205">In the applications list, select **GoToMeeting**.</span></span>

    ![The GoToMeeting link in the Applications list](./media/citrix-gotomeeting-tutorial/tutorial_gotomeeting_app.png)  

3. <span data-ttu-id="5e9c5-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-207">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="5e9c5-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-209">Click **Add** button.</span></span> <span data-ttu-id="5e9c5-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="5e9c5-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5e9c5-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e9c5-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5e9c5-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9c5-215">Test single sign-on</span></span>

<span data-ttu-id="5e9c5-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5e9c5-217">When you click the GoToMeeting tile in the Access Panel, you should get automatically signed-on to your GoToMeeting application.</span><span class="sxs-lookup"><span data-stu-id="5e9c5-217">When you click the GoToMeeting tile in the Access Panel, you should get automatically signed-on to your GoToMeeting application.</span></span>
<span data-ttu-id="5e9c5-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e9c5-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5e9c5-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5e9c5-219">Additional resources</span></span>

* [<span data-ttu-id="5e9c5-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e9c5-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5e9c5-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5e9c5-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="5e9c5-222">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="5e9c5-222">Configure User Provisioning</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-citrixgotomeeting-provisioning-tutorial)


<!--Image references-->

[1]: ./media/gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/gotomeeting-tutorial/tutorial_general_203.png

