---
title: 'Tutorial: Azure Active Directory integration with Reviewsnap | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Reviewsnap.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b00fb373-2b31-4dcf-84ce-abc29e4c639c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: 8c66985c7a1d9084ab2a264b1ba799b1fdfa3b0f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967728"
---
# <a name="tutorial-azure-active-directory-integration-with-reviewsnap"></a><span data-ttu-id="2e55c-103">Tutorial: Azure Active Directory integration with Reviewsnap</span><span class="sxs-lookup"><span data-stu-id="2e55c-103">Tutorial: Azure Active Directory integration with Reviewsnap</span></span>

<span data-ttu-id="2e55c-104">In this tutorial, you learn how to integrate Reviewsnap with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e55c-104">In this tutorial, you learn how to integrate Reviewsnap with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e55c-105">Integrating Reviewsnap with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2e55c-105">Integrating Reviewsnap with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e55c-106">You can control in Azure AD who has access to Reviewsnap.</span><span class="sxs-lookup"><span data-stu-id="2e55c-106">You can control in Azure AD who has access to Reviewsnap.</span></span>
- <span data-ttu-id="2e55c-107">You can enable your users to automatically get signed-on to Reviewsnap (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="2e55c-107">You can enable your users to automatically get signed-on to Reviewsnap (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2e55c-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2e55c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2e55c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2e55c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e55c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2e55c-110">Prerequisites</span></span>

<span data-ttu-id="2e55c-111">To configure Azure AD integration with Reviewsnap, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2e55c-111">To configure Azure AD integration with Reviewsnap, you need the following items:</span></span>

- <span data-ttu-id="2e55c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2e55c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e55c-113">A Reviewsnap single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2e55c-113">A Reviewsnap single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e55c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2e55c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e55c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2e55c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e55c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2e55c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e55c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e55c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e55c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2e55c-118">Scenario description</span></span>
<span data-ttu-id="2e55c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2e55c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e55c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2e55c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e55c-121">Adding Reviewsnap from the gallery</span><span class="sxs-lookup"><span data-stu-id="2e55c-121">Adding Reviewsnap from the gallery</span></span>
1. <span data-ttu-id="2e55c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e55c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reviewsnap-from-the-gallery"></a><span data-ttu-id="2e55c-123">Adding Reviewsnap from the gallery</span><span class="sxs-lookup"><span data-stu-id="2e55c-123">Adding Reviewsnap from the gallery</span></span>
<span data-ttu-id="2e55c-124">To configure the integration of Reviewsnap into Azure AD, you need to add Reviewsnap from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2e55c-124">To configure the integration of Reviewsnap into Azure AD, you need to add Reviewsnap from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e55c-125">**To add Reviewsnap from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e55c-125">**To add Reviewsnap from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e55c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2e55c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="2e55c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e55c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="2e55c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2e55c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="2e55c-133">In the search box, type **Reviewsnap**, select **Reviewsnap** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2e55c-133">In the search box, type **Reviewsnap**, select **Reviewsnap** from result panel then click **Add** button to add the application.</span></span>

    ![Reviewsnap in the results list](./media/reviewsnap-tutorial/tutorial_reviewsnap_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e55c-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e55c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2e55c-136">In this section, you configure and test Azure AD single sign-on with Reviewsnap based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e55c-136">In this section, you configure and test Azure AD single sign-on with Reviewsnap based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e55c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Reviewsnap is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e55c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Reviewsnap is to a user in Azure AD.</span></span> <span data-ttu-id="2e55c-138">In other words, a link relationship between an Azure AD user and the related user in Reviewsnap needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2e55c-138">In other words, a link relationship between an Azure AD user and the related user in Reviewsnap needs to be established.</span></span>

<span data-ttu-id="2e55c-139">To configure and test Azure AD single sign-on with Reviewsnap, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2e55c-139">To configure and test Azure AD single sign-on with Reviewsnap, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e55c-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2e55c-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2e55c-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e55c-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2e55c-142">**[Create a Reviewsnap test user](#create-a-reviewsnap-test-user)** - to have a counterpart of Britta Simon in Reviewsnap that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2e55c-142">**[Create a Reviewsnap test user](#create-a-reviewsnap-test-user)** - to have a counterpart of Britta Simon in Reviewsnap that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2e55c-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e55c-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2e55c-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2e55c-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e55c-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e55c-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2e55c-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reviewsnap application.</span><span class="sxs-lookup"><span data-stu-id="2e55c-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reviewsnap application.</span></span>

<span data-ttu-id="2e55c-147">**To configure Azure AD single sign-on with Reviewsnap, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e55c-147">**To configure Azure AD single sign-on with Reviewsnap, perform the following steps:**</span></span>

1. <span data-ttu-id="2e55c-148">In the Azure portal, on the **Reviewsnap** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-148">In the Azure portal, on the **Reviewsnap** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="2e55c-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e55c-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/reviewsnap-tutorial/tutorial_reviewsnap_samlbase.png)

1. <span data-ttu-id="2e55c-152">On the **Reviewsnap Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="2e55c-152">On the **Reviewsnap Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Reviewsnap Domain and URLs single sign-on information](./media/reviewsnap-tutorial/tutorial_reviewsnap_url.png)

    <span data-ttu-id="2e55c-154">a.</span><span class="sxs-lookup"><span data-stu-id="2e55c-154">a.</span></span> <span data-ttu-id="2e55c-155">In the **Identifier** textbox, type a URL: `https://app.reviewsnap.com`</span><span class="sxs-lookup"><span data-stu-id="2e55c-155">In the **Identifier** textbox, type a URL: `https://app.reviewsnap.com`</span></span>

    <span data-ttu-id="2e55c-156">b.</span><span class="sxs-lookup"><span data-stu-id="2e55c-156">b.</span></span> <span data-ttu-id="2e55c-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.reviewsnap.com/auth/saml/callback?namespace=<CUSTOMER_NAMESPACE>
`</span><span class="sxs-lookup"><span data-stu-id="2e55c-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.reviewsnap.com/auth/saml/callback?namespace=<CUSTOMER_NAMESPACE>
`</span></span>

1. <span data-ttu-id="2e55c-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="2e55c-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Reviewsnap Domain and URLs single sign-on information](./media/reviewsnap-tutorial/tutorial_reviewsnap_url1.png)

    <span data-ttu-id="2e55c-160">In the **Sign-on URL** textbox, type a URL: `https://app.reviewsnap.com/login`</span><span class="sxs-lookup"><span data-stu-id="2e55c-160">In the **Sign-on URL** textbox, type a URL: `https://app.reviewsnap.com/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2e55c-161">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="2e55c-161">The Reply URL value is not real.</span></span> <span data-ttu-id="2e55c-162">Update the value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="2e55c-162">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="2e55c-163">Contact [Reviewsnap Client support team](mailto:support@reviewsnap.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="2e55c-163">Contact [Reviewsnap Client support team](mailto:support@reviewsnap.com) to get the value.</span></span> 

1. <span data-ttu-id="2e55c-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2e55c-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/reviewsnap-tutorial/tutorial_reviewsnap_certificate.png) 

1. <span data-ttu-id="2e55c-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2e55c-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/reviewsnap-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="2e55c-168">On the **Reviewsnap Configuration** section, click **Configure Reviewsnap** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="2e55c-168">On the **Reviewsnap Configuration** section, click **Configure Reviewsnap** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2e55c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="2e55c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Reviewsnap Configuration](./media/reviewsnap-tutorial/tutorial_reviewsnap_configure.png) 

1. <span data-ttu-id="2e55c-171">To configure single sign-on on **Reviewsnap** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Reviewsnap support team](mailto:support@reviewsnap.com).</span><span class="sxs-lookup"><span data-stu-id="2e55c-171">To configure single sign-on on **Reviewsnap** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Reviewsnap support team](mailto:support@reviewsnap.com).</span></span> <span data-ttu-id="2e55c-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="2e55c-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e55c-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2e55c-173">Create an Azure AD test user</span></span>

<span data-ttu-id="2e55c-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e55c-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="2e55c-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e55c-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e55c-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="2e55c-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/reviewsnap-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="2e55c-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/reviewsnap-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="2e55c-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2e55c-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/reviewsnap-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="2e55c-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e55c-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/reviewsnap-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2e55c-185">a.</span><span class="sxs-lookup"><span data-stu-id="2e55c-185">a.</span></span> <span data-ttu-id="2e55c-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e55c-187">b.</span><span class="sxs-lookup"><span data-stu-id="2e55c-187">b.</span></span> <span data-ttu-id="2e55c-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e55c-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2e55c-189">c.</span><span class="sxs-lookup"><span data-stu-id="2e55c-189">c.</span></span> <span data-ttu-id="2e55c-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="2e55c-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2e55c-191">d.</span><span class="sxs-lookup"><span data-stu-id="2e55c-191">d.</span></span> <span data-ttu-id="2e55c-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-192">Click **Create**.</span></span>
 
### <a name="create-a-reviewsnap-test-user"></a><span data-ttu-id="2e55c-193">Create a Reviewsnap test user</span><span class="sxs-lookup"><span data-stu-id="2e55c-193">Create a Reviewsnap test user</span></span>

<span data-ttu-id="2e55c-194">In this section, you create a user called Britta Simon in Reviewsnap.</span><span class="sxs-lookup"><span data-stu-id="2e55c-194">In this section, you create a user called Britta Simon in Reviewsnap.</span></span> <span data-ttu-id="2e55c-195">Work with [Reviewsnap support team](mailto:support@reviewsnap.com) to add the users in the Reviewsnap platform.</span><span class="sxs-lookup"><span data-stu-id="2e55c-195">Work with [Reviewsnap support team](mailto:support@reviewsnap.com) to add the users in the Reviewsnap platform.</span></span> <span data-ttu-id="2e55c-196">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e55c-196">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2e55c-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2e55c-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="2e55c-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reviewsnap.</span><span class="sxs-lookup"><span data-stu-id="2e55c-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reviewsnap.</span></span>

![Assign the user role][200] 

<span data-ttu-id="2e55c-200">**To assign Britta Simon to Reviewsnap, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e55c-200">**To assign Britta Simon to Reviewsnap, perform the following steps:**</span></span>

1. <span data-ttu-id="2e55c-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2e55c-203">In the applications list, select **Reviewsnap**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-203">In the applications list, select **Reviewsnap**.</span></span>

    ![The Reviewsnap link in the Applications list](./media/reviewsnap-tutorial/tutorial_reviewsnap_app.png)  

1. <span data-ttu-id="2e55c-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2e55c-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="2e55c-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2e55c-207">Click **Add** button.</span></span> <span data-ttu-id="2e55c-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e55c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="2e55c-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2e55c-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2e55c-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e55c-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2e55c-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e55c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2e55c-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e55c-213">Test single sign-on</span></span>

<span data-ttu-id="2e55c-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2e55c-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e55c-215">When you click the Reviewsnap tile in the Access Panel, you should get automatically signed-on to your Reviewsnap application.</span><span class="sxs-lookup"><span data-stu-id="2e55c-215">When you click the Reviewsnap tile in the Access Panel, you should get automatically signed-on to your Reviewsnap application.</span></span>
<span data-ttu-id="2e55c-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e55c-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e55c-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2e55c-217">Additional resources</span></span>

* [<span data-ttu-id="2e55c-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e55c-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2e55c-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e55c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/reviewsnap-tutorial/tutorial_general_01.png
[2]: ./media/reviewsnap-tutorial/tutorial_general_02.png
[3]: ./media/reviewsnap-tutorial/tutorial_general_03.png
[4]: ./media/reviewsnap-tutorial/tutorial_general_04.png

[100]: ./media/reviewsnap-tutorial/tutorial_general_100.png

[200]: ./media/reviewsnap-tutorial/tutorial_general_200.png
[201]: ./media/reviewsnap-tutorial/tutorial_general_201.png
[202]: ./media/reviewsnap-tutorial/tutorial_general_202.png
[203]: ./media/reviewsnap-tutorial/tutorial_general_203.png

