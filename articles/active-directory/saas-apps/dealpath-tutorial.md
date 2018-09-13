---
title: 'Tutorial: Azure Active Directory integration with Dealpath | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dealpath.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51ace608-5a4f-48c0-9446-d9f86ad2e890
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/11/2017
ms.author: jeedes
ms.openlocfilehash: 8fa9014ec066e888e9c5cc9330d76c2487786530
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867968"
---
# <a name="tutorial-azure-active-directory-integration-with-dealpath"></a><span data-ttu-id="3194b-103">Tutorial: Azure Active Directory integration with Dealpath</span><span class="sxs-lookup"><span data-stu-id="3194b-103">Tutorial: Azure Active Directory integration with Dealpath</span></span>

<span data-ttu-id="3194b-104">In this tutorial, you learn how to integrate Dealpath with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3194b-104">In this tutorial, you learn how to integrate Dealpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3194b-105">Integrating Dealpath with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3194b-105">Integrating Dealpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3194b-106">You can control in Azure AD who has access to Dealpath.</span><span class="sxs-lookup"><span data-stu-id="3194b-106">You can control in Azure AD who has access to Dealpath.</span></span>
- <span data-ttu-id="3194b-107">You can enable your users to automatically get signed-on to Dealpath (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3194b-107">You can enable your users to automatically get signed-on to Dealpath (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3194b-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3194b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3194b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3194b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3194b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3194b-110">Prerequisites</span></span>

<span data-ttu-id="3194b-111">To configure Azure AD integration with Dealpath, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3194b-111">To configure Azure AD integration with Dealpath, you need the following items:</span></span>

- <span data-ttu-id="3194b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3194b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3194b-113">A Dealpath single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3194b-113">A Dealpath single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3194b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3194b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3194b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3194b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3194b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3194b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3194b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3194b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3194b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3194b-118">Scenario description</span></span>
<span data-ttu-id="3194b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3194b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3194b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3194b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3194b-121">Adding Dealpath from the gallery</span><span class="sxs-lookup"><span data-stu-id="3194b-121">Adding Dealpath from the gallery</span></span>
1. <span data-ttu-id="3194b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3194b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dealpath-from-the-gallery"></a><span data-ttu-id="3194b-123">Adding Dealpath from the gallery</span><span class="sxs-lookup"><span data-stu-id="3194b-123">Adding Dealpath from the gallery</span></span>
<span data-ttu-id="3194b-124">To configure the integration of Dealpath into Azure AD, you need to add Dealpath from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3194b-124">To configure the integration of Dealpath into Azure AD, you need to add Dealpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3194b-125">**To add Dealpath from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3194b-125">**To add Dealpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3194b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3194b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="3194b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3194b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3194b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3194b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="3194b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3194b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="3194b-133">In the search box, type **Dealpath**, select **Dealpath** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3194b-133">In the search box, type **Dealpath**, select **Dealpath** from result panel then click **Add** button to add the application.</span></span>

    ![Dealpath in the results list](./media/dealpath-tutorial/tutorial_dealpath_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3194b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3194b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3194b-136">In this section, you configure and test Azure AD single sign-on with Dealpath based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3194b-136">In this section, you configure and test Azure AD single sign-on with Dealpath based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3194b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dealpath is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3194b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dealpath is to a user in Azure AD.</span></span> <span data-ttu-id="3194b-138">In other words, a link relationship between an Azure AD user and the related user in Dealpath needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3194b-138">In other words, a link relationship between an Azure AD user and the related user in Dealpath needs to be established.</span></span>

<span data-ttu-id="3194b-139">In Dealpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="3194b-139">In Dealpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3194b-140">To configure and test Azure AD single sign-on with Dealpath, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3194b-140">To configure and test Azure AD single sign-on with Dealpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3194b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3194b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3194b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3194b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3194b-143">**[Create a Dealpath test user](#create-a-dealpath-test-user)** - to have a counterpart of Britta Simon in Dealpath that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3194b-143">**[Create a Dealpath test user](#create-a-dealpath-test-user)** - to have a counterpart of Britta Simon in Dealpath that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3194b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3194b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3194b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3194b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3194b-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3194b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3194b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dealpath application.</span><span class="sxs-lookup"><span data-stu-id="3194b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dealpath application.</span></span>

<span data-ttu-id="3194b-148">**To configure Azure AD single sign-on with Dealpath, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3194b-148">**To configure Azure AD single sign-on with Dealpath, perform the following steps:**</span></span>

1. <span data-ttu-id="3194b-149">In the Azure portal, on the **Dealpath** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3194b-149">In the Azure portal, on the **Dealpath** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="3194b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3194b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/dealpath-tutorial/tutorial_dealpath_samlbase.png)

1. <span data-ttu-id="3194b-153">On the **Dealpath Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3194b-153">On the **Dealpath Domain and URLs** section, perform the following steps:</span></span>

    ![Dealpath Domain and URLs single sign-on information](./media/dealpath-tutorial/tutorial_dealpath_url.png)

    <span data-ttu-id="3194b-155">a.</span><span class="sxs-lookup"><span data-stu-id="3194b-155">a.</span></span> <span data-ttu-id="3194b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.dealpath.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="3194b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.dealpath.com/account/login`</span></span>

    <span data-ttu-id="3194b-157">b.</span><span class="sxs-lookup"><span data-stu-id="3194b-157">b.</span></span> <span data-ttu-id="3194b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.dealpath.com/saml/metadata/<ID>`</span><span class="sxs-lookup"><span data-stu-id="3194b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.dealpath.com/saml/metadata/<ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3194b-159">The Identifier is not real.</span><span class="sxs-lookup"><span data-stu-id="3194b-159">The Identifier is not real.</span></span> <span data-ttu-id="3194b-160">Update the value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="3194b-160">Update the value with the actual Identifier.</span></span> <span data-ttu-id="3194b-161">Contact [Dealpath Client support team](mailto:kenter@dealpath.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="3194b-161">Contact [Dealpath Client support team](mailto:kenter@dealpath.com) to get the value.</span></span> 
 
1. <span data-ttu-id="3194b-162">On the **SAML Signing Certificate** section, click **certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3194b-162">On the **SAML Signing Certificate** section, click **certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/dealpath-tutorial/tutorial_dealpath_certificate.png) 

1. <span data-ttu-id="3194b-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3194b-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/dealpath-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="3194b-166">On the **Dealpath Configuration** section, click **Configure Dealpath** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3194b-166">On the **Dealpath Configuration** section, click **Configure Dealpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3194b-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3194b-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Dealpath Configuration](./media/dealpath-tutorial/tutorial_dealpath_configure.png) 

1. <span data-ttu-id="3194b-169">In a different web browser window, login to Dealpath as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="3194b-169">In a different web browser window, login to Dealpath as an Administrator.</span></span>

1. <span data-ttu-id="3194b-170">In the top right, click **Admin Tools** and navigate to **Integrations**, then in **SAML 2.0 Authentication** section click **Update Settings**:</span><span class="sxs-lookup"><span data-stu-id="3194b-170">In the top right, click **Admin Tools** and navigate to **Integrations**, then in **SAML 2.0 Authentication** section click **Update Settings**:</span></span>

    ![Dealpath Configuration](./media/dealpath-tutorial/tutorial_dealpath_admin.png)

1. <span data-ttu-id="3194b-172">In the **Set up SAML 2.0 authentication** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3194b-172">In the **Set up SAML 2.0 authentication** page, perform the following steps:</span></span>

    ![Dealpath Configuration](./media/dealpath-tutorial/tutorial_dealpath_saml.png) 

    <span data-ttu-id="3194b-174">a.</span><span class="sxs-lookup"><span data-stu-id="3194b-174">a.</span></span> <span data-ttu-id="3194b-175">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3194b-175">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3194b-176">b.</span><span class="sxs-lookup"><span data-stu-id="3194b-176">b.</span></span> <span data-ttu-id="3194b-177">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**,  which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3194b-177">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**,  which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3194b-178">c.</span><span class="sxs-lookup"><span data-stu-id="3194b-178">c.</span></span> <span data-ttu-id="3194b-179">Copy the content of the downloaded **certificate(Base64)** file in notepad, and then paste it into the **Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="3194b-179">Copy the content of the downloaded **certificate(Base64)** file in notepad, and then paste it into the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="3194b-180">d.</span><span class="sxs-lookup"><span data-stu-id="3194b-180">d.</span></span> <span data-ttu-id="3194b-181">Click **Update settings**.</span><span class="sxs-lookup"><span data-stu-id="3194b-181">Click **Update settings**.</span></span>


> [!TIP]
> <span data-ttu-id="3194b-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3194b-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3194b-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3194b-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3194b-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3194b-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3194b-185">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3194b-185">Create an Azure AD test user</span></span>

<span data-ttu-id="3194b-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3194b-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3194b-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3194b-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3194b-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3194b-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/dealpath-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="3194b-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3194b-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/dealpath-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="3194b-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3194b-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/dealpath-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="3194b-195">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3194b-195">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/dealpath-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3194b-197">a.</span><span class="sxs-lookup"><span data-stu-id="3194b-197">a.</span></span> <span data-ttu-id="3194b-198">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3194b-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3194b-199">b.</span><span class="sxs-lookup"><span data-stu-id="3194b-199">b.</span></span> <span data-ttu-id="3194b-200">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3194b-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3194b-201">c.</span><span class="sxs-lookup"><span data-stu-id="3194b-201">c.</span></span> <span data-ttu-id="3194b-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3194b-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3194b-203">d.</span><span class="sxs-lookup"><span data-stu-id="3194b-203">d.</span></span> <span data-ttu-id="3194b-204">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3194b-204">Click **Create**.</span></span>
 
### <a name="create-a-dealpath-test-user"></a><span data-ttu-id="3194b-205">Create a Dealpath test user</span><span class="sxs-lookup"><span data-stu-id="3194b-205">Create a Dealpath test user</span></span>

<span data-ttu-id="3194b-206">In this section, you create a user called Britta Simon in Dealpath.</span><span class="sxs-lookup"><span data-stu-id="3194b-206">In this section, you create a user called Britta Simon in Dealpath.</span></span> <span data-ttu-id="3194b-207">Work with [Dealpath Client support team](mailto:kenter@dealpath.com) to add the users in the Dealpath platform.</span><span class="sxs-lookup"><span data-stu-id="3194b-207">Work with [Dealpath Client support team](mailto:kenter@dealpath.com) to add the users in the Dealpath platform.</span></span> <span data-ttu-id="3194b-208">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="3194b-208">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3194b-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3194b-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="3194b-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dealpath.</span><span class="sxs-lookup"><span data-stu-id="3194b-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dealpath.</span></span>

![Assign the user role][200] 

<span data-ttu-id="3194b-212">**To assign Britta Simon to Dealpath, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3194b-212">**To assign Britta Simon to Dealpath, perform the following steps:**</span></span>

1. <span data-ttu-id="3194b-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3194b-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="3194b-215">In the applications list, select **Dealpath**.</span><span class="sxs-lookup"><span data-stu-id="3194b-215">In the applications list, select **Dealpath**.</span></span>

    ![The Dealpath link in the Applications list](./media/dealpath-tutorial/tutorial_dealpath_app.png)  

1. <span data-ttu-id="3194b-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3194b-217">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="3194b-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3194b-219">Click **Add** button.</span></span> <span data-ttu-id="3194b-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3194b-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="3194b-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3194b-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3194b-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3194b-223">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3194b-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3194b-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3194b-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3194b-225">Test single sign-on</span></span>

<span data-ttu-id="3194b-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3194b-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3194b-227">When you click the Dealpath tile in the Access Panel, you should get automatically signed-on to your Dealpath application.</span><span class="sxs-lookup"><span data-stu-id="3194b-227">When you click the Dealpath tile in the Access Panel, you should get automatically signed-on to your Dealpath application.</span></span>
<span data-ttu-id="3194b-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3194b-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3194b-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3194b-229">Additional resources</span></span>

* [<span data-ttu-id="3194b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3194b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3194b-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3194b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/dealpath-tutorial/tutorial_general_01.png
[2]: ./media/dealpath-tutorial/tutorial_general_02.png
[3]: ./media/dealpath-tutorial/tutorial_general_03.png
[4]: ./media/dealpath-tutorial/tutorial_general_04.png

[100]: ./media/dealpath-tutorial/tutorial_general_100.png

[200]: ./media/dealpath-tutorial/tutorial_general_200.png
[201]: ./media/dealpath-tutorial/tutorial_general_201.png
[202]: ./media/dealpath-tutorial/tutorial_general_202.png
[203]: ./media/dealpath-tutorial/tutorial_general_203.png

