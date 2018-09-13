---
title: 'Tutorial: Azure Active Directory integration with Insight4GRC | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Insight4GRC.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: db3b4bd1-b372-4660-88d7-aea0b0ca962e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2018
ms.author: jeedes
ms.openlocfilehash: 256550dc6aaa832599747f6fe39c2ca77ed3f8d7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857732"
---
# <a name="tutorial-azure-active-directory-integration-with-insight4grc"></a><span data-ttu-id="59fde-103">Tutorial: Azure Active Directory integration with Insight4GRC</span><span class="sxs-lookup"><span data-stu-id="59fde-103">Tutorial: Azure Active Directory integration with Insight4GRC</span></span>

<span data-ttu-id="59fde-104">In this tutorial, you learn how to integrate Insight4GRC with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59fde-104">In this tutorial, you learn how to integrate Insight4GRC with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59fde-105">Integrating Insight4GRC with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="59fde-105">Integrating Insight4GRC with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59fde-106">You can control in Azure AD who has access to Insight4GRC.</span><span class="sxs-lookup"><span data-stu-id="59fde-106">You can control in Azure AD who has access to Insight4GRC.</span></span>
- <span data-ttu-id="59fde-107">You can enable your users to automatically get signed-on to Insight4GRC (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="59fde-107">You can enable your users to automatically get signed-on to Insight4GRC (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="59fde-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59fde-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="59fde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="59fde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59fde-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59fde-110">Prerequisites</span></span>

<span data-ttu-id="59fde-111">To configure Azure AD integration with Insight4GRC, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="59fde-111">To configure Azure AD integration with Insight4GRC, you need the following items:</span></span>

- <span data-ttu-id="59fde-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="59fde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59fde-113">An Insight4GRC single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="59fde-113">An Insight4GRC single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59fde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="59fde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59fde-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="59fde-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59fde-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="59fde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59fde-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59fde-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59fde-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="59fde-118">Scenario description</span></span>
<span data-ttu-id="59fde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="59fde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59fde-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="59fde-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59fde-121">Adding Insight4GRC from the gallery</span><span class="sxs-lookup"><span data-stu-id="59fde-121">Adding Insight4GRC from the gallery</span></span>
1. <span data-ttu-id="59fde-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="59fde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insight4grc-from-the-gallery"></a><span data-ttu-id="59fde-123">Adding Insight4GRC from the gallery</span><span class="sxs-lookup"><span data-stu-id="59fde-123">Adding Insight4GRC from the gallery</span></span>
<span data-ttu-id="59fde-124">To configure the integration of Insight4GRC into Azure AD, you need to add Insight4GRC from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="59fde-124">To configure the integration of Insight4GRC into Azure AD, you need to add Insight4GRC from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59fde-125">**To add Insight4GRC from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59fde-125">**To add Insight4GRC from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59fde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="59fde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="59fde-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="59fde-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59fde-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="59fde-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="59fde-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="59fde-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="59fde-133">In the search box, type **Insight4GRC**, select **Insight4GRC** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="59fde-133">In the search box, type **Insight4GRC**, select **Insight4GRC** from result panel then click **Add** button to add the application.</span></span>

    ![Insight4GRC in the results list](./media/insight4grc-tutorial/tutorial_insight_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="59fde-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="59fde-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="59fde-136">In this section, you configure and test Azure AD single sign-on with Insight4GRC based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59fde-136">In this section, you configure and test Azure AD single sign-on with Insight4GRC based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59fde-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Insight4GRC is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59fde-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Insight4GRC is to a user in Azure AD.</span></span> <span data-ttu-id="59fde-138">In other words, a link relationship between an Azure AD user and the related user in Insight4GRC needs to be established.</span><span class="sxs-lookup"><span data-stu-id="59fde-138">In other words, a link relationship between an Azure AD user and the related user in Insight4GRC needs to be established.</span></span>

<span data-ttu-id="59fde-139">To configure and test Azure AD single sign-on with Insight4GRC, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="59fde-139">To configure and test Azure AD single sign-on with Insight4GRC, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59fde-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="59fde-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="59fde-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59fde-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="59fde-142">**[Create an Insight4GRC test user](#create-an-insight4grc-test-user)** - to have a counterpart of Britta Simon in Insight4GRC that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="59fde-142">**[Create an Insight4GRC test user](#create-an-insight4grc-test-user)** - to have a counterpart of Britta Simon in Insight4GRC that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="59fde-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59fde-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="59fde-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="59fde-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="59fde-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="59fde-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="59fde-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insight4GRC application.</span><span class="sxs-lookup"><span data-stu-id="59fde-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insight4GRC application.</span></span>

<span data-ttu-id="59fde-147">**To configure Azure AD single sign-on with Insight4GRC, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59fde-147">**To configure Azure AD single sign-on with Insight4GRC, perform the following steps:**</span></span>

1. <span data-ttu-id="59fde-148">In the Azure portal, on the **Insight4GRC** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="59fde-148">In the Azure portal, on the **Insight4GRC** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="59fde-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59fde-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/insight4grc-tutorial/tutorial_insight_samlbase.png)

1. <span data-ttu-id="59fde-152">On the **Insight4GRC Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="59fde-152">On the **Insight4GRC Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Insight4GRC Domain and URLs single sign-on information](./media/insight4grc-tutorial/tutorial_insight_url.png)

    <span data-ttu-id="59fde-154">a.</span><span class="sxs-lookup"><span data-stu-id="59fde-154">a.</span></span> <span data-ttu-id="59fde-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.Insight4GRC.com/SAML`</span><span class="sxs-lookup"><span data-stu-id="59fde-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.Insight4GRC.com/SAML`</span></span>

    <span data-ttu-id="59fde-156">b.</span><span class="sxs-lookup"><span data-stu-id="59fde-156">b.</span></span> <span data-ttu-id="59fde-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.Insight4GRC.com/Public/SAML/ACS.aspx`</span><span class="sxs-lookup"><span data-stu-id="59fde-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.Insight4GRC.com/Public/SAML/ACS.aspx`</span></span>

1. <span data-ttu-id="59fde-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="59fde-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Insight4GRC Domain and URLs single sign-on information](./media/insight4grc-tutorial/tutorial_insight_url1.png)

    <span data-ttu-id="59fde-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.Insight4GRC.com/Public/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="59fde-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.Insight4GRC.com/Public/Login.aspx`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="59fde-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="59fde-161">These values are not real.</span></span> <span data-ttu-id="59fde-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="59fde-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="59fde-163">Contact [Insight4GRC Client support team](mailto:support.ss@rsmuk.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="59fde-163">Contact [Insight4GRC Client support team](mailto:support.ss@rsmuk.com) to get these values.</span></span> 

1. <span data-ttu-id="59fde-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="59fde-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/insight4grc-tutorial/tutorial_insight_certificate.png) 

1. <span data-ttu-id="59fde-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="59fde-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/insight4grc-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="59fde-168">To configure single sign-on on **Insight4GRC** side, you need to send the copied **App Federation Metadata Url** to [Insight4GRC support team](mailto:support.ss@rsmuk.com).</span><span class="sxs-lookup"><span data-stu-id="59fde-168">To configure single sign-on on **Insight4GRC** side, you need to send the copied **App Federation Metadata Url** to [Insight4GRC support team](mailto:support.ss@rsmuk.com).</span></span> <span data-ttu-id="59fde-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="59fde-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="59fde-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="59fde-170">Create an Azure AD test user</span></span>

<span data-ttu-id="59fde-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59fde-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="59fde-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59fde-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59fde-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="59fde-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/insight4grc-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="59fde-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="59fde-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/insight4grc-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="59fde-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="59fde-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/insight4grc-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="59fde-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59fde-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/insight4grc-tutorial/create_aaduser_04.png)

    <span data-ttu-id="59fde-182">a.</span><span class="sxs-lookup"><span data-stu-id="59fde-182">a.</span></span> <span data-ttu-id="59fde-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59fde-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59fde-184">b.</span><span class="sxs-lookup"><span data-stu-id="59fde-184">b.</span></span> <span data-ttu-id="59fde-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59fde-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="59fde-186">c.</span><span class="sxs-lookup"><span data-stu-id="59fde-186">c.</span></span> <span data-ttu-id="59fde-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="59fde-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="59fde-188">d.</span><span class="sxs-lookup"><span data-stu-id="59fde-188">d.</span></span> <span data-ttu-id="59fde-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="59fde-189">Click **Create**.</span></span>
 
### <a name="create-an-insight4grc-test-user"></a><span data-ttu-id="59fde-190">Create an Insight4GRC test user</span><span class="sxs-lookup"><span data-stu-id="59fde-190">Create an Insight4GRC test user</span></span>

<span data-ttu-id="59fde-191">The objective of this section is to create a user called Britta Simon in Insight4GRC.</span><span class="sxs-lookup"><span data-stu-id="59fde-191">The objective of this section is to create a user called Britta Simon in Insight4GRC.</span></span> <span data-ttu-id="59fde-192">Insight4GRC supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="59fde-192">Insight4GRC supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="59fde-193">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="59fde-193">There is no action item for you in this section.</span></span> <span data-ttu-id="59fde-194">A new user is created during an attempt to access Insight4GRC if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="59fde-194">A new user is created during an attempt to access Insight4GRC if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="59fde-195">If you need to create a user manually, contact [Insight4GRC Client support team](mailto:support.ss@rsmuk.com).</span><span class="sxs-lookup"><span data-stu-id="59fde-195">If you need to create a user manually, contact [Insight4GRC Client support team](mailto:support.ss@rsmuk.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="59fde-196">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="59fde-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="59fde-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insight4GRC.</span><span class="sxs-lookup"><span data-stu-id="59fde-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insight4GRC.</span></span>

![Assign the user role][200] 

<span data-ttu-id="59fde-199">**To assign Britta Simon to Insight4GRC, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59fde-199">**To assign Britta Simon to Insight4GRC, perform the following steps:**</span></span>

1. <span data-ttu-id="59fde-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="59fde-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="59fde-202">In the applications list, select **Insight4GRC**.</span><span class="sxs-lookup"><span data-stu-id="59fde-202">In the applications list, select **Insight4GRC**.</span></span>

    ![The Insight4GRC link in the Applications list](./media/insight4grc-tutorial/tutorial_insight_app.png)  

1. <span data-ttu-id="59fde-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="59fde-204">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="59fde-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="59fde-206">Click **Add** button.</span></span> <span data-ttu-id="59fde-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="59fde-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="59fde-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="59fde-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="59fde-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="59fde-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="59fde-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="59fde-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="59fde-212">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="59fde-212">Test single sign-on</span></span>

<span data-ttu-id="59fde-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="59fde-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="59fde-214">When you click the Insight4GRC tile in the Access Panel, you should get automatically signed-on to your Insight4GRC application.</span><span class="sxs-lookup"><span data-stu-id="59fde-214">When you click the Insight4GRC tile in the Access Panel, you should get automatically signed-on to your Insight4GRC application.</span></span>
<span data-ttu-id="59fde-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59fde-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="59fde-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="59fde-216">Additional resources</span></span>

* [<span data-ttu-id="59fde-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59fde-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="59fde-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59fde-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/insight4grc-tutorial/tutorial_general_01.png
[2]: ./media/insight4grc-tutorial/tutorial_general_02.png
[3]: ./media/insight4grc-tutorial/tutorial_general_03.png
[4]: ./media/insight4grc-tutorial/tutorial_general_04.png

[100]: ./media/insight4grc-tutorial/tutorial_general_100.png

[200]: ./media/insight4grc-tutorial/tutorial_general_200.png
[201]: ./media/insight4grc-tutorial/tutorial_general_201.png
[202]: ./media/insight4grc-tutorial/tutorial_general_202.png
[203]: ./media/insight4grc-tutorial/tutorial_general_203.png

