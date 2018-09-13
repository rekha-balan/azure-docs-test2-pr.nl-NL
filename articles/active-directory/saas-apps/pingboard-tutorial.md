---
title: 'Tutorial: Azure Active Directory integration with Pingboard | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 794e3f6fe568d76f0687caa36709185f2a538270
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865279"
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="e4eef-103">Tutorial: Azure Active Directory integration with Pingboard</span><span class="sxs-lookup"><span data-stu-id="e4eef-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="e4eef-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e4eef-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4eef-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e4eef-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e4eef-106">You can control in Azure AD who has access to Pingboard</span><span class="sxs-lookup"><span data-stu-id="e4eef-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="e4eef-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e4eef-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4eef-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4eef-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e4eef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e4eef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4eef-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4eef-110">Prerequisites</span></span>

<span data-ttu-id="e4eef-111">To configure Azure AD integration with Pingboard, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e4eef-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="e4eef-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e4eef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4eef-113">A Pingboard single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e4eef-113">A Pingboard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4eef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e4eef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4eef-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e4eef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4eef-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e4eef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4eef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4eef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4eef-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e4eef-118">Scenario description</span></span>
<span data-ttu-id="e4eef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e4eef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4eef-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e4eef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4eef-121">Adding Pingboard from the gallery</span><span class="sxs-lookup"><span data-stu-id="e4eef-121">Adding Pingboard from the gallery</span></span>
1. <span data-ttu-id="e4eef-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e4eef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="e4eef-123">Adding Pingboard from the gallery</span><span class="sxs-lookup"><span data-stu-id="e4eef-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="e4eef-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e4eef-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e4eef-125">**To add Pingboard from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e4eef-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e4eef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e4eef-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e4eef-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications][2]

1. <span data-ttu-id="e4eef-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="e4eef-131">Click **Add** button on the top of the dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e4eef-133">In the search box, type **Pingboard**, select **Pingboard** from result panel and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e4eef-133">In the search box, type **Pingboard**, select **Pingboard** from result panel and then click **Add** button to add the application.</span></span>

    ![Pingboard in the results list](./media/pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e4eef-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e4eef-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e4eef-136">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e4eef-136">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e4eef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4eef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="e4eef-138">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e4eef-138">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="e4eef-139">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e4eef-139">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="e4eef-140">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e4eef-140">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e4eef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e4eef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e4eef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e4eef-143">**[Create a Pingboard test user](#create-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e4eef-143">**[Create a Pingboard test user](#create-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e4eef-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e4eef-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e4eef-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e4eef-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e4eef-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e4eef-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e4eef-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pingboard application.</span><span class="sxs-lookup"><span data-stu-id="e4eef-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="e4eef-148">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e4eef-148">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="e4eef-149">In the Azure portal, on the **Pingboard** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-149">In the Azure portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1.  <span data-ttu-id="e4eef-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e4eef-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/pingboard-tutorial/tutorial_pingboard_samlbase.png)

1. <span data-ttu-id="e4eef-153">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e4eef-153">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Pingboard Domain and URLs single sign-on information IDP](./media/pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="e4eef-155">a.</span><span class="sxs-lookup"><span data-stu-id="e4eef-155">a.</span></span> <span data-ttu-id="e4eef-156">In the **Identifier** textbox, type the value as: `http://app.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="e4eef-156">In the **Identifier** textbox, type the value as: `http://app.pingboard.com/sp`</span></span>

    <span data-ttu-id="e4eef-157">b.</span><span class="sxs-lookup"><span data-stu-id="e4eef-157">b.</span></span> <span data-ttu-id="e4eef-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="e4eef-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

1. <span data-ttu-id="e4eef-159">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e4eef-159">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Pingboard Domain and URLs single sign-on information SP](./media/pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

     <span data-ttu-id="e4eef-161">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="e4eef-161">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.pingboard.com/sign_in`</span></span>

    > [!NOTE]
    > <span data-ttu-id="e4eef-162">Please note that these values are not real.</span><span class="sxs-lookup"><span data-stu-id="e4eef-162">Please note that these values are not real.</span></span> <span data-ttu-id="e4eef-163">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="e4eef-163">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="e4eef-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e4eef-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span>

1. <span data-ttu-id="e4eef-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e4eef-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Pingboard metadata xml](./media/pingboard-tutorial/tutorial_pingboard_certificate.png)

1. <span data-ttu-id="e4eef-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e4eef-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/pingboard-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e4eef-169">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span><span class="sxs-lookup"><span data-stu-id="e4eef-169">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="e4eef-170">You must be a Pingboard admin to set up single sign on.</span><span class="sxs-lookup"><span data-stu-id="e4eef-170">You must be a Pingboard admin to set up single sign on.</span></span>

1. <span data-ttu-id="e4eef-171">From the top menu,, select **Apps > Integrations**</span><span class="sxs-lookup"><span data-stu-id="e4eef-171">From the top menu,, select **Apps > Integrations**</span></span>

    ![Configure Single Sign-On](./media/pingboard-tutorial/Pingboard_integration.png)

1. <span data-ttu-id="e4eef-173">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span><span class="sxs-lookup"><span data-stu-id="e4eef-173">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Pingboard Single Sign-On Integration](./media/pingboard-tutorial/Pingboard_aad.png)

1. <span data-ttu-id="e4eef-175">In the modal that follows click **"Configure"**</span><span class="sxs-lookup"><span data-stu-id="e4eef-175">In the modal that follows click **"Configure"**</span></span>

    ![Pingboard configuration button](./media/pingboard-tutorial/Pingboard_configure.png)

1. <span data-ttu-id="e4eef-177">On the following page, you notice that "Azure SSO Integration is enabled".</span><span class="sxs-lookup"><span data-stu-id="e4eef-177">On the following page, you notice that "Azure SSO Integration is enabled".</span></span> <span data-ttu-id="e4eef-178">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-178">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Pingboard SSO configuration screen](./media/pingboard-tutorial/Pingboard_sso_configure.png)

1. <span data-ttu-id="e4eef-180">The file is validated, and if everything is correct, single sign-on will now be enabled.</span><span class="sxs-lookup"><span data-stu-id="e4eef-180">The file is validated, and if everything is correct, single sign-on will now be enabled.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e4eef-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e4eef-181">Create an Azure AD test user</span></span>

<span data-ttu-id="e4eef-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="e4eef-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e4eef-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e4eef-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/pingboard-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="e4eef-187">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/pingboard-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e4eef-189">At the top of the dialog, click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="e4eef-189">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>

    ![Add button](./media/pingboard-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="e4eef-191">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e4eef-191">On the **User** dialog page, perform the following steps:</span></span>

    ![The User dialog box](./media/pingboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e4eef-193">a.</span><span class="sxs-lookup"><span data-stu-id="e4eef-193">a.</span></span> <span data-ttu-id="e4eef-194">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4eef-195">b.</span><span class="sxs-lookup"><span data-stu-id="e4eef-195">b.</span></span> <span data-ttu-id="e4eef-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4eef-197">c.</span><span class="sxs-lookup"><span data-stu-id="e4eef-197">c.</span></span> <span data-ttu-id="e4eef-198">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e4eef-199">d.</span><span class="sxs-lookup"><span data-stu-id="e4eef-199">d.</span></span> <span data-ttu-id="e4eef-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-200">Click **Create**.</span></span>

### <a name="create-a-pingboard-test-user"></a><span data-ttu-id="e4eef-201">Create a Pingboard test user</span><span class="sxs-lookup"><span data-stu-id="e4eef-201">Create a Pingboard test user</span></span>

<span data-ttu-id="e4eef-202">The objective of this section is to create a user called Britta Simon in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e4eef-202">The objective of this section is to create a user called Britta Simon in Pingboard.</span></span> <span data-ttu-id="e4eef-203">Pingboard supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="e4eef-203">Pingboard supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="e4eef-204">You can find more details [here](pingboard-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="e4eef-204">You can find more details [here](pingboard-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="e4eef-205">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="e4eef-205">**If you need to create user manually, perform following steps:**</span></span>

1. <span data-ttu-id="e4eef-206">Log in to your Pingboard company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e4eef-206">Log in to your Pingboard company site as an administrator.</span></span>

1. <span data-ttu-id="e4eef-207">Click **“Add Employee”** button on **Directory** page.</span><span class="sxs-lookup"><span data-stu-id="e4eef-207">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Add Employee](./media/pingboard-tutorial/create_testuser_add.png)

1. <span data-ttu-id="e4eef-209">On the **“Add Employee”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e4eef-209">On the **“Add Employee”** dialog page, perform the following steps:</span></span>

    ![Invite People](./media/pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="e4eef-211">a.</span><span class="sxs-lookup"><span data-stu-id="e4eef-211">a.</span></span> <span data-ttu-id="e4eef-212">In the **Full Name** textbox, type the full name of user like **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-212">In the **Full Name** textbox, type the full name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="e4eef-213">b.</span><span class="sxs-lookup"><span data-stu-id="e4eef-213">b.</span></span> <span data-ttu-id="e4eef-214">In the **Email** textbox, type the email address of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-214">In the **Email** textbox, type the email address of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e4eef-215">c.</span><span class="sxs-lookup"><span data-stu-id="e4eef-215">c.</span></span> <span data-ttu-id="e4eef-216">In the **Job Title** textbox, type the job title of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-216">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="e4eef-217">d.</span><span class="sxs-lookup"><span data-stu-id="e4eef-217">d.</span></span> <span data-ttu-id="e4eef-218">In the **Location** dropdown, select the location  of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4eef-218">In the **Location** dropdown, select the location  of Britta Simon.</span></span>

    <span data-ttu-id="e4eef-219">e.</span><span class="sxs-lookup"><span data-stu-id="e4eef-219">e.</span></span> <span data-ttu-id="e4eef-220">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-220">Click **Add**.</span></span>

1. <span data-ttu-id="e4eef-221">A confirmation screen comes up to confirm the addition of user.</span><span class="sxs-lookup"><span data-stu-id="e4eef-221">A confirmation screen comes up to confirm the addition of user.</span></span>

    ![confirm](./media/pingboard-tutorial/create_testuser_confirm.png)

    > [!NOTE]
    > <span data-ttu-id="e4eef-223">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="e4eef-223">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e4eef-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e4eef-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="e4eef-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e4eef-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pingboard.</span></span>

![Assign User][200] 

<span data-ttu-id="e4eef-227">**To assign Britta Simon to Pingboard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e4eef-227">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="e4eef-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e4eef-230">In the applications list, select **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-230">In the applications list, select **Pingboard**.</span></span>

    ![The Pingboard link in the Applications list](./media/pingboard-tutorial/tutorial_pingboard_app.png) 

1. <span data-ttu-id="e4eef-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e4eef-232">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="e4eef-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e4eef-234">Click **Add** button.</span></span> <span data-ttu-id="e4eef-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e4eef-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e4eef-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e4eef-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e4eef-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e4eef-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e4eef-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e4eef-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e4eef-240">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e4eef-240">Test single sign-on</span></span>

<span data-ttu-id="e4eef-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e4eef-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="e4eef-242">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e4eef-242">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e4eef-243">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span><span class="sxs-lookup"><span data-stu-id="e4eef-243">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4eef-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e4eef-244">Additional resources</span></span>

* [<span data-ttu-id="e4eef-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4eef-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e4eef-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e4eef-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="e4eef-247">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="e4eef-247">Configure User Provisioning</span></span>](pingboard-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/pingboard-tutorial/tutorial_general_01.png
[2]: ./media/pingboard-tutorial/tutorial_general_02.png
[3]: ./media/pingboard-tutorial/tutorial_general_03.png
[4]: ./media/pingboard-tutorial/tutorial_general_04.png

[100]: ./media/pingboard-tutorial/tutorial_general_100.png

[200]: ./media/pingboard-tutorial/tutorial_general_200.png
[201]: ./media/pingboard-tutorial/tutorial_general_201.png
[202]: ./media/pingboard-tutorial/tutorial_general_202.png
[203]: ./media/pingboard-tutorial/tutorial_general_203.png