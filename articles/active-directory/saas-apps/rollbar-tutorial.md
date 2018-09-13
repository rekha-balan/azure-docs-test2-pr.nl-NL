---
title: 'Tutorial: Azure Active Directory integration with Rollbar | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Rollbar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 57537e54-9388-4272-a610-805ce45a451f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/04/2017
ms.author: jeedes
ms.openlocfilehash: e12e3187893690b75dc69835312ec86a0e601d32
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967822"
---
# <a name="tutorial-azure-active-directory-integration-with-rollbar"></a><span data-ttu-id="dab83-103">Tutorial: Azure Active Directory integration with Rollbar</span><span class="sxs-lookup"><span data-stu-id="dab83-103">Tutorial: Azure Active Directory integration with Rollbar</span></span>

<span data-ttu-id="dab83-104">In this tutorial, you learn how to integrate Rollbar with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dab83-104">In this tutorial, you learn how to integrate Rollbar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dab83-105">Integrating Rollbar with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dab83-105">Integrating Rollbar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dab83-106">You can control in Azure AD who has access to Rollbar.</span><span class="sxs-lookup"><span data-stu-id="dab83-106">You can control in Azure AD who has access to Rollbar.</span></span>
- <span data-ttu-id="dab83-107">You can enable your users to automatically get signed-on to Rollbar (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="dab83-107">You can enable your users to automatically get signed-on to Rollbar (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dab83-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dab83-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="dab83-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dab83-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dab83-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dab83-110">Prerequisites</span></span>

<span data-ttu-id="dab83-111">To configure Azure AD integration with Rollbar, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dab83-111">To configure Azure AD integration with Rollbar, you need the following items:</span></span>

- <span data-ttu-id="dab83-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dab83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dab83-113">A Rollbar single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dab83-113">A Rollbar single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dab83-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dab83-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dab83-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dab83-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dab83-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="dab83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dab83-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dab83-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dab83-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dab83-118">Scenario description</span></span>
<span data-ttu-id="dab83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dab83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dab83-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dab83-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dab83-121">Adding Rollbar from the gallery</span><span class="sxs-lookup"><span data-stu-id="dab83-121">Adding Rollbar from the gallery</span></span>
1. <span data-ttu-id="dab83-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rollbar-from-the-gallery"></a><span data-ttu-id="dab83-123">Adding Rollbar from the gallery</span><span class="sxs-lookup"><span data-stu-id="dab83-123">Adding Rollbar from the gallery</span></span>
<span data-ttu-id="dab83-124">To configure the integration of Rollbar into Azure AD, you need to add Rollbar from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dab83-124">To configure the integration of Rollbar into Azure AD, you need to add Rollbar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dab83-125">**To add Rollbar from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab83-125">**To add Rollbar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dab83-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dab83-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="dab83-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dab83-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dab83-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dab83-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="dab83-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="dab83-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="dab83-133">In the search box, type **Rollbar**, select **Rollbar** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dab83-133">In the search box, type **Rollbar**, select **Rollbar** from result panel then click **Add** button to add the application.</span></span>

    ![Rollbar in the results list](./media/rollbar-tutorial/tutorial_rollbar_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dab83-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab83-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dab83-136">In this section, you configure and test Azure AD single sign-on with Rollbar based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dab83-136">In this section, you configure and test Azure AD single sign-on with Rollbar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dab83-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rollbar is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab83-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rollbar is to a user in Azure AD.</span></span> <span data-ttu-id="dab83-138">In other words, a link relationship between an Azure AD user and the related user in Rollbar needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dab83-138">In other words, a link relationship between an Azure AD user and the related user in Rollbar needs to be established.</span></span>

<span data-ttu-id="dab83-139">In Rollbar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="dab83-139">In Rollbar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dab83-140">To configure and test Azure AD single sign-on with Rollbar, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dab83-140">To configure and test Azure AD single sign-on with Rollbar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dab83-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dab83-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dab83-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab83-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dab83-143">**[Create a Rollbar test user](#create-a-rollbar-test-user)** - to have a counterpart of Britta Simon in Rollbar that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="dab83-143">**[Create a Rollbar test user](#create-a-rollbar-test-user)** - to have a counterpart of Britta Simon in Rollbar that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="dab83-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dab83-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dab83-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dab83-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dab83-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab83-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dab83-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rollbar application.</span><span class="sxs-lookup"><span data-stu-id="dab83-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rollbar application.</span></span>

<span data-ttu-id="dab83-148">**To configure Azure AD single sign-on with Rollbar, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab83-148">**To configure Azure AD single sign-on with Rollbar, perform the following steps:**</span></span>

1. <span data-ttu-id="dab83-149">In the Azure portal, on the **Rollbar** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dab83-149">In the Azure portal, on the **Rollbar** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="dab83-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dab83-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/rollbar-tutorial/tutorial_rollbar_samlbase.png)

1. <span data-ttu-id="dab83-153">On the **Rollbar Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="dab83-153">On the **Rollbar Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Rollbar Domain and URLs single sign-on information](./media/rollbar-tutorial/tutorial_rollbar_url.png)

    <span data-ttu-id="dab83-155">a.</span><span class="sxs-lookup"><span data-stu-id="dab83-155">a.</span></span> <span data-ttu-id="dab83-156">In the **Identifier** textbox, type the URL: `https://saml.rollbar.com`</span><span class="sxs-lookup"><span data-stu-id="dab83-156">In the **Identifier** textbox, type the URL: `https://saml.rollbar.com`</span></span>

    <span data-ttu-id="dab83-157">b.</span><span class="sxs-lookup"><span data-stu-id="dab83-157">b.</span></span> <span data-ttu-id="dab83-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://rollbar.com/<accountname>/saml/sso/azure/`</span><span class="sxs-lookup"><span data-stu-id="dab83-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://rollbar.com/<accountname>/saml/sso/azure/`</span></span>

1. <span data-ttu-id="dab83-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="dab83-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Rollbar Domain and URLs single sign-on information](./media/rollbar-tutorial/tutorial_rollbar_url1.png)

    <span data-ttu-id="dab83-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://rollbar.com/<accountname>/saml/login/azure/`</span><span class="sxs-lookup"><span data-stu-id="dab83-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://rollbar.com/<accountname>/saml/login/azure/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="dab83-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="dab83-162">These values are not real.</span></span> <span data-ttu-id="dab83-163">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="dab83-163">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="dab83-164">Contact [Rollbar Client support team](mailto:support@rollbar.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="dab83-164">Contact [Rollbar Client support team](mailto:support@rollbar.com) to get these values.</span></span> 

1. <span data-ttu-id="dab83-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dab83-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/rollbar-tutorial/tutorial_rollbar_certificate.png) 

1. <span data-ttu-id="dab83-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dab83-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/rollbar-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="dab83-169">In a different web browser window, log in to your Rollbar company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dab83-169">In a different web browser window, log in to your Rollbar company site as an administrator.</span></span>

1. <span data-ttu-id="dab83-170">Click on the **Profile Settings** on the right top corner and then click **Account Name settings**.</span><span class="sxs-lookup"><span data-stu-id="dab83-170">Click on the **Profile Settings** on the right top corner and then click **Account Name settings**.</span></span>
    
    ![Configuration](./media/rollbar-tutorial/general.png)

1. <span data-ttu-id="dab83-172">Click **Identity Provider** under SECURITY.</span><span class="sxs-lookup"><span data-stu-id="dab83-172">Click **Identity Provider** under SECURITY.</span></span>

    ![Configuration](./media/rollbar-tutorial/configure1.png)

1. <span data-ttu-id="dab83-174">In the **SAML Identity Provider** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dab83-174">In the **SAML Identity Provider** section, perform the following steps:</span></span>
    
    ![Configuration](./media/rollbar-tutorial/configure2.png)

    <span data-ttu-id="dab83-176">a.</span><span class="sxs-lookup"><span data-stu-id="dab83-176">a.</span></span> <span data-ttu-id="dab83-177">Select **AZURE** from the **SAML Identity Provider** dropdown.</span><span class="sxs-lookup"><span data-stu-id="dab83-177">Select **AZURE** from the **SAML Identity Provider** dropdown.</span></span>

    <span data-ttu-id="dab83-178">b.</span><span class="sxs-lookup"><span data-stu-id="dab83-178">b.</span></span> <span data-ttu-id="dab83-179">Open your metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **SAML Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="dab83-179">Open your metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **SAML Metadata** textbox.</span></span>

    <span data-ttu-id="dab83-180">c.</span><span class="sxs-lookup"><span data-stu-id="dab83-180">c.</span></span> <span data-ttu-id="dab83-181">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dab83-181">Click **Save**.</span></span>

1. <span data-ttu-id="dab83-182">After clicking the save button, the screen will be like this:</span><span class="sxs-lookup"><span data-stu-id="dab83-182">After clicking the save button, the screen will be like this:</span></span>
    
    ![Configuration](./media/rollbar-tutorial/configure3.png)
    > [!NOTE] 
    > <span data-ttu-id="dab83-184">In order to complete the following step, you must first add yourself as a user to the Rollbar app in Azure.</span><span class="sxs-lookup"><span data-stu-id="dab83-184">In order to complete the following step, you must first add yourself as a user to the Rollbar app in Azure.</span></span>
    <span data-ttu-id="dab83-185">a.</span><span class="sxs-lookup"><span data-stu-id="dab83-185">a.</span></span> <span data-ttu-id="dab83-186">If you want to require all users to authenticate via Azure, then click **log in via your identity provider** to re-authenticate via Azure.</span><span class="sxs-lookup"><span data-stu-id="dab83-186">If you want to require all users to authenticate via Azure, then click **log in via your identity provider** to re-authenticate via Azure.</span></span>  

    <span data-ttu-id="dab83-187">b.</span><span class="sxs-lookup"><span data-stu-id="dab83-187">b.</span></span>  <span data-ttu-id="dab83-188">Once you're returned to the screen, select the **Require login via SAML Identity Provider** checkbox.</span><span class="sxs-lookup"><span data-stu-id="dab83-188">Once you're returned to the screen, select the **Require login via SAML Identity Provider** checkbox.</span></span>

    <span data-ttu-id="dab83-189">b.</span><span class="sxs-lookup"><span data-stu-id="dab83-189">b.</span></span> <span data-ttu-id="dab83-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dab83-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dab83-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="dab83-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dab83-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="dab83-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dab83-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dab83-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dab83-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dab83-194">Create an Azure AD test user</span></span>

<span data-ttu-id="dab83-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab83-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="dab83-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab83-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dab83-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="dab83-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/rollbar-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="dab83-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="dab83-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/rollbar-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="dab83-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dab83-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/rollbar-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="dab83-204">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dab83-204">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/rollbar-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dab83-206">a.</span><span class="sxs-lookup"><span data-stu-id="dab83-206">a.</span></span> <span data-ttu-id="dab83-207">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dab83-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dab83-208">b.</span><span class="sxs-lookup"><span data-stu-id="dab83-208">b.</span></span> <span data-ttu-id="dab83-209">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab83-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dab83-210">c.</span><span class="sxs-lookup"><span data-stu-id="dab83-210">c.</span></span> <span data-ttu-id="dab83-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="dab83-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dab83-212">d.</span><span class="sxs-lookup"><span data-stu-id="dab83-212">d.</span></span> <span data-ttu-id="dab83-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dab83-213">Click **Create**.</span></span>
 
### <a name="create-a-rollbar-test-user"></a><span data-ttu-id="dab83-214">Create a Rollbar test user</span><span class="sxs-lookup"><span data-stu-id="dab83-214">Create a Rollbar test user</span></span>

<span data-ttu-id="dab83-215">To enable Azure AD users to log in to Rollbar, they must be provisioned into Rollbar.</span><span class="sxs-lookup"><span data-stu-id="dab83-215">To enable Azure AD users to log in to Rollbar, they must be provisioned into Rollbar.</span></span> <span data-ttu-id="dab83-216">In the case of Rollbar, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="dab83-216">In the case of Rollbar, provisioning is a manual task.</span></span>

<span data-ttu-id="dab83-217">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab83-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="dab83-218">Log in to your Rollbar company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dab83-218">Log in to your Rollbar company site as an administrator.</span></span>

1. <span data-ttu-id="dab83-219">Click on the **Profile Settings** on the right top corner and then click **Account Name settings**.</span><span class="sxs-lookup"><span data-stu-id="dab83-219">Click on the **Profile Settings** on the right top corner and then click **Account Name settings**.</span></span>

    ![User](./media/rollbar-tutorial/general.png)

1. <span data-ttu-id="dab83-221">Click **Users**.</span><span class="sxs-lookup"><span data-stu-id="dab83-221">Click **Users**.</span></span>
    
    ![Add Employee](./media/rollbar-tutorial/user1.png)

1. <span data-ttu-id="dab83-223">Click **Invite Team Members**.</span><span class="sxs-lookup"><span data-stu-id="dab83-223">Click **Invite Team Members**.</span></span>

    ![Invite People](./media/rollbar-tutorial/user2.png)

1. <span data-ttu-id="dab83-225">In the textbox, enter the name of user like **brittasimon@contoso.com** and the click **Add/Invite**.</span><span class="sxs-lookup"><span data-stu-id="dab83-225">In the textbox, enter the name of user like **brittasimon@contoso.com** and the click **Add/Invite**.</span></span>

    ![Invite People](./media/rollbar-tutorial/user3.png)

1. <span data-ttu-id="dab83-227">User receives an invitation and after accepting it he/she created in the system.</span><span class="sxs-lookup"><span data-stu-id="dab83-227">User receives an invitation and after accepting it he/she created in the system.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dab83-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dab83-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="dab83-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rollbar.</span><span class="sxs-lookup"><span data-stu-id="dab83-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rollbar.</span></span>

![Assign the user role][200] 

<span data-ttu-id="dab83-231">**To assign Britta Simon to Rollbar, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab83-231">**To assign Britta Simon to Rollbar, perform the following steps:**</span></span>

1. <span data-ttu-id="dab83-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dab83-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="dab83-234">In the applications list, select **Rollbar**.</span><span class="sxs-lookup"><span data-stu-id="dab83-234">In the applications list, select **Rollbar**.</span></span>

    ![The Rollbar link in the Applications list](./media/rollbar-tutorial/tutorial_rollbar_app.png)  

1. <span data-ttu-id="dab83-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dab83-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="dab83-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dab83-238">Click **Add** button.</span></span> <span data-ttu-id="dab83-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dab83-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="dab83-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="dab83-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="dab83-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="dab83-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="dab83-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dab83-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dab83-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab83-244">Test single sign-on</span></span>

<span data-ttu-id="dab83-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dab83-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dab83-246">When you click the Rollbar tile in the Access Panel, you should get automatically signed-on to your Rollbar application.</span><span class="sxs-lookup"><span data-stu-id="dab83-246">When you click the Rollbar tile in the Access Panel, you should get automatically signed-on to your Rollbar application.</span></span>
<span data-ttu-id="dab83-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dab83-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dab83-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dab83-248">Additional resources</span></span>

* [<span data-ttu-id="dab83-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dab83-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dab83-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dab83-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/rollbar-tutorial/tutorial_general_01.png
[2]: ./media/rollbar-tutorial/tutorial_general_02.png
[3]: ./media/rollbar-tutorial/tutorial_general_03.png
[4]: ./media/rollbar-tutorial/tutorial_general_04.png

[100]: ./media/rollbar-tutorial/tutorial_general_100.png

[200]: ./media/rollbar-tutorial/tutorial_general_200.png
[201]: ./media/rollbar-tutorial/tutorial_general_201.png
[202]: ./media/rollbar-tutorial/tutorial_general_202.png
[203]: ./media/rollbar-tutorial/tutorial_general_203.png

