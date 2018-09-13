---
title: 'Tutorial: Azure Active Directory integration with Nimblex | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nimblex.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d3e165a5-f062-4b50-ac0b-b400838e99cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2018
ms.author: jeedes
ms.openlocfilehash: 7b5dc6d892741f63596589a48ad5d45891b14c21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965969"
---
# <a name="tutorial-azure-active-directory-integration-with-nimblex"></a><span data-ttu-id="75fad-103">Tutorial: Azure Active Directory integration with Nimblex</span><span class="sxs-lookup"><span data-stu-id="75fad-103">Tutorial: Azure Active Directory integration with Nimblex</span></span>

<span data-ttu-id="75fad-104">In this tutorial, you learn how to integrate Nimblex with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75fad-104">In this tutorial, you learn how to integrate Nimblex with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75fad-105">Integrating Nimblex with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="75fad-105">Integrating Nimblex with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75fad-106">You can control in Azure AD who has access to Nimblex.</span><span class="sxs-lookup"><span data-stu-id="75fad-106">You can control in Azure AD who has access to Nimblex.</span></span>
- <span data-ttu-id="75fad-107">You can enable your users to automatically get signed-on to Nimblex (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="75fad-107">You can enable your users to automatically get signed-on to Nimblex (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="75fad-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75fad-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="75fad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="75fad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75fad-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="75fad-110">Prerequisites</span></span>

<span data-ttu-id="75fad-111">To configure Azure AD integration with Nimblex, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="75fad-111">To configure Azure AD integration with Nimblex, you need the following items:</span></span>

- <span data-ttu-id="75fad-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="75fad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75fad-113">A Nimblex single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="75fad-113">A Nimblex single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75fad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="75fad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75fad-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="75fad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75fad-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="75fad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75fad-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75fad-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75fad-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="75fad-118">Scenario description</span></span>
<span data-ttu-id="75fad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="75fad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75fad-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="75fad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75fad-121">Adding Nimblex from the gallery</span><span class="sxs-lookup"><span data-stu-id="75fad-121">Adding Nimblex from the gallery</span></span>
2. <span data-ttu-id="75fad-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="75fad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nimblex-from-the-gallery"></a><span data-ttu-id="75fad-123">Adding Nimblex from the gallery</span><span class="sxs-lookup"><span data-stu-id="75fad-123">Adding Nimblex from the gallery</span></span>
<span data-ttu-id="75fad-124">To configure the integration of Nimblex into Azure AD, you need to add Nimblex from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="75fad-124">To configure the integration of Nimblex into Azure AD, you need to add Nimblex from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75fad-125">**To add Nimblex from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="75fad-125">**To add Nimblex from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75fad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="75fad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="75fad-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="75fad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="75fad-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="75fad-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="75fad-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="75fad-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="75fad-133">In the search box, type **Nimblex**, select **Nimblex** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="75fad-133">In the search box, type **Nimblex**, select **Nimblex** from result panel then click **Add** button to add the application.</span></span>

    ![Nimblex in the results list](./media/nimblex-tutorial/tutorial_nimblex_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="75fad-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="75fad-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="75fad-136">In this section, you configure and test Azure AD single sign-on with Nimblex based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="75fad-136">In this section, you configure and test Azure AD single sign-on with Nimblex based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75fad-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nimblex is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75fad-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nimblex is to a user in Azure AD.</span></span> <span data-ttu-id="75fad-138">In other words, a link relationship between an Azure AD user and the related user in Nimblex needs to be established.</span><span class="sxs-lookup"><span data-stu-id="75fad-138">In other words, a link relationship between an Azure AD user and the related user in Nimblex needs to be established.</span></span>

<span data-ttu-id="75fad-139">To configure and test Azure AD single sign-on with Nimblex, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="75fad-139">To configure and test Azure AD single sign-on with Nimblex, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75fad-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="75fad-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75fad-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75fad-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75fad-142">**[Create a Nimblex test user](#create-a-nimblex-test-user)** - to have a counterpart of Britta Simon in Nimblex that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="75fad-142">**[Create a Nimblex test user](#create-a-nimblex-test-user)** - to have a counterpart of Britta Simon in Nimblex that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="75fad-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75fad-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75fad-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="75fad-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="75fad-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="75fad-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="75fad-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nimblex application.</span><span class="sxs-lookup"><span data-stu-id="75fad-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nimblex application.</span></span>

<span data-ttu-id="75fad-147">**To configure Azure AD single sign-on with Nimblex, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="75fad-147">**To configure Azure AD single sign-on with Nimblex, perform the following steps:**</span></span>

1. <span data-ttu-id="75fad-148">In the Azure portal, on the **Nimblex** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="75fad-148">In the Azure portal, on the **Nimblex** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="75fad-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75fad-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/nimblex-tutorial/tutorial_nimblex_samlbase.png)

3. <span data-ttu-id="75fad-152">On the **Nimblex Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="75fad-152">On the **Nimblex Domain and URLs** section, perform the following steps:</span></span>

    ![Nimblex Domain and URLs single sign-on information](./media/nimblex-tutorial/tutorial_nimblex_url.png)

    <span data-ttu-id="75fad-154">a.</span><span class="sxs-lookup"><span data-stu-id="75fad-154">a.</span></span> <span data-ttu-id="75fad-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR APPLICATION PATH>/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="75fad-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR APPLICATION PATH>/Login.aspx`</span></span>

    <span data-ttu-id="75fad-156">b.</span><span class="sxs-lookup"><span data-stu-id="75fad-156">b.</span></span> <span data-ttu-id="75fad-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR APPLICATION PATH>/`</span><span class="sxs-lookup"><span data-stu-id="75fad-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR APPLICATION PATH>/`</span></span>

    <span data-ttu-id="75fad-158">c.</span><span class="sxs-lookup"><span data-stu-id="75fad-158">c.</span></span> <span data-ttu-id="75fad-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<path-to-application>/SamlReply.aspx`</span><span class="sxs-lookup"><span data-stu-id="75fad-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<path-to-application>/SamlReply.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75fad-160">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="75fad-160">These values are not real.</span></span> <span data-ttu-id="75fad-161">Update these values with the actual Sign-On URL,Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="75fad-161">Update these values with the actual Sign-On URL,Identifier and Reply URL.</span></span> <span data-ttu-id="75fad-162">Contact [Nimblex Client support team](mailto:support@ebms.com.au) to get these values.</span><span class="sxs-lookup"><span data-stu-id="75fad-162">Contact [Nimblex Client support team](mailto:support@ebms.com.au) to get these values.</span></span>

4. <span data-ttu-id="75fad-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="75fad-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/nimblex-tutorial/tutorial_nimblex_certificate.png) 

5. <span data-ttu-id="75fad-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="75fad-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/nimblex-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75fad-167">On the **Nimblex Configuration** section, click **Configure Nimblex** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="75fad-167">On the **Nimblex Configuration** section, click **Configure Nimblex** to open **Configure sign-on** window.</span></span> <span data-ttu-id="75fad-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="75fad-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Nimblex Configuration](./media/nimblex-tutorial/tutorial_nimblex_configure.png) 

7. <span data-ttu-id="75fad-170">In a different web browser window, log in to Nimblex as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="75fad-170">In a different web browser window, log in to Nimblex as a Security Administrator.</span></span>

9. <span data-ttu-id="75fad-171">On the top right side of the page, click **Settings** logo.</span><span class="sxs-lookup"><span data-stu-id="75fad-171">On the top right side of the page, click **Settings** logo.</span></span>

    ![Nimblex settings](./media/nimblex-tutorial/tutorial_nimblex_settings.png)

10. <span data-ttu-id="75fad-173">On the **Control Panel** page, under **Security** section click **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="75fad-173">On the **Control Panel** page, under **Security** section click **Single Sign-on**.</span></span>

    ![Nimblex settings](./media/nimblex-tutorial/tutorial_nimblex_single.png)

11. <span data-ttu-id="75fad-175">On the **Manage Single Sign-On** page, select your instance name and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="75fad-175">On the **Manage Single Sign-On** page, select your instance name and click **Edit**.</span></span>

    ![Nimblex saml](./media/nimblex-tutorial/tutorial_nimblex_saml.png)

12. <span data-ttu-id="75fad-177">On the **Edit SSO Provider** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="75fad-177">On the **Edit SSO Provider** page, perform the following steps:</span></span>

    ![Nimblex saml](./media/nimblex-tutorial/tutorial_nimblex_sso.png)

    <span data-ttu-id="75fad-179">a.</span><span class="sxs-lookup"><span data-stu-id="75fad-179">a.</span></span> <span data-ttu-id="75fad-180">In the **Description** textbox, type your instance name.</span><span class="sxs-lookup"><span data-stu-id="75fad-180">In the **Description** textbox, type your instance name.</span></span>

    <span data-ttu-id="75fad-181">b.</span><span class="sxs-lookup"><span data-stu-id="75fad-181">b.</span></span> <span data-ttu-id="75fad-182">In Notepad, open the base-64 encoded certificate that you downloaded from the Azure portal, copy its content, and then paste it into the **Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="75fad-182">In Notepad, open the base-64 encoded certificate that you downloaded from the Azure portal, copy its content, and then paste it into the **Certificate** box.</span></span>

    <span data-ttu-id="75fad-183">c.</span><span class="sxs-lookup"><span data-stu-id="75fad-183">c.</span></span> <span data-ttu-id="75fad-184">In the **Identity Provider Sso Target Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75fad-184">In the **Identity Provider Sso Target Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="75fad-185">d.</span><span class="sxs-lookup"><span data-stu-id="75fad-185">d.</span></span> <span data-ttu-id="75fad-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="75fad-186">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75fad-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="75fad-187">Create an Azure AD test user</span></span>

<span data-ttu-id="75fad-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75fad-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="75fad-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="75fad-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75fad-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="75fad-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/nimblex-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="75fad-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="75fad-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/nimblex-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="75fad-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="75fad-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/nimblex-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="75fad-197">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="75fad-197">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/nimblex-tutorial/create_aaduser_04.png)

    <span data-ttu-id="75fad-199">a.</span><span class="sxs-lookup"><span data-stu-id="75fad-199">a.</span></span> <span data-ttu-id="75fad-200">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75fad-200">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75fad-201">b.</span><span class="sxs-lookup"><span data-stu-id="75fad-201">b.</span></span> <span data-ttu-id="75fad-202">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75fad-202">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="75fad-203">c.</span><span class="sxs-lookup"><span data-stu-id="75fad-203">c.</span></span> <span data-ttu-id="75fad-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="75fad-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="75fad-205">d.</span><span class="sxs-lookup"><span data-stu-id="75fad-205">d.</span></span> <span data-ttu-id="75fad-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="75fad-206">Click **Create**.</span></span>
 
### <a name="create-a-nimblex-test-user"></a><span data-ttu-id="75fad-207">Create a Nimblex test user</span><span class="sxs-lookup"><span data-stu-id="75fad-207">Create a Nimblex test user</span></span>

<span data-ttu-id="75fad-208">The objective of this section is to create a user called Britta Simon in Nimblex.</span><span class="sxs-lookup"><span data-stu-id="75fad-208">The objective of this section is to create a user called Britta Simon in Nimblex.</span></span> <span data-ttu-id="75fad-209">Nimblex supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="75fad-209">Nimblex supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="75fad-210">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="75fad-210">There is no action item for you in this section.</span></span> <span data-ttu-id="75fad-211">A new user is created during an attempt to access Nimblex if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="75fad-211">A new user is created during an attempt to access Nimblex if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="75fad-212">If you need to create a user manually, contact [Nimblex Client support team](mailto:support@ebms.com.au).</span><span class="sxs-lookup"><span data-stu-id="75fad-212">If you need to create a user manually, contact [Nimblex Client support team](mailto:support@ebms.com.au).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="75fad-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="75fad-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="75fad-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nimblex.</span><span class="sxs-lookup"><span data-stu-id="75fad-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nimblex.</span></span>

![Assign the user role][200] 

<span data-ttu-id="75fad-216">**To assign Britta Simon to Nimblex, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="75fad-216">**To assign Britta Simon to Nimblex, perform the following steps:**</span></span>

1. <span data-ttu-id="75fad-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="75fad-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="75fad-219">In the applications list, select **Nimblex**.</span><span class="sxs-lookup"><span data-stu-id="75fad-219">In the applications list, select **Nimblex**.</span></span>

    ![The Nimblex link in the Applications list](./media/nimblex-tutorial/tutorial_nimblex_app.png)  

3. <span data-ttu-id="75fad-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="75fad-221">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="75fad-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="75fad-223">Click **Add** button.</span></span> <span data-ttu-id="75fad-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="75fad-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="75fad-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="75fad-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="75fad-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="75fad-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75fad-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="75fad-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="75fad-229">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="75fad-229">Test single sign-on</span></span>

<span data-ttu-id="75fad-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="75fad-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="75fad-231">When you click the Nimblex tile in the Access Panel, you should get automatically signed-on to your Nimblex application.</span><span class="sxs-lookup"><span data-stu-id="75fad-231">When you click the Nimblex tile in the Access Panel, you should get automatically signed-on to your Nimblex application.</span></span>
<span data-ttu-id="75fad-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="75fad-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="75fad-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="75fad-233">Additional resources</span></span>

* [<span data-ttu-id="75fad-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75fad-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="75fad-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75fad-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/nimblex-tutorial/tutorial_general_01.png
[2]: ./media/nimblex-tutorial/tutorial_general_02.png
[3]: ./media/nimblex-tutorial/tutorial_general_03.png
[4]: ./media/nimblex-tutorial/tutorial_general_04.png

[100]: ./media/nimblex-tutorial/tutorial_general_100.png

[200]: ./media/nimblex-tutorial/tutorial_general_200.png
[201]: ./media/nimblex-tutorial/tutorial_general_201.png
[202]: ./media/nimblex-tutorial/tutorial_general_202.png
[203]: ./media/nimblex-tutorial/tutorial_general_203.png

