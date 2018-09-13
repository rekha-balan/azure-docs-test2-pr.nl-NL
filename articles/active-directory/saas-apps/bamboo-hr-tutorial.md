---
title: 'Tutorial: Azure Active Directory integration with BambooHR | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BambooHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2018
ms.author: jeedes
ms.openlocfilehash: dc6664321588d383b4656199c3e8ea79159ca850
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867684"
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="cc1c1-103">Tutorial: Azure Active Directory integration with BambooHR</span><span class="sxs-lookup"><span data-stu-id="cc1c1-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="cc1c1-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc1c1-105">Integrating BambooHR with Azure AD provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-105">Integrating BambooHR with Azure AD provides the following benefits:</span></span>

- <span data-ttu-id="cc1c1-106">You can control in Azure AD who has access to BambooHR.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-106">You can control in Azure AD who has access to BambooHR.</span></span>
- <span data-ttu-id="cc1c1-107">You can enable your users to automatically get signed in to BambooHR by using single sign-on (SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-107">You can enable your users to automatically get signed in to BambooHR by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cc1c1-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="cc1c1-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc1c1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc1c1-110">Prerequisites</span></span>

<span data-ttu-id="cc1c1-111">To configure Azure AD integration with BambooHR, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="cc1c1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cc1c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc1c1-113">A BambooHR SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cc1c1-113">A BambooHR SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc1c1-114">When you test the steps in this tutorial, we recommend that you not use a production environment.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-114">When you test the steps in this tutorial, we recommend that you not use a production environment.</span></span>

<span data-ttu-id="cc1c1-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="cc1c1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc1c1-117">If you don't have an Azure AD trial environment, you can [get a free, one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-117">If you don't have an Azure AD trial environment, you can [get a free, one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc1c1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cc1c1-118">Scenario description</span></span>
<span data-ttu-id="cc1c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="cc1c1-120">The scenario that this tutorial outlines consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-120">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc1c1-121">Adding BambooHR from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc1c1-121">Adding BambooHR from the gallery</span></span>
1. <span data-ttu-id="cc1c1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-bamboohr-from-the-gallery"></a><span data-ttu-id="cc1c1-123">Add BambooHR from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc1c1-123">Add BambooHR from the gallery</span></span>
<span data-ttu-id="cc1c1-124">To configure the integration of BambooHR into Azure AD, add BambooHR from the gallery to your list of managed SaaS apps by doing the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-124">To configure the integration of BambooHR into Azure AD, add BambooHR from the gallery to your list of managed SaaS apps by doing the following:</span></span>

1. <span data-ttu-id="cc1c1-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="cc1c1-127">Select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-127">Select **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications pane][2]
    
1. <span data-ttu-id="cc1c1-129">To add an application, select **New application**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-129">To add an application, select **New application**.</span></span>

    ![The "New application" button][3]

1. <span data-ttu-id="cc1c1-131">In the search box, type **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-131">In the search box, type **BambooHR**.</span></span> <span data-ttu-id="cc1c1-132">In the results list, select **BambooHR**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-132">In the results list, select **BambooHR**, and then select **Add**.</span></span>

    ![BambooHR in the results list](./media/bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cc1c1-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1c1-134">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cc1c1-135">In this section, you configure and test Azure AD SSO with BambooHR by using test user "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="cc1c1-135">In this section, you configure and test Azure AD SSO with BambooHR by using test user "Britta Simon."</span></span>

<span data-ttu-id="cc1c1-136">For SSO to work, Azure AD needs to know what its counterpart user is in BambooHR.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-136">For SSO to work, Azure AD needs to know what its counterpart user is in BambooHR.</span></span> <span data-ttu-id="cc1c1-137">In other words, you must establish a link relationship between the Azure AD user and the related user in BambooHR.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-137">In other words, you must establish a link relationship between the Azure AD user and the related user in BambooHR.</span></span>

<span data-ttu-id="cc1c1-138">To establish the link relationship in BambooHR, assign the Azure AD **user name** value as the BambooHR **Username** value.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-138">To establish the link relationship in BambooHR, assign the Azure AD **user name** value as the BambooHR **Username** value.</span></span>

<span data-ttu-id="cc1c1-139">To configure and test Azure AD SSO with BambooHR, complete the building blocks in the next five sections.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-139">To configure and test Azure AD SSO with BambooHR, complete the building blocks in the next five sections.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cc1c1-140">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1c1-140">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cc1c1-141">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your BambooHR application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-141">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your BambooHR application by doing the following:</span></span>

1. <span data-ttu-id="cc1c1-142">In the Azure portal, on the **BambooHR** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-142">In the Azure portal, on the **BambooHR** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="cc1c1-144">In the **Single sign-on** window, in the **Mode** drop-down list, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-144">In the **Single sign-on** window, in the **Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Single sign-on window](./media/bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

1. <span data-ttu-id="cc1c1-146">Under **BambooHR Domain and URLs**, do the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-146">Under **BambooHR Domain and URLs**, do the following:</span></span>

    ![The BambooHR Domain and URLs section](./media/bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="cc1c1-148">a.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-148">a.</span></span> <span data-ttu-id="cc1c1-149">In the **Sign on URL** box, type a URL in the following format: `https://<company>.bamboohr.com`.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-149">In the **Sign on URL** box, type a URL in the following format: `https://<company>.bamboohr.com`.</span></span>

    <span data-ttu-id="cc1c1-150">b.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-150">b.</span></span> <span data-ttu-id="cc1c1-151">In the **Identifier** box, type a value: `BambooHR-SAML`.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-151">In the **Identifier** box, type a value: `BambooHR-SAML`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc1c1-152">The **Sign on URL** value is not real.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-152">The **Sign on URL** value is not real.</span></span> <span data-ttu-id="cc1c1-153">Update it with your actual sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-153">Update it with your actual sign-on URL.</span></span> <span data-ttu-id="cc1c1-154">To obtain the value, contact the [BambooHR client support team](https://www.bamboohr.com/contact.php).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-154">To obtain the value, contact the [BambooHR client support team](https://www.bamboohr.com/contact.php).</span></span> 
 
1. <span data-ttu-id="cc1c1-155">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-155">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

1. <span data-ttu-id="cc1c1-157">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-157">Select **Save**.</span></span>

    ![The Save button](./media/bamboo-hr-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cc1c1-159">Under **BambooHR Configuration**, select **Configure BambooHR** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-159">Under **BambooHR Configuration**, select **Configure BambooHR** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="cc1c1-160">In the **Quick Reference** section, copy the **SAML Single Sign-On Service URL** for later use.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-160">In the **Quick Reference** section, copy the **SAML Single Sign-On Service URL** for later use.</span></span>

    ![BambooHR configuration](./media/bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

1. <span data-ttu-id="cc1c1-162">In a new window, sign in to your BambooHR company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-162">In a new window, sign in to your BambooHR company site as an administrator.</span></span>

1. <span data-ttu-id="cc1c1-163">On the home page, do the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-163">On the home page, do the following:</span></span>
   
    <span data-ttu-id="cc1c1-164">![The BambooHR Single Sign-On page](./media/bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cc1c1-164">![The BambooHR Single Sign-On page](./media/bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="cc1c1-165">a.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-165">a.</span></span> <span data-ttu-id="cc1c1-166">Select **Apps**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-166">Select **Apps**.</span></span>
   
    <span data-ttu-id="cc1c1-167">b.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-167">b.</span></span> <span data-ttu-id="cc1c1-168">In the **Apps** pane, select **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-168">In the **Apps** pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="cc1c1-169">c.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-169">c.</span></span> <span data-ttu-id="cc1c1-170">Select **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-170">Select **SAML Single Sign-On**.</span></span>

1. <span data-ttu-id="cc1c1-171">In the **SAML Single Sign-On** pane, do the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-171">In the **SAML Single Sign-On** pane, do the following:</span></span>
   
    <span data-ttu-id="cc1c1-172">![The SAML Single Sign-On pane](./media/bamboo-hr-tutorial/IC796692.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cc1c1-172">![The SAML Single Sign-On pane](./media/bamboo-hr-tutorial/IC796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="cc1c1-173">a.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-173">a.</span></span> <span data-ttu-id="cc1c1-174">Into the **SSO Login Url** box, paste the **SAML Single Sign-On Service URL** that you copied from the Azure portal in step 6.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-174">Into the **SSO Login Url** box, paste the **SAML Single Sign-On Service URL** that you copied from the Azure portal in step 6.</span></span>
      
    <span data-ttu-id="cc1c1-175">b.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-175">b.</span></span> <span data-ttu-id="cc1c1-176">In Notepad, open the base-64 encoded certificate that you downloaded from the Azure portal, copy its content, and then paste it into the **X.509 Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-176">In Notepad, open the base-64 encoded certificate that you downloaded from the Azure portal, copy its content, and then paste it into the **X.509 Certificate** box.</span></span>
   
    <span data-ttu-id="cc1c1-177">c.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-177">c.</span></span> <span data-ttu-id="cc1c1-178">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-178">Select **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cc1c1-179">While you're setting up the app, you can read a concise version of these instructions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-179">While you're setting up the app, you can read a concise version of these instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cc1c1-180">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and then access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-180">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc1c1-181">For information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-181">For information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cc1c1-182">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc1c1-182">Create an Azure AD test user</span></span>

<span data-ttu-id="cc1c1-183">The objective of this section is to create a test user called Britta Simon in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-183">The objective of this section is to create a test user called Britta Simon in the Azure portal.</span></span>

   ![Create Azure AD test user Britta Simon][100]

<span data-ttu-id="cc1c1-185">To create a test user in Azure AD, do the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-185">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="cc1c1-186">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-186">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory button](./media/bamboo-hr-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="cc1c1-188">To display the list of users, go to **Users and groups**, and then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-188">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/bamboo-hr-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="cc1c1-190">At the top of the **All Users** pane, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-190">At the top of the **All Users** pane, select **Add**.</span></span>

    ![The Add button](./media/bamboo-hr-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="cc1c1-192">In the **User** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-192">In the **User** window, do the following:</span></span>

    ![The User window](./media/bamboo-hr-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cc1c1-194">a.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-194">a.</span></span> <span data-ttu-id="cc1c1-195">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc1c1-196">b.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-196">b.</span></span> <span data-ttu-id="cc1c1-197">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="cc1c1-198">c.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-198">c.</span></span> <span data-ttu-id="cc1c1-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="cc1c1-200">d.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-200">d.</span></span> <span data-ttu-id="cc1c1-201">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-201">Select **Create**.</span></span>
 
### <a name="create-a-bamboohr-test-user"></a><span data-ttu-id="cc1c1-202">Create a BambooHR test user</span><span class="sxs-lookup"><span data-stu-id="cc1c1-202">Create a BambooHR test user</span></span>

<span data-ttu-id="cc1c1-203">To enable Azure AD users to sign in to BambooHR, set them up manually in BambooHR by doing the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-203">To enable Azure AD users to sign in to BambooHR, set them up manually in BambooHR by doing the following:</span></span>

1. <span data-ttu-id="cc1c1-204">Sign in to your **BambooHR** site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-204">Sign in to your **BambooHR** site as an administrator.</span></span>

1. <span data-ttu-id="cc1c1-205">In the toolbar at the top, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-205">In the toolbar at the top, select **Settings**.</span></span>
   
    <span data-ttu-id="cc1c1-206">![The Settings button](./media/bamboo-hr-tutorial/IC796694.png "Setting")</span><span class="sxs-lookup"><span data-stu-id="cc1c1-206">![The Settings button](./media/bamboo-hr-tutorial/IC796694.png "Setting")</span></span>

1. <span data-ttu-id="cc1c1-207">Select **Overview**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-207">Select **Overview**.</span></span>

1. <span data-ttu-id="cc1c1-208">In the left pane, select **Security** > **Users**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-208">In the left pane, select **Security** > **Users**.</span></span>

1. <span data-ttu-id="cc1c1-209">Type the username, password, and email address of the valid Azure AD account that you want to set up.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-209">Type the username, password, and email address of the valid Azure AD account that you want to set up.</span></span>

1. <span data-ttu-id="cc1c1-210">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-210">Select **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="cc1c1-211">To set up Azure AD user accounts, you can also use BambooHR user account-creation tools or APIs.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-211">To set up Azure AD user accounts, you can also use BambooHR user account-creation tools or APIs.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cc1c1-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc1c1-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="cc1c1-213">Enable user Britta Simon to use Azure SSO by granting access to BambooHR.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-213">Enable user Britta Simon to use Azure SSO by granting access to BambooHR.</span></span>

![Assign the user role][200] 

<span data-ttu-id="cc1c1-215">To assign user Britta Simon to BambooHR, do the following:</span><span class="sxs-lookup"><span data-stu-id="cc1c1-215">To assign user Britta Simon to BambooHR, do the following:</span></span>

1. <span data-ttu-id="cc1c1-216">In the Azure portal, open the applications view, go to the directory view, and then select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-216">In the Azure portal, open the applications view, go to the directory view, and then select **Enterprise applications** > **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cc1c1-218">In the **Enterprise Applications** list, select **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-218">In the **Enterprise Applications** list, select **BambooHR**.</span></span>

    ![The BambooHR link in the Enterprise Applications list](./media/bamboo-hr-tutorial/tutorial_bamboohr_app.png)  

1. <span data-ttu-id="cc1c1-220">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-220">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="cc1c1-222">Select the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-222">Select the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="cc1c1-224">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-224">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="cc1c1-225">Select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-225">Select the **Select** button.</span></span>

1. <span data-ttu-id="cc1c1-226">In the **Add Assignment** window, select the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-226">In the **Add Assignment** window, select the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cc1c1-227">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1c1-227">Test single sign-on</span></span>

<span data-ttu-id="cc1c1-228">Test your Azure AD SSO configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-228">Test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="cc1c1-229">When you select the **BambooHR** tile in the Access Panel, you should get automatically signed in to your BambooHR application.</span><span class="sxs-lookup"><span data-stu-id="cc1c1-229">When you select the **BambooHR** tile in the Access Panel, you should get automatically signed in to your BambooHR application.</span></span>

<span data-ttu-id="cc1c1-230">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc1c1-230">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc1c1-231">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cc1c1-231">Additional resources</span></span>

* [<span data-ttu-id="cc1c1-232">List of tutorials on integrating SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc1c1-232">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cc1c1-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc1c1-233">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/bamboo-hr-tutorial/tutorial_general_203.png

