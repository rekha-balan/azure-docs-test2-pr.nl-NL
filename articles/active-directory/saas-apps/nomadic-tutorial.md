---
title: 'Tutorial: Azure Active Directory integration with Nomadic | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nomadic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5200eb6e3b1116c12d83d5752b07161385197671
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870427"
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="4dd61-103">Tutorial: Azure Active Directory integration with Nomadic</span><span class="sxs-lookup"><span data-stu-id="4dd61-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="4dd61-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4dd61-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dd61-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4dd61-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4dd61-106">You can control in Azure AD who has access to Nomadic.</span><span class="sxs-lookup"><span data-stu-id="4dd61-106">You can control in Azure AD who has access to Nomadic.</span></span>
- <span data-ttu-id="4dd61-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="4dd61-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4dd61-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4dd61-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4dd61-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4dd61-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dd61-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4dd61-110">Prerequisites</span></span>

<span data-ttu-id="4dd61-111">To configure Azure AD integration with Nomadic, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4dd61-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="4dd61-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4dd61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4dd61-113">A Nomadic single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4dd61-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4dd61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4dd61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4dd61-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4dd61-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4dd61-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4dd61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4dd61-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dd61-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dd61-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4dd61-118">Scenario description</span></span>
<span data-ttu-id="4dd61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4dd61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4dd61-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dd61-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dd61-121">Add Nomadic from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dd61-121">Add Nomadic from the gallery</span></span>
1. <span data-ttu-id="4dd61-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd61-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="4dd61-123">Add Nomadic from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dd61-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="4dd61-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4dd61-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4dd61-125">**To add Nomadic from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd61-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd61-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4dd61-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="4dd61-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4dd61-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="4dd61-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd61-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="4dd61-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4dd61-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span></span>

    ![Nomadic in the results list](./media/nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4dd61-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd61-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4dd61-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4dd61-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4dd61-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dd61-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="4dd61-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4dd61-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="4dd61-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4dd61-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4dd61-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dd61-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4dd61-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4dd61-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4dd61-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd61-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4dd61-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4dd61-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4dd61-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dd61-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4dd61-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4dd61-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4dd61-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd61-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4dd61-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span><span class="sxs-lookup"><span data-stu-id="4dd61-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="4dd61-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd61-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd61-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="4dd61-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dd61-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/nomadic-tutorial/tutorial_nomadic_samlbase.png)

1. <span data-ttu-id="4dd61-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd61-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span></span>

    ![Nomadic Domain and URLs single sign-on information](./media/nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="4dd61-155">a.</span><span class="sxs-lookup"><span data-stu-id="4dd61-155">a.</span></span> <span data-ttu-id="4dd61-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="4dd61-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="4dd61-157">b.</span><span class="sxs-lookup"><span data-stu-id="4dd61-157">b.</span></span> <span data-ttu-id="4dd61-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="4dd61-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dd61-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4dd61-159">These values are not real.</span></span> <span data-ttu-id="4dd61-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="4dd61-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4dd61-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4dd61-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span></span> 
 


1. <span data-ttu-id="4dd61-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4dd61-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/nomadic-tutorial/tutorial_nomadic_certificate.png) 

1. <span data-ttu-id="4dd61-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4dd61-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/nomadic-tutorial/tutorial_general_400.png)

1.  <span data-ttu-id="4dd61-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="4dd61-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4dd61-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4dd61-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4dd61-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4dd61-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4dd61-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4dd61-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dd61-170">Create an Azure AD test user</span></span>

<span data-ttu-id="4dd61-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd61-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="4dd61-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd61-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd61-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="4dd61-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/nomadic-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="4dd61-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/nomadic-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="4dd61-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4dd61-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/nomadic-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="4dd61-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd61-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4dd61-182">a.</span><span class="sxs-lookup"><span data-stu-id="4dd61-182">a.</span></span> <span data-ttu-id="4dd61-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4dd61-184">b.</span><span class="sxs-lookup"><span data-stu-id="4dd61-184">b.</span></span> <span data-ttu-id="4dd61-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd61-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4dd61-186">c.</span><span class="sxs-lookup"><span data-stu-id="4dd61-186">c.</span></span> <span data-ttu-id="4dd61-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="4dd61-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4dd61-188">d.</span><span class="sxs-lookup"><span data-stu-id="4dd61-188">d.</span></span> <span data-ttu-id="4dd61-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="4dd61-190">Create a Nomadic test user</span><span class="sxs-lookup"><span data-stu-id="4dd61-190">Create a Nomadic test user</span></span>

<span data-ttu-id="4dd61-191">In this section, you create a user called Britta Simon in Nomadic.</span><span class="sxs-lookup"><span data-stu-id="4dd61-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="4dd61-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span><span class="sxs-lookup"><span data-stu-id="4dd61-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4dd61-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dd61-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="4dd61-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span><span class="sxs-lookup"><span data-stu-id="4dd61-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span></span>

![Assign the user role][200] 

<span data-ttu-id="4dd61-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd61-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd61-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4dd61-199">In the applications list, select **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-199">In the applications list, select **Nomadic**.</span></span>

    ![The Nomadic link in the Applications list](./media/nomadic-tutorial/tutorial_nomadic_app.png)  

1. <span data-ttu-id="4dd61-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4dd61-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="4dd61-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4dd61-203">Click **Add** button.</span></span> <span data-ttu-id="4dd61-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd61-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="4dd61-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4dd61-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4dd61-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd61-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4dd61-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd61-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4dd61-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd61-209">Test single sign-on</span></span>

<span data-ttu-id="4dd61-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4dd61-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4dd61-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span><span class="sxs-lookup"><span data-stu-id="4dd61-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>
<span data-ttu-id="4dd61-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4dd61-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4dd61-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4dd61-213">Additional resources</span></span>

* [<span data-ttu-id="4dd61-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dd61-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4dd61-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dd61-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/nomadic-tutorial/tutorial_general_01.png
[2]: ./media/nomadic-tutorial/tutorial_general_02.png
[3]: ./media/nomadic-tutorial/tutorial_general_03.png
[4]: ./media/nomadic-tutorial/tutorial_general_04.png

[100]: ./media/nomadic-tutorial/tutorial_general_100.png

[200]: ./media/nomadic-tutorial/tutorial_general_200.png
[201]: ./media/nomadic-tutorial/tutorial_general_201.png
[202]: ./media/nomadic-tutorial/tutorial_general_202.png
[203]: ./media/nomadic-tutorial/tutorial_general_203.png

