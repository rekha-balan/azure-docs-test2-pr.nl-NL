---
title: 'Tutorial: Azure Active Directory integration with Evernote | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Evernote.
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
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7a9282f5418737b583e29d99893df3fc81f52955
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867525"
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="73a98-103">Tutorial: Azure Active Directory integration with Evernote</span><span class="sxs-lookup"><span data-stu-id="73a98-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="73a98-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73a98-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73a98-105">Integrating Evernote with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="73a98-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73a98-106">You can control in Azure AD who has access to Evernote.</span><span class="sxs-lookup"><span data-stu-id="73a98-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="73a98-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="73a98-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="73a98-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="73a98-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="73a98-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="73a98-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73a98-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="73a98-110">Prerequisites</span></span>

<span data-ttu-id="73a98-111">To configure Azure AD integration with Evernote, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="73a98-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="73a98-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="73a98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73a98-113">An Evernote single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="73a98-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73a98-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="73a98-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73a98-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="73a98-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73a98-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="73a98-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73a98-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73a98-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73a98-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="73a98-118">Scenario description</span></span>
<span data-ttu-id="73a98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="73a98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73a98-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="73a98-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73a98-121">Adding Evernote from the gallery</span><span class="sxs-lookup"><span data-stu-id="73a98-121">Adding Evernote from the gallery</span></span>
1. <span data-ttu-id="73a98-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73a98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="73a98-123">Adding Evernote from the gallery</span><span class="sxs-lookup"><span data-stu-id="73a98-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="73a98-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="73a98-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73a98-125">**To add Evernote from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73a98-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73a98-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="73a98-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="73a98-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="73a98-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73a98-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="73a98-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="73a98-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="73a98-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="73a98-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="73a98-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote in the results list](./media/evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="73a98-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73a98-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="73a98-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="73a98-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73a98-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73a98-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="73a98-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span><span class="sxs-lookup"><span data-stu-id="73a98-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="73a98-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="73a98-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="73a98-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="73a98-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73a98-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="73a98-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="73a98-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73a98-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="73a98-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="73a98-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="73a98-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73a98-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="73a98-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="73a98-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="73a98-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73a98-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="73a98-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span><span class="sxs-lookup"><span data-stu-id="73a98-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="73a98-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73a98-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="73a98-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="73a98-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="73a98-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73a98-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/evernote-tutorial/tutorial_evernote_samlbase.png)

1. <span data-ttu-id="73a98-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="73a98-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Evernote Domain and URLs single sign-on information](./media/evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="73a98-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="73a98-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

1. <span data-ttu-id="73a98-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="73a98-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Evernote Domain and URLs single sign-on information](./media/evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="73a98-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="73a98-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

1. <span data-ttu-id="73a98-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="73a98-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/evernote-tutorial/tutorial_evernote_certificate.png) 

1. <span data-ttu-id="73a98-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="73a98-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/evernote-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="73a98-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="73a98-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="73a98-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="73a98-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evernote Configuration](./media/evernote-tutorial/tutorial_evernote_configure.png) 

1. <span data-ttu-id="73a98-166">In a different web browser window, log into your Evernote company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="73a98-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

1. <span data-ttu-id="73a98-167">Go to **'Admin Console'**</span><span class="sxs-lookup"><span data-stu-id="73a98-167">Go to **'Admin Console'**</span></span>

    ![Admin-Console](./media/evernote-tutorial/tutorial_evernote_adminconsole.png)

1. <span data-ttu-id="73a98-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span><span class="sxs-lookup"><span data-stu-id="73a98-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/evernote-tutorial/tutorial_evernote_sso.png)

1. <span data-ttu-id="73a98-171">Configure the following values:</span><span class="sxs-lookup"><span data-stu-id="73a98-171">Configure the following values:</span></span>

    ![Certificate-Setting](./media/evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="73a98-173">a.</span><span class="sxs-lookup"><span data-stu-id="73a98-173">a.</span></span>  <span data-ttu-id="73a98-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span><span class="sxs-lookup"><span data-stu-id="73a98-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="73a98-175">b.</span><span class="sxs-lookup"><span data-stu-id="73a98-175">b.</span></span> <span data-ttu-id="73a98-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="73a98-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="73a98-177">c.</span><span class="sxs-lookup"><span data-stu-id="73a98-177">c.</span></span> <span data-ttu-id="73a98-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="73a98-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="73a98-179">d.Click **Save Changes**</span><span class="sxs-lookup"><span data-stu-id="73a98-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="73a98-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="73a98-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="73a98-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="73a98-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="73a98-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73a98-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="73a98-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="73a98-183">Create an Azure AD test user</span></span>

<span data-ttu-id="73a98-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73a98-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="73a98-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73a98-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73a98-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="73a98-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/evernote-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="73a98-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="73a98-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/evernote-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="73a98-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="73a98-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/evernote-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="73a98-193">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73a98-193">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="73a98-195">a.</span><span class="sxs-lookup"><span data-stu-id="73a98-195">a.</span></span> <span data-ttu-id="73a98-196">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73a98-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73a98-197">b.</span><span class="sxs-lookup"><span data-stu-id="73a98-197">b.</span></span> <span data-ttu-id="73a98-198">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73a98-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="73a98-199">c.</span><span class="sxs-lookup"><span data-stu-id="73a98-199">c.</span></span> <span data-ttu-id="73a98-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="73a98-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="73a98-201">d.</span><span class="sxs-lookup"><span data-stu-id="73a98-201">d.</span></span> <span data-ttu-id="73a98-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="73a98-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="73a98-203">Create an Evernote test user</span><span class="sxs-lookup"><span data-stu-id="73a98-203">Create an Evernote test user</span></span>

<span data-ttu-id="73a98-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span><span class="sxs-lookup"><span data-stu-id="73a98-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="73a98-205">In the case of Evernote, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="73a98-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="73a98-206">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73a98-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="73a98-207">Log in to your Evernote company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="73a98-207">Log in to your Evernote company site as an administrator.</span></span>

1. <span data-ttu-id="73a98-208">Click the **'Admin Console'**.</span><span class="sxs-lookup"><span data-stu-id="73a98-208">Click the **'Admin Console'**.</span></span>

    ![Admin-Console](./media/evernote-tutorial/tutorial_evernote_adminconsole.png)

1. <span data-ttu-id="73a98-210">From the **'Admin Console'**, go to **‘Add users’**.</span><span class="sxs-lookup"><span data-stu-id="73a98-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Add-testUser](./media/evernote-tutorial/create_aaduser_0001.png)

1. <span data-ttu-id="73a98-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span><span class="sxs-lookup"><span data-stu-id="73a98-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/evernote-tutorial/create_aaduser_0002.png)
    
1. <span data-ttu-id="73a98-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span><span class="sxs-lookup"><span data-stu-id="73a98-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="73a98-215">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="73a98-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="73a98-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span><span class="sxs-lookup"><span data-stu-id="73a98-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Assign the user role][200] 

<span data-ttu-id="73a98-218">**To assign Britta Simon to Evernote, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73a98-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="73a98-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="73a98-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="73a98-221">In the applications list, select **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="73a98-221">In the applications list, select **Evernote**.</span></span>

    ![The Evernote link in the Applications list](./media/evernote-tutorial/tutorial_evernote_app.png)  

1. <span data-ttu-id="73a98-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="73a98-223">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="73a98-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="73a98-225">Click **Add** button.</span></span> <span data-ttu-id="73a98-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="73a98-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="73a98-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="73a98-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="73a98-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="73a98-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="73a98-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="73a98-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="73a98-231">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="73a98-231">Test single sign-on</span></span>

<span data-ttu-id="73a98-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="73a98-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="73a98-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span><span class="sxs-lookup"><span data-stu-id="73a98-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="73a98-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span><span class="sxs-lookup"><span data-stu-id="73a98-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="73a98-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="73a98-235">Additional resources</span></span>

* [<span data-ttu-id="73a98-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73a98-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="73a98-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73a98-237">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/evernote-tutorial/tutorial_general_01.png
[2]: ./media/evernote-tutorial/tutorial_general_02.png
[3]: ./media/evernote-tutorial/tutorial_general_03.png
[4]: ./media/evernote-tutorial/tutorial_general_04.png

[100]: ./media/evernote-tutorial/tutorial_general_100.png

[200]: ./media/evernote-tutorial/tutorial_general_200.png
[201]: ./media/evernote-tutorial/tutorial_general_201.png
[202]: ./media/evernote-tutorial/tutorial_general_202.png
[203]: ./media/evernote-tutorial/tutorial_general_203.png

