---
title: 'Tutorial: Azure Active Directory integration with Sequr | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sequr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a491e2ce-b4e8-41b8-8f4a-a2e263e462c3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/8/2017
ms.author: jeedes
ms.openlocfilehash: 183d5f9d1e8da4e0ed9e4648ea48ba5e23e2e70e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865331"
---
# <a name="tutorial-azure-active-directory-integration-with-sequr"></a><span data-ttu-id="c1094-103">Tutorial: Azure Active Directory integration with Sequr</span><span class="sxs-lookup"><span data-stu-id="c1094-103">Tutorial: Azure Active Directory integration with Sequr</span></span>

<span data-ttu-id="c1094-104">In this tutorial, you learn how to integrate Sequr with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1094-104">In this tutorial, you learn how to integrate Sequr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1094-105">Integrating Sequr with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c1094-105">Integrating Sequr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1094-106">You can control in Azure AD who has access to Sequr.</span><span class="sxs-lookup"><span data-stu-id="c1094-106">You can control in Azure AD who has access to Sequr.</span></span>
- <span data-ttu-id="c1094-107">You can enable your users to automatically get signed-on to Sequr (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c1094-107">You can enable your users to automatically get signed-on to Sequr (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c1094-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c1094-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c1094-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c1094-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1094-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c1094-110">Prerequisites</span></span>

<span data-ttu-id="c1094-111">To configure Azure AD integration with Sequr, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c1094-111">To configure Azure AD integration with Sequr, you need the following items:</span></span>

- <span data-ttu-id="c1094-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c1094-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1094-113">A Sequr single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c1094-113">A Sequr single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1094-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c1094-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1094-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c1094-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1094-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c1094-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1094-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1094-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1094-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c1094-118">Scenario description</span></span>
<span data-ttu-id="c1094-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c1094-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1094-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c1094-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1094-121">Adding Sequr from the gallery</span><span class="sxs-lookup"><span data-stu-id="c1094-121">Adding Sequr from the gallery</span></span>
1. <span data-ttu-id="c1094-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c1094-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sequr-from-the-gallery"></a><span data-ttu-id="c1094-123">Adding Sequr from the gallery</span><span class="sxs-lookup"><span data-stu-id="c1094-123">Adding Sequr from the gallery</span></span>
<span data-ttu-id="c1094-124">To configure the integration of Sequr into Azure AD, you need to add Sequr from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c1094-124">To configure the integration of Sequr into Azure AD, you need to add Sequr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1094-125">**To add Sequr from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1094-125">**To add Sequr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1094-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c1094-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c1094-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c1094-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1094-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c1094-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c1094-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c1094-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c1094-133">In the search box, type **Sequr**, select **Sequr** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c1094-133">In the search box, type **Sequr**, select **Sequr** from result panel then click **Add** button to add the application.</span></span>

    ![Sequr in the results list](./media/sequr-tutorial/tutorial_sequr_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c1094-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c1094-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c1094-136">In this section, you configure and test Azure AD single sign-on with Sequr based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1094-136">In this section, you configure and test Azure AD single sign-on with Sequr based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1094-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Sequr is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1094-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Sequr is to a user in Azure AD.</span></span> <span data-ttu-id="c1094-138">In other words, a link relationship between an Azure AD user and the related user in Sequr needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c1094-138">In other words, a link relationship between an Azure AD user and the related user in Sequr needs to be established.</span></span>

<span data-ttu-id="c1094-139">In Sequr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c1094-139">In Sequr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1094-140">To configure and test Azure AD single sign-on with Sequr, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c1094-140">To configure and test Azure AD single sign-on with Sequr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1094-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c1094-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c1094-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1094-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c1094-143">**[Create a Sequr test user](#create-a-sequr-test-user)** - to have a counterpart of Britta Simon in Sequr that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c1094-143">**[Create a Sequr test user](#create-a-sequr-test-user)** - to have a counterpart of Britta Simon in Sequr that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c1094-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c1094-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c1094-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c1094-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c1094-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c1094-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c1094-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sequr application.</span><span class="sxs-lookup"><span data-stu-id="c1094-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sequr application.</span></span>

<span data-ttu-id="c1094-148">**To configure Azure AD single sign-on with Sequr, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1094-148">**To configure Azure AD single sign-on with Sequr, perform the following steps:**</span></span>

1. <span data-ttu-id="c1094-149">In the Azure portal, on the **Sequr** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c1094-149">In the Azure portal, on the **Sequr** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="c1094-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c1094-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sequr-tutorial/tutorial_sequr_samlbase.png)

1. <span data-ttu-id="c1094-153">On the **Sequr Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="c1094-153">On the **Sequr Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Sequr Domain and URLs single sign-on information](./media/sequr-tutorial/tutorial_sequr_url.png)

    <span data-ttu-id="c1094-155">In the **Identifier** textbox, type the URL: `https://login.sequr.io`</span><span class="sxs-lookup"><span data-stu-id="c1094-155">In the **Identifier** textbox, type the URL: `https://login.sequr.io`</span></span>

1. <span data-ttu-id="c1094-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="c1094-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Sequr Domain and URLs single sign-on information](./media/sequr-tutorial/tutorial_sequr_url1.png)

    <span data-ttu-id="c1094-158">a.</span><span class="sxs-lookup"><span data-stu-id="c1094-158">a.</span></span> <span data-ttu-id="c1094-159">In the **Sign-on URL** textbox, type the URL: `https://login.sequr.io`</span><span class="sxs-lookup"><span data-stu-id="c1094-159">In the **Sign-on URL** textbox, type the URL: `https://login.sequr.io`</span></span>

    <span data-ttu-id="c1094-160">b.</span><span class="sxs-lookup"><span data-stu-id="c1094-160">b.</span></span> <span data-ttu-id="c1094-161">In the **Relay State** textbox, you will get this value, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c1094-161">In the **Relay State** textbox, you will get this value, which is explained later in the tutorial.</span></span>
     
1. <span data-ttu-id="c1094-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c1094-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/sequr-tutorial/tutorial_sequr_certificate.png) 

1. <span data-ttu-id="c1094-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c1094-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sequr-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="c1094-166">On the **Sequr Configuration** section, click **Configure Sequr** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c1094-166">On the **Sequr Configuration** section, click **Configure Sequr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c1094-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c1094-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sequr Configuration](./media/sequr-tutorial/tutorial_sequr_configure.png)

1. <span data-ttu-id="c1094-169">In a different web browser window, log in to your Sequr company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c1094-169">In a different web browser window, log in to your Sequr company site as an administrator.</span></span>

1. <span data-ttu-id="c1094-170">Click on the **Integrations** from the left navigation panel.</span><span class="sxs-lookup"><span data-stu-id="c1094-170">Click on the **Integrations** from the left navigation panel.</span></span>

    ![Sequr Configuration](./media/sequr-tutorial/configure1.png)

1. <span data-ttu-id="c1094-172">Scroll down to the **Single Sign-On** section and click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="c1094-172">Scroll down to the **Single Sign-On** section and click **Manage**.</span></span>

    ![Sequr Configuration](./media/sequr-tutorial/configure2.png)

1. <span data-ttu-id="c1094-174">In the **Manage Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c1094-174">In the **Manage Single Sign-On** section, perform the following steps:</span></span>

    ![Sequr Configuration](./media/sequr-tutorial/configure3.png)

    <span data-ttu-id="c1094-176">a.</span><span class="sxs-lookup"><span data-stu-id="c1094-176">a.</span></span> <span data-ttu-id="c1094-177">In the **Identity Provider Single Sign-On URL** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c1094-177">In the **Identity Provider Single Sign-On URL** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="c1094-178">b.</span><span class="sxs-lookup"><span data-stu-id="c1094-178">b.</span></span> <span data-ttu-id="c1094-179">Drag and drop the **Certificate** file, which you have downloaded from the Azure portal or manually enter the content of the certificate.</span><span class="sxs-lookup"><span data-stu-id="c1094-179">Drag and drop the **Certificate** file, which you have downloaded from the Azure portal or manually enter the content of the certificate.</span></span>

    <span data-ttu-id="c1094-180">c.</span><span class="sxs-lookup"><span data-stu-id="c1094-180">c.</span></span> <span data-ttu-id="c1094-181">After saving the configuration, the relay state value will be generated.</span><span class="sxs-lookup"><span data-stu-id="c1094-181">After saving the configuration, the relay state value will be generated.</span></span> <span data-ttu-id="c1094-182">Copy the **relay state** value and paste it in the **Relay State** textbox of **Sequr Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c1094-182">Copy the **relay state** value and paste it in the **Relay State** textbox of **Sequr Domain and URLs** section in the Azure portal.</span></span>

    <span data-ttu-id="c1094-183">d.</span><span class="sxs-lookup"><span data-stu-id="c1094-183">d.</span></span> <span data-ttu-id="c1094-184">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c1094-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c1094-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c1094-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1094-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c1094-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1094-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1094-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c1094-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c1094-188">Create an Azure AD test user</span></span>

<span data-ttu-id="c1094-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1094-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c1094-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1094-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1094-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c1094-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sequr-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c1094-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c1094-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sequr-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c1094-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c1094-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sequr-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c1094-198">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c1094-198">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sequr-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c1094-200">a.</span><span class="sxs-lookup"><span data-stu-id="c1094-200">a.</span></span> <span data-ttu-id="c1094-201">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1094-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1094-202">b.</span><span class="sxs-lookup"><span data-stu-id="c1094-202">b.</span></span> <span data-ttu-id="c1094-203">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1094-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c1094-204">c.</span><span class="sxs-lookup"><span data-stu-id="c1094-204">c.</span></span> <span data-ttu-id="c1094-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c1094-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c1094-206">d.</span><span class="sxs-lookup"><span data-stu-id="c1094-206">d.</span></span> <span data-ttu-id="c1094-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1094-207">Click **Create**.</span></span>
 
### <a name="create-a-sequr-test-user"></a><span data-ttu-id="c1094-208">Create a Sequr test user</span><span class="sxs-lookup"><span data-stu-id="c1094-208">Create a Sequr test user</span></span>

<span data-ttu-id="c1094-209">In this section, you create a user called Britta Simon in Sequr.</span><span class="sxs-lookup"><span data-stu-id="c1094-209">In this section, you create a user called Britta Simon in Sequr.</span></span> <span data-ttu-id="c1094-210">Work with [Sequr Client support team](mailto:support@sequr.io) to add the users in the Sequr platform.</span><span class="sxs-lookup"><span data-stu-id="c1094-210">Work with [Sequr Client support team](mailto:support@sequr.io) to add the users in the Sequr platform.</span></span> <span data-ttu-id="c1094-211">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c1094-211">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c1094-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c1094-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="c1094-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sequr.</span><span class="sxs-lookup"><span data-stu-id="c1094-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sequr.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c1094-215">**To assign Britta Simon to Sequr, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1094-215">**To assign Britta Simon to Sequr, perform the following steps:**</span></span>

1. <span data-ttu-id="c1094-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c1094-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c1094-218">In the applications list, select **Sequr**.</span><span class="sxs-lookup"><span data-stu-id="c1094-218">In the applications list, select **Sequr**.</span></span>

    ![The Sequr link in the Applications list](./media/sequr-tutorial/tutorial_sequr_app.png)  

1. <span data-ttu-id="c1094-220">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c1094-220">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c1094-222">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c1094-222">Click **Add** button.</span></span> <span data-ttu-id="c1094-223">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c1094-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c1094-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c1094-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c1094-226">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c1094-226">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c1094-227">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c1094-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c1094-228">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c1094-228">Test single sign-on</span></span>

<span data-ttu-id="c1094-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c1094-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c1094-230">When you click the Sequr tile in the Access Panel, you should get automatically signed-on to your Sequr application.</span><span class="sxs-lookup"><span data-stu-id="c1094-230">When you click the Sequr tile in the Access Panel, you should get automatically signed-on to your Sequr application.</span></span>
<span data-ttu-id="c1094-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1094-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c1094-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c1094-232">Additional resources</span></span>

* [<span data-ttu-id="c1094-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1094-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c1094-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1094-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sequr-tutorial/tutorial_general_01.png
[2]: ./media/sequr-tutorial/tutorial_general_02.png
[3]: ./media/sequr-tutorial/tutorial_general_03.png
[4]: ./media/sequr-tutorial/tutorial_general_04.png

[100]: ./media/sequr-tutorial/tutorial_general_100.png

[200]: ./media/sequr-tutorial/tutorial_general_200.png
[201]: ./media/sequr-tutorial/tutorial_general_201.png
[202]: ./media/sequr-tutorial/tutorial_general_202.png
[203]: ./media/sequr-tutorial/tutorial_general_203.png

