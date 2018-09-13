---
title: 'Tutorial: Azure Active Directory integration with Hornbill | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Hornbill.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 173061e4-ac1d-458f-bb9b-e9a2493aab0e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2018
ms.author: jeedes
ms.openlocfilehash: 30fdb55758d5fbac41452236ebaa9f96ab9bba6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866157"
---
# <a name="tutorial-azure-active-directory-integration-with-hornbill"></a><span data-ttu-id="fc5bc-103">Tutorial: Azure Active Directory integration with Hornbill</span><span class="sxs-lookup"><span data-stu-id="fc5bc-103">Tutorial: Azure Active Directory integration with Hornbill</span></span>

<span data-ttu-id="fc5bc-104">In this tutorial, you learn how to integrate Hornbill with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc5bc-104">In this tutorial, you learn how to integrate Hornbill with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc5bc-105">Integrating Hornbill with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-105">Integrating Hornbill with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fc5bc-106">You can control in Azure AD who has access to Hornbill.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-106">You can control in Azure AD who has access to Hornbill.</span></span>
- <span data-ttu-id="fc5bc-107">You can enable your users to automatically get signed-on to Hornbill (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-107">You can enable your users to automatically get signed-on to Hornbill (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fc5bc-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fc5bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fc5bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc5bc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fc5bc-110">Prerequisites</span></span>

<span data-ttu-id="fc5bc-111">To configure Azure AD integration with Hornbill, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-111">To configure Azure AD integration with Hornbill, you need the following items:</span></span>

- <span data-ttu-id="fc5bc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fc5bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc5bc-113">A Hornbill single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fc5bc-113">A Hornbill single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc5bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc5bc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc5bc-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc5bc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc5bc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc5bc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fc5bc-118">Scenario description</span></span>
<span data-ttu-id="fc5bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc5bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc5bc-121">Adding Hornbill from the gallery</span><span class="sxs-lookup"><span data-stu-id="fc5bc-121">Adding Hornbill from the gallery</span></span>
2. <span data-ttu-id="fc5bc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fc5bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hornbill-from-the-gallery"></a><span data-ttu-id="fc5bc-123">Adding Hornbill from the gallery</span><span class="sxs-lookup"><span data-stu-id="fc5bc-123">Adding Hornbill from the gallery</span></span>
<span data-ttu-id="fc5bc-124">To configure the integration of Hornbill into Azure AD, you need to add Hornbill from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-124">To configure the integration of Hornbill into Azure AD, you need to add Hornbill from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fc5bc-125">**To add Hornbill from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fc5bc-125">**To add Hornbill from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fc5bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="fc5bc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fc5bc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="fc5bc-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="fc5bc-133">In the search box, type **Hornbill**, select **Hornbill** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-133">In the search box, type **Hornbill**, select **Hornbill** from result panel then click **Add** button to add the application.</span></span>

    ![Hornbill in the results list](./media/hornbill-tutorial/tutorial_hornbill_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fc5bc-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fc5bc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fc5bc-136">In this section, you configure and test Azure AD single sign-on with Hornbill based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fc5bc-136">In this section, you configure and test Azure AD single sign-on with Hornbill based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fc5bc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Hornbill is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Hornbill is to a user in Azure AD.</span></span> <span data-ttu-id="fc5bc-138">In other words, a link relationship between an Azure AD user and the related user in Hornbill needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-138">In other words, a link relationship between an Azure AD user and the related user in Hornbill needs to be established.</span></span>

<span data-ttu-id="fc5bc-139">To configure and test Azure AD single sign-on with Hornbill, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-139">To configure and test Azure AD single sign-on with Hornbill, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fc5bc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fc5bc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc5bc-142">**[Create a Hornbill test user](#create-a-hornbill-test-user)** - to have a counterpart of Britta Simon in Hornbill that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-142">**[Create a Hornbill test user](#create-a-hornbill-test-user)** - to have a counterpart of Britta Simon in Hornbill that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc5bc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc5bc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fc5bc-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fc5bc-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fc5bc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hornbill application.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hornbill application.</span></span>

<span data-ttu-id="fc5bc-147">**To configure Azure AD single sign-on with Hornbill, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fc5bc-147">**To configure Azure AD single sign-on with Hornbill, perform the following steps:**</span></span>

1. <span data-ttu-id="fc5bc-148">In the Azure portal, on the **Hornbill** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-148">In the Azure portal, on the **Hornbill** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="fc5bc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/hornbill-tutorial/tutorial_hornbill_samlbase.png)

3. <span data-ttu-id="fc5bc-152">On the **Hornbill Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-152">On the **Hornbill Domain and URLs** section, perform the following steps:</span></span>

    ![Hornbill Domain and URLs single sign-on information](./media/hornbill-tutorial/tutorial_hornbill_url.png)

    <span data-ttu-id="fc5bc-154">a.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-154">a.</span></span> <span data-ttu-id="fc5bc-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.hornbill.com/<INSTANCE_NAME>/`</span><span class="sxs-lookup"><span data-stu-id="fc5bc-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.hornbill.com/<INSTANCE_NAME>/`</span></span>

    <span data-ttu-id="fc5bc-156">b.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-156">b.</span></span> <span data-ttu-id="fc5bc-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.hornbill.com/<INSTANCE_NAME>/lib/saml/auth/simplesaml/module.php/saml/sp/metadata.php/saml`</span><span class="sxs-lookup"><span data-stu-id="fc5bc-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.hornbill.com/<INSTANCE_NAME>/lib/saml/auth/simplesaml/module.php/saml/sp/metadata.php/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc5bc-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-158">These values are not real.</span></span> <span data-ttu-id="fc5bc-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fc5bc-160">Contact [Hornbill Client support team](https://www.hornbill.com/support/?request/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-160">Contact [Hornbill Client support team](https://www.hornbill.com/support/?request/) to get these values.</span></span> 

4. <span data-ttu-id="fc5bc-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/hornbill-tutorial/tutorial_hornbill_certificate.png) 

5. <span data-ttu-id="fc5bc-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/hornbill-tutorial/tutorial_general_400.png)
 
6. <span data-ttu-id="fc5bc-165">In a different web browser window, log in to Hornbill as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-165">In a different web browser window, log in to Hornbill as a Security Administrator.</span></span>

7. <span data-ttu-id="fc5bc-166">On the Home page click **System**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-166">On the Home page click **System**.</span></span>

    ![Hornbill system](./media/hornbill-tutorial/tutorial_hornbill_system.png)

8. <span data-ttu-id="fc5bc-168">Navigate to **Security**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-168">Navigate to **Security**.</span></span>

    ![Hornbill security](./media/hornbill-tutorial/tutorial_hornbill_security.png)

9. <span data-ttu-id="fc5bc-170">Click **SSO Profiles**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-170">Click **SSO Profiles**.</span></span>

    ![Hornbill single](./media/hornbill-tutorial/tutorial_hornbill_sso.png)

10. <span data-ttu-id="fc5bc-172">On the right side of the page, click on **Add logo**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-172">On the right side of the page, click on **Add logo**.</span></span>

    ![Hornbill add](./media/hornbill-tutorial/tutorial_hornbill_addlogo.png)

11. <span data-ttu-id="fc5bc-174">On the **Profile Details** bar, click on **Import SAML Meta logo**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-174">On the **Profile Details** bar, click on **Import SAML Meta logo**.</span></span>

    ![Hornbill logo](./media/hornbill-tutorial/tutorial_hornbill_logo.png)

12. <span data-ttu-id="fc5bc-176">On the Pop-up page in the **URL** text box, paste the **App Federation Metadata Url**, which you have copied from Azure portal and click **Process**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-176">On the Pop-up page in the **URL** text box, paste the **App Federation Metadata Url**, which you have copied from Azure portal and click **Process**.</span></span>

    ![Hornbill process](./media/hornbill-tutorial/tutorial_hornbill_process.png)

13. <span data-ttu-id="fc5bc-178">After clicking process the values get auto populated automatically under **Profile Details** section.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-178">After clicking process the values get auto populated automatically under **Profile Details** section.</span></span>

    ![Hornbill page1](./media/hornbill-tutorial/tutorial_hornbill_ssopage.png)

    ![Hornbill page2](./media/hornbill-tutorial/tutorial_hornbill_ssopage1.png)

    ![Hornbill page3](./media/hornbill-tutorial/tutorial_hornbill_ssopage2.png)

14. <span data-ttu-id="fc5bc-182">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-182">Click **Save Changes**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fc5bc-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fc5bc-183">Create an Azure AD test user</span></span>

<span data-ttu-id="fc5bc-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="fc5bc-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fc5bc-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fc5bc-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/hornbill-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fc5bc-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/hornbill-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fc5bc-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/hornbill-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fc5bc-193">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fc5bc-193">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/hornbill-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fc5bc-195">a.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-195">a.</span></span> <span data-ttu-id="fc5bc-196">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc5bc-197">b.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-197">b.</span></span> <span data-ttu-id="fc5bc-198">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fc5bc-199">c.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-199">c.</span></span> <span data-ttu-id="fc5bc-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fc5bc-201">d.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-201">d.</span></span> <span data-ttu-id="fc5bc-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-202">Click **Create**.</span></span>
 
### <a name="create-a-hornbill-test-user"></a><span data-ttu-id="fc5bc-203">Create a Hornbill test user</span><span class="sxs-lookup"><span data-stu-id="fc5bc-203">Create a Hornbill test user</span></span>

<span data-ttu-id="fc5bc-204">The objective of this section is to create a user called Britta Simon in Hornbill.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-204">The objective of this section is to create a user called Britta Simon in Hornbill.</span></span> <span data-ttu-id="fc5bc-205">Hornbill supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-205">Hornbill supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="fc5bc-206">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-206">There is no action item for you in this section.</span></span> <span data-ttu-id="fc5bc-207">A new user is created during an attempt to access Hornbill if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-207">A new user is created during an attempt to access Hornbill if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="fc5bc-208">If you need to create a user manually, contact [Hornbill Client support team](https://www.hornbill.com/support/?request/).</span><span class="sxs-lookup"><span data-stu-id="fc5bc-208">If you need to create a user manually, contact [Hornbill Client support team](https://www.hornbill.com/support/?request/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fc5bc-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fc5bc-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="fc5bc-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hornbill.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hornbill.</span></span>

![Assign the user role][200] 

<span data-ttu-id="fc5bc-212">**To assign Britta Simon to Hornbill, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fc5bc-212">**To assign Britta Simon to Hornbill, perform the following steps:**</span></span>

1. <span data-ttu-id="fc5bc-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="fc5bc-215">In the applications list, select **Hornbill**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-215">In the applications list, select **Hornbill**.</span></span>

    ![The Hornbill link in the Applications list](./media/hornbill-tutorial/tutorial_hornbill_app.png)  

3. <span data-ttu-id="fc5bc-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-217">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="fc5bc-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-219">Click **Add** button.</span></span> <span data-ttu-id="fc5bc-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="fc5bc-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fc5bc-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc5bc-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fc5bc-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="fc5bc-225">Test single sign-on</span></span>

<span data-ttu-id="fc5bc-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fc5bc-227">When you click the Hornbill tile in the Access Panel, you should get automatically signed-on to your Hornbill application.</span><span class="sxs-lookup"><span data-stu-id="fc5bc-227">When you click the Hornbill tile in the Access Panel, you should get automatically signed-on to your Hornbill application.</span></span>
<span data-ttu-id="fc5bc-228">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fc5bc-228">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fc5bc-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fc5bc-229">Additional resources</span></span>

* [<span data-ttu-id="fc5bc-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc5bc-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fc5bc-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fc5bc-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hornbill-tutorial/tutorial_general_01.png
[2]: ./media/hornbill-tutorial/tutorial_general_02.png
[3]: ./media/hornbill-tutorial/tutorial_general_03.png
[4]: ./media/hornbill-tutorial/tutorial_general_04.png

[100]: ./media/hornbill-tutorial/tutorial_general_100.png

[200]: ./media/hornbill-tutorial/tutorial_general_200.png
[201]: ./media/hornbill-tutorial/tutorial_general_201.png
[202]: ./media/hornbill-tutorial/tutorial_general_202.png
[203]: ./media/hornbill-tutorial/tutorial_general_203.png

