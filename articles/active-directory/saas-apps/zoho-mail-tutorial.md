---
title: 'Tutorial: Azure Active Directory integration with Zoho | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 03950d983f6ed119ae6cf7a7391418804bb20c76
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869087"
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="94d71-103">Tutorial: Azure Active Directory integration with Zoho</span><span class="sxs-lookup"><span data-stu-id="94d71-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="94d71-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94d71-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94d71-105">Integrating Zoho with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="94d71-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94d71-106">You can control in Azure AD who has access to Zoho.</span><span class="sxs-lookup"><span data-stu-id="94d71-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="94d71-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="94d71-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="94d71-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94d71-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="94d71-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="94d71-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94d71-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="94d71-110">Prerequisites</span></span>

<span data-ttu-id="94d71-111">To configure Azure AD integration with Zoho, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="94d71-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="94d71-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="94d71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94d71-113">A Zoho single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="94d71-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94d71-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="94d71-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94d71-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="94d71-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94d71-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="94d71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94d71-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94d71-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94d71-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="94d71-118">Scenario description</span></span>
<span data-ttu-id="94d71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="94d71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94d71-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="94d71-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94d71-121">Adding Zoho from the gallery</span><span class="sxs-lookup"><span data-stu-id="94d71-121">Adding Zoho from the gallery</span></span>
1. <span data-ttu-id="94d71-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="94d71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="94d71-123">Adding Zoho from the gallery</span><span class="sxs-lookup"><span data-stu-id="94d71-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="94d71-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="94d71-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94d71-125">**To add Zoho from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94d71-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94d71-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="94d71-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="94d71-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="94d71-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94d71-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="94d71-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="94d71-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="94d71-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="94d71-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="94d71-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho in the results list](./media/zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="94d71-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="94d71-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="94d71-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94d71-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94d71-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94d71-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="94d71-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span><span class="sxs-lookup"><span data-stu-id="94d71-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="94d71-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="94d71-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94d71-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="94d71-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94d71-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="94d71-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="94d71-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94d71-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="94d71-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="94d71-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="94d71-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="94d71-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="94d71-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="94d71-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="94d71-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="94d71-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="94d71-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span><span class="sxs-lookup"><span data-stu-id="94d71-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="94d71-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94d71-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="94d71-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="94d71-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="94d71-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="94d71-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/zoho-mail-tutorial/tutorial_zoho_samlbase.png)

1. <span data-ttu-id="94d71-153">On the **Zoho Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="94d71-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Zoho Domain and URLs single sign-on information](./media/zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="94d71-155">a.</span><span class="sxs-lookup"><span data-stu-id="94d71-155">a.</span></span> <span data-ttu-id="94d71-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="94d71-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94d71-157">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="94d71-157">This value is not real.</span></span> <span data-ttu-id="94d71-158">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="94d71-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="94d71-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span><span class="sxs-lookup"><span data-stu-id="94d71-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
1. <span data-ttu-id="94d71-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="94d71-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/zoho-mail-tutorial/tutorial_zoho_certificate.png) 

1. <span data-ttu-id="94d71-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="94d71-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zoho-mail-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="94d71-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="94d71-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94d71-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="94d71-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoho Configuration](./media/zoho-mail-tutorial/tutorial_zoho_configure.png) 

1. <span data-ttu-id="94d71-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="94d71-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

1. <span data-ttu-id="94d71-168">Go to the **Control panel**.</span><span class="sxs-lookup"><span data-stu-id="94d71-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="94d71-169">![Control Panel](./media/zoho-mail-tutorial/ic789607.png "Control Panel")</span><span class="sxs-lookup"><span data-stu-id="94d71-169">![Control Panel](./media/zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

1. <span data-ttu-id="94d71-170">Click the **SAML Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="94d71-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="94d71-171">![SAML Authentication](./media/zoho-mail-tutorial/ic789608.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="94d71-171">![SAML Authentication](./media/zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

1. <span data-ttu-id="94d71-172">In the **SAML Authentication Details** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="94d71-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="94d71-173">![SAML Authentication Details](./media/zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span><span class="sxs-lookup"><span data-stu-id="94d71-173">![SAML Authentication Details](./media/zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="94d71-174">a.</span><span class="sxs-lookup"><span data-stu-id="94d71-174">a.</span></span> <span data-ttu-id="94d71-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94d71-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="94d71-176">b.</span><span class="sxs-lookup"><span data-stu-id="94d71-176">b.</span></span> <span data-ttu-id="94d71-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94d71-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="94d71-178">c.</span><span class="sxs-lookup"><span data-stu-id="94d71-178">c.</span></span> <span data-ttu-id="94d71-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94d71-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="94d71-180">d.</span><span class="sxs-lookup"><span data-stu-id="94d71-180">d.</span></span> <span data-ttu-id="94d71-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span><span class="sxs-lookup"><span data-stu-id="94d71-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="94d71-182">e.</span><span class="sxs-lookup"><span data-stu-id="94d71-182">e.</span></span> <span data-ttu-id="94d71-183">As **Algorithm**, select **RSA**.</span><span class="sxs-lookup"><span data-stu-id="94d71-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="94d71-184">f.</span><span class="sxs-lookup"><span data-stu-id="94d71-184">f.</span></span> <span data-ttu-id="94d71-185">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="94d71-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="94d71-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="94d71-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94d71-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="94d71-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94d71-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94d71-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="94d71-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="94d71-189">Create an Azure AD test user</span></span>

<span data-ttu-id="94d71-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94d71-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="94d71-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94d71-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94d71-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="94d71-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zoho-mail-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="94d71-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="94d71-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zoho-mail-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="94d71-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="94d71-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zoho-mail-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="94d71-199">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="94d71-199">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="94d71-201">a.</span><span class="sxs-lookup"><span data-stu-id="94d71-201">a.</span></span> <span data-ttu-id="94d71-202">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94d71-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94d71-203">b.</span><span class="sxs-lookup"><span data-stu-id="94d71-203">b.</span></span> <span data-ttu-id="94d71-204">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94d71-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="94d71-205">c.</span><span class="sxs-lookup"><span data-stu-id="94d71-205">c.</span></span> <span data-ttu-id="94d71-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="94d71-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="94d71-207">d.</span><span class="sxs-lookup"><span data-stu-id="94d71-207">d.</span></span> <span data-ttu-id="94d71-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="94d71-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="94d71-209">Create a Zoho test user</span><span class="sxs-lookup"><span data-stu-id="94d71-209">Create a Zoho test user</span></span>

<span data-ttu-id="94d71-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="94d71-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="94d71-211">In the case of Zoho Mail, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="94d71-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="94d71-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="94d71-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="94d71-213">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="94d71-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="94d71-214">Log in to your **Zoho Mail** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="94d71-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

1. <span data-ttu-id="94d71-215">Go to **Control Panel \> Mail & Docs**.</span><span class="sxs-lookup"><span data-stu-id="94d71-215">Go to **Control Panel \> Mail & Docs**.</span></span>

1. <span data-ttu-id="94d71-216">Go to **User Details \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="94d71-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="94d71-217">![Add User](./media/zoho-mail-tutorial/ic789611.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="94d71-217">![Add User](./media/zoho-mail-tutorial/ic789611.png "Add User")</span></span>

1. <span data-ttu-id="94d71-218">On the **Add users** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="94d71-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="94d71-219">![Add User](./media/zoho-mail-tutorial/ic789612.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="94d71-219">![Add User](./media/zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="94d71-220">a.</span><span class="sxs-lookup"><span data-stu-id="94d71-220">a.</span></span> <span data-ttu-id="94d71-221">In the **First Name** textbox, type the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="94d71-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="94d71-222">b.</span><span class="sxs-lookup"><span data-stu-id="94d71-222">b.</span></span> <span data-ttu-id="94d71-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="94d71-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="94d71-224">c.</span><span class="sxs-lookup"><span data-stu-id="94d71-224">c.</span></span> <span data-ttu-id="94d71-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="94d71-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="94d71-226">d.</span><span class="sxs-lookup"><span data-stu-id="94d71-226">d.</span></span> <span data-ttu-id="94d71-227">In the **Password** textbox, enter password of user.</span><span class="sxs-lookup"><span data-stu-id="94d71-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="94d71-228">e.</span><span class="sxs-lookup"><span data-stu-id="94d71-228">e.</span></span> <span data-ttu-id="94d71-229">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="94d71-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="94d71-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="94d71-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="94d71-231">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="94d71-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="94d71-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span><span class="sxs-lookup"><span data-stu-id="94d71-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Assign the user role][200] 

<span data-ttu-id="94d71-234">**To assign Britta Simon to Zoho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94d71-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="94d71-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="94d71-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="94d71-237">In the applications list, select **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="94d71-237">In the applications list, select **Zoho**.</span></span>

    ![The Zoho link in the Applications list](./media/zoho-mail-tutorial/tutorial_zoho_app.png)  

1. <span data-ttu-id="94d71-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="94d71-239">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="94d71-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="94d71-241">Click **Add** button.</span></span> <span data-ttu-id="94d71-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="94d71-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="94d71-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="94d71-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="94d71-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="94d71-245">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="94d71-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="94d71-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="94d71-247">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="94d71-247">Test single sign-on</span></span>

<span data-ttu-id="94d71-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="94d71-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94d71-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span><span class="sxs-lookup"><span data-stu-id="94d71-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="94d71-250">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="94d71-250">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="94d71-251">Additional resources</span><span class="sxs-lookup"><span data-stu-id="94d71-251">Additional resources</span></span>

* [<span data-ttu-id="94d71-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94d71-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="94d71-253">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94d71-253">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/zoho-mail-tutorial/tutorial_general_203.png

