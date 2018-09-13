---
title: 'Tutorial: Azure Active Directory integration with Flock | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Flock.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7b2c3ac5-17f1-49a0-8961-c541b258d4b1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 6589bbe581ec5e4ca3a18363ede427bf08f8b7cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866108"
---
# <a name="tutorial-azure-active-directory-integration-with-flock"></a><span data-ttu-id="3d9ac-103">Tutorial: Azure Active Directory integration with Flock</span><span class="sxs-lookup"><span data-stu-id="3d9ac-103">Tutorial: Azure Active Directory integration with Flock</span></span>

<span data-ttu-id="3d9ac-104">In this tutorial, you learn how to integrate Flock with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-104">In this tutorial, you learn how to integrate Flock with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d9ac-105">Integrating Flock with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-105">Integrating Flock with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d9ac-106">You can control in Azure AD who has access to Flock.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-106">You can control in Azure AD who has access to Flock.</span></span>
- <span data-ttu-id="3d9ac-107">You can enable your users to automatically get signed-on to Flock (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-107">You can enable your users to automatically get signed-on to Flock (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3d9ac-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3d9ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d9ac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3d9ac-110">Prerequisites</span></span>

<span data-ttu-id="3d9ac-111">To configure Azure AD integration with Flock, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-111">To configure Azure AD integration with Flock, you need the following items:</span></span>

- <span data-ttu-id="3d9ac-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3d9ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d9ac-113">A Flock single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3d9ac-113">A Flock single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d9ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d9ac-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d9ac-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d9ac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d9ac-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3d9ac-118">Scenario description</span></span>
<span data-ttu-id="3d9ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d9ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d9ac-121">Adding Flock from the gallery</span><span class="sxs-lookup"><span data-stu-id="3d9ac-121">Adding Flock from the gallery</span></span>
1. <span data-ttu-id="3d9ac-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d9ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flock-from-the-gallery"></a><span data-ttu-id="3d9ac-123">Adding Flock from the gallery</span><span class="sxs-lookup"><span data-stu-id="3d9ac-123">Adding Flock from the gallery</span></span>
<span data-ttu-id="3d9ac-124">To configure the integration of Flock into Azure AD, you need to add Flock from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-124">To configure the integration of Flock into Azure AD, you need to add Flock from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d9ac-125">**To add Flock from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d9ac-125">**To add Flock from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d9ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="3d9ac-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d9ac-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="3d9ac-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="3d9ac-133">In the search box, type **Flock**, select **Flock** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-133">In the search box, type **Flock**, select **Flock** from result panel then click **Add** button to add the application.</span></span>

    ![Flock in the results list](./media/flock-tutorial/tutorial_flock_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3d9ac-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d9ac-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3d9ac-136">In this section, you configure and test Azure AD single sign-on with Flock based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d9ac-136">In this section, you configure and test Azure AD single sign-on with Flock based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d9ac-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Flock is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Flock is to a user in Azure AD.</span></span> <span data-ttu-id="3d9ac-138">In other words, a link relationship between an Azure AD user and the related user in Flock needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-138">In other words, a link relationship between an Azure AD user and the related user in Flock needs to be established.</span></span>

<span data-ttu-id="3d9ac-139">To configure and test Azure AD single sign-on with Flock, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-139">To configure and test Azure AD single sign-on with Flock, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d9ac-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3d9ac-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3d9ac-142">**[Create a Flock test user](#create-a-flock-test-user)** - to have a counterpart of Britta Simon in Flock that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-142">**[Create a Flock test user](#create-a-flock-test-user)** - to have a counterpart of Britta Simon in Flock that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3d9ac-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3d9ac-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3d9ac-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d9ac-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3d9ac-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flock application.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flock application.</span></span>

<span data-ttu-id="3d9ac-147">**To configure Azure AD single sign-on with Flock, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d9ac-147">**To configure Azure AD single sign-on with Flock, perform the following steps:**</span></span>

1. <span data-ttu-id="3d9ac-148">In the Azure portal, on the **Flock** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-148">In the Azure portal, on the **Flock** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="3d9ac-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/flock-tutorial/tutorial_flock_samlbase.png)

1. <span data-ttu-id="3d9ac-152">On the **Flock Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-152">On the **Flock Domain and URLs** section, perform the following steps:</span></span>

    ![Flock Domain and URLs single sign-on information](./media/flock-tutorial/tutorial_flock_url.png)

    <span data-ttu-id="3d9ac-154">a.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-154">a.</span></span> <span data-ttu-id="3d9ac-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.flock.com/`</span><span class="sxs-lookup"><span data-stu-id="3d9ac-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.flock.com/`</span></span>

    <span data-ttu-id="3d9ac-156">b.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-156">b.</span></span> <span data-ttu-id="3d9ac-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.flock.com/`</span><span class="sxs-lookup"><span data-stu-id="3d9ac-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.flock.com/`</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d9ac-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-158">These values are not real.</span></span> <span data-ttu-id="3d9ac-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3d9ac-160">Contact [Flock Client support team](mailto:support@flock.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-160">Contact [Flock Client support team](mailto:support@flock.com) to get these values.</span></span>

1. <span data-ttu-id="3d9ac-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/flock-tutorial/tutorial_flock_certificate.png)

1. <span data-ttu-id="3d9ac-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/flock-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="3d9ac-165">On the **Flock Configuration** section, click **Configure Flock** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-165">On the **Flock Configuration** section, click **Configure Flock** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3d9ac-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3d9ac-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Flock Configuration](./media/flock-tutorial/tutorial_flock_configure.png) 

1. <span data-ttu-id="3d9ac-168">In a different web browser window, log in to your Flock company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-168">In a different web browser window, log in to your Flock company site as an administrator.</span></span>

1. <span data-ttu-id="3d9ac-169">Select **Authentication** tab from the left navigation panel and then select **SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-169">Select **Authentication** tab from the left navigation panel and then select **SAML Authentication**.</span></span>

    ![Flock Configuration](./media/flock-tutorial/configure1.png)

1. <span data-ttu-id="3d9ac-171">In the **SAML Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-171">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Flock Configuration](./media/flock-tutorial/configure2.png)

    <span data-ttu-id="3d9ac-173">a.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-173">a.</span></span> <span data-ttu-id="3d9ac-174">In the **SAML 2.0 Endpoint(HTTP)** textbox, paste **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-174">In the **SAML 2.0 Endpoint(HTTP)** textbox, paste **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="3d9ac-175">b.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-175">b.</span></span> <span data-ttu-id="3d9ac-176">In the **Identity Provider Issuer** textbox, paste **SAML Entity ID** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-176">In the **Identity Provider Issuer** textbox, paste **SAML Entity ID** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="3d9ac-177">c.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-177">c.</span></span> <span data-ttu-id="3d9ac-178">Open the downloaded **Certificate(Base64)** from Azure portal in notepad, paste the content into the **Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-178">Open the downloaded **Certificate(Base64)** from Azure portal in notepad, paste the content into the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="3d9ac-179">d.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-179">d.</span></span> <span data-ttu-id="3d9ac-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-180">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3d9ac-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3d9ac-181">Create an Azure AD test user</span></span>

<span data-ttu-id="3d9ac-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3d9ac-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d9ac-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d9ac-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/flock-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="3d9ac-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/flock-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="3d9ac-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/flock-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="3d9ac-191">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d9ac-191">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/flock-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3d9ac-193">a.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-193">a.</span></span> <span data-ttu-id="3d9ac-194">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-194">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d9ac-195">b.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-195">b.</span></span> <span data-ttu-id="3d9ac-196">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-196">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3d9ac-197">c.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-197">c.</span></span> <span data-ttu-id="3d9ac-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3d9ac-199">d.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-199">d.</span></span> <span data-ttu-id="3d9ac-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-200">Click **Create**.</span></span>

### <a name="create-a-flock-test-user"></a><span data-ttu-id="3d9ac-201">Create a Flock test user</span><span class="sxs-lookup"><span data-stu-id="3d9ac-201">Create a Flock test user</span></span>

<span data-ttu-id="3d9ac-202">To enable Azure AD users to log in to Flock, they must be provisioned into Flock.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-202">To enable Azure AD users to log in to Flock, they must be provisioned into Flock.</span></span> <span data-ttu-id="3d9ac-203">In the case of Flock, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-203">In the case of Flock, provisioning is a manual task.</span></span>

<span data-ttu-id="3d9ac-204">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d9ac-204">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3d9ac-205">Log in to your Flock company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-205">Log in to your Flock company site as an administrator.</span></span>

1. <span data-ttu-id="3d9ac-206">Click **Manage Team** from the left navigation panel.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-206">Click **Manage Team** from the left navigation panel.</span></span>

    ![Add Employee](./media/flock-tutorial/user1.png)

1. <span data-ttu-id="3d9ac-208">Click **Add Member** tab and then select **Team Members**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-208">Click **Add Member** tab and then select **Team Members**.</span></span>

    ![Add Employee](./media/flock-tutorial/user2.png)

1. <span data-ttu-id="3d9ac-210">Enter the email address of the user like **Brittasimon@contoso.com** and then select **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-210">Enter the email address of the user like **Brittasimon@contoso.com** and then select **Add Users**.</span></span>

    ![Add Employee](./media/flock-tutorial/user3.png)

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3d9ac-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3d9ac-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="3d9ac-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flock.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flock.</span></span>

![Assign the user role][200]

<span data-ttu-id="3d9ac-215">**To assign Britta Simon to Flock, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d9ac-215">**To assign Britta Simon to Flock, perform the following steps:**</span></span>

1. <span data-ttu-id="3d9ac-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="3d9ac-218">In the applications list, select **Flock**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-218">In the applications list, select **Flock**.</span></span>

    ![The Flock link in the Applications list](./media/flock-tutorial/tutorial_flock_app.png)

1. <span data-ttu-id="3d9ac-220">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-220">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="3d9ac-222">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-222">Click **Add** button.</span></span> <span data-ttu-id="3d9ac-223">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="3d9ac-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3d9ac-226">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-226">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3d9ac-227">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-227">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="3d9ac-228">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d9ac-228">Test single sign-on</span></span>

<span data-ttu-id="3d9ac-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d9ac-230">When you click the Flock tile in the Access Panel, you should get automatically signed-on to your Flock application.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-230">When you click the Flock tile in the Access Panel, you should get automatically signed-on to your Flock application.</span></span>
<span data-ttu-id="3d9ac-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d9ac-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3d9ac-232">Additional resources</span></span>

* [<span data-ttu-id="3d9ac-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d9ac-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3d9ac-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d9ac-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/flock-tutorial/tutorial_general_01.png
[2]: ./media/flock-tutorial/tutorial_general_02.png
[3]: ./media/flock-tutorial/tutorial_general_03.png
[4]: ./media/flock-tutorial/tutorial_general_04.png

[100]: ./media/flock-tutorial/tutorial_general_100.png

[200]: ./media/flock-tutorial/tutorial_general_200.png
[201]: ./media/flock-tutorial/tutorial_general_201.png
[202]: ./media/flock-tutorial/tutorial_general_202.png
[203]: ./media/flock-tutorial/tutorial_general_203.png
