---
title: 'Tutorial: Azure Active Directory integration with Form.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Form.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f1bc0112-315c-4e6f-8c69-7c6873007bcf
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: jeedes
ms.openlocfilehash: faa89ffd572733c580235b1c6dec58893de20503
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865372"
---
# <a name="tutorial-azure-active-directory-integration-with-formcom"></a><span data-ttu-id="97aa2-103">Tutorial: Azure Active Directory integration with Form.com</span><span class="sxs-lookup"><span data-stu-id="97aa2-103">Tutorial: Azure Active Directory integration with Form.com</span></span>

<span data-ttu-id="97aa2-104">In this tutorial, you learn how to integrate Form.com with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97aa2-104">In this tutorial, you learn how to integrate Form.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97aa2-105">Integrating Form.com with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="97aa2-105">Integrating Form.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97aa2-106">You can control in Azure AD who has access to Form.com.</span><span class="sxs-lookup"><span data-stu-id="97aa2-106">You can control in Azure AD who has access to Form.com.</span></span>
- <span data-ttu-id="97aa2-107">You can enable your users to automatically get signed-on to Form.com (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="97aa2-107">You can enable your users to automatically get signed-on to Form.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="97aa2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="97aa2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="97aa2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="97aa2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97aa2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="97aa2-110">Prerequisites</span></span>

<span data-ttu-id="97aa2-111">To configure Azure AD integration with Form.com, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="97aa2-111">To configure Azure AD integration with Form.com, you need the following items:</span></span>

- <span data-ttu-id="97aa2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="97aa2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97aa2-113">A Form.com single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="97aa2-113">A Form.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97aa2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="97aa2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97aa2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="97aa2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97aa2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="97aa2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97aa2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97aa2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97aa2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="97aa2-118">Scenario description</span></span>
<span data-ttu-id="97aa2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="97aa2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97aa2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="97aa2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97aa2-121">Adding Form.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="97aa2-121">Adding Form.com from the gallery</span></span>
1. <span data-ttu-id="97aa2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="97aa2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-formcom-from-the-gallery"></a><span data-ttu-id="97aa2-123">Adding Form.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="97aa2-123">Adding Form.com from the gallery</span></span>
<span data-ttu-id="97aa2-124">To configure the integration of Form.com into Azure AD, you need to add Form.com from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="97aa2-124">To configure the integration of Form.com into Azure AD, you need to add Form.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97aa2-125">**To add Form.com from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="97aa2-125">**To add Form.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97aa2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="97aa2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="97aa2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97aa2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="97aa2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="97aa2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="97aa2-133">In the search box, type **Form.com**, select **Form.com** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="97aa2-133">In the search box, type **Form.com**, select **Form.com** from result panel then click **Add** button to add the application.</span></span>

    ![Form.com in the results list](./media/formcom-tutorial/tutorial_form.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="97aa2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="97aa2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="97aa2-136">In this section, you configure and test Azure AD single sign-on with Form.com based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="97aa2-136">In this section, you configure and test Azure AD single sign-on with Form.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="97aa2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Form.com is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97aa2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Form.com is to a user in Azure AD.</span></span> <span data-ttu-id="97aa2-138">In other words, a link relationship between an Azure AD user and the related user in Form.com needs to be established.</span><span class="sxs-lookup"><span data-stu-id="97aa2-138">In other words, a link relationship between an Azure AD user and the related user in Form.com needs to be established.</span></span>

<span data-ttu-id="97aa2-139">In Form.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="97aa2-139">In Form.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="97aa2-140">To configure and test Azure AD single sign-on with Form.com, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="97aa2-140">To configure and test Azure AD single sign-on with Form.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97aa2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="97aa2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="97aa2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97aa2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="97aa2-143">**[Create a Form.com test user](#create-a-formcom-test-user)** - to have a counterpart of Britta Simon in Form.com that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="97aa2-143">**[Create a Form.com test user](#create-a-formcom-test-user)** - to have a counterpart of Britta Simon in Form.com that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="97aa2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="97aa2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="97aa2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="97aa2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="97aa2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="97aa2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="97aa2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Form.com application.</span><span class="sxs-lookup"><span data-stu-id="97aa2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Form.com application.</span></span>

<span data-ttu-id="97aa2-148">**To configure Azure AD single sign-on with Form.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="97aa2-148">**To configure Azure AD single sign-on with Form.com, perform the following steps:**</span></span>

1. <span data-ttu-id="97aa2-149">In the Azure portal, on the **Form.com** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-149">In the Azure portal, on the **Form.com** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="97aa2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="97aa2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/formcom-tutorial/tutorial_form.com_samlbase.png)

1. <span data-ttu-id="97aa2-153">On the **Form.com Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="97aa2-153">On the **Form.com Domain and URLs** section, perform the following steps:</span></span>

    ![Form.com Domain and URLs single sign-on information](./media/formcom-tutorial/tutorial_form.com_url.png)

    <span data-ttu-id="97aa2-155">a.</span><span class="sxs-lookup"><span data-stu-id="97aa2-155">a.</span></span> <span data-ttu-id="97aa2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wa-form.com`</span><span class="sxs-lookup"><span data-stu-id="97aa2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wa-form.com`</span></span>

    <span data-ttu-id="97aa2-157">b.</span><span class="sxs-lookup"><span data-stu-id="97aa2-157">b.</span></span> <span data-ttu-id="97aa2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.form.com`</span><span class="sxs-lookup"><span data-stu-id="97aa2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.form.com`</span></span>

    <span data-ttu-id="97aa2-159">c.</span><span class="sxs-lookup"><span data-stu-id="97aa2-159">c.</span></span> <span data-ttu-id="97aa2-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="97aa2-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.wa-form.com/Member/UserAccount/SAML2.action` |
    | `https://<subdomain>.form.com/Member/UserAccount/SAML2.action` |
    
    > [!NOTE]
    > <span data-ttu-id="97aa2-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="97aa2-161">These values are not real.</span></span> <span data-ttu-id="97aa2-162">Update these values with the actual Sign-On URL, Reply URL, and Identifier.</span><span class="sxs-lookup"><span data-stu-id="97aa2-162">Update these values with the actual Sign-On URL, Reply URL, and Identifier.</span></span> <span data-ttu-id="97aa2-163">Contact [Form.com Client support team](https://form.com/about/company/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="97aa2-163">Contact [Form.com Client support team](https://form.com/about/company/contact-us/) to get these values.</span></span>

1. <span data-ttu-id="97aa2-164">On the **SAML Signing Certificate** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="97aa2-164">On the **SAML Signing Certificate** section, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/formcom-tutorial/tutorial_metadataurl.png)

    <span data-ttu-id="97aa2-166">a.</span><span class="sxs-lookup"><span data-stu-id="97aa2-166">a.</span></span> <span data-ttu-id="97aa2-167">Click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="97aa2-167">Click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    <span data-ttu-id="97aa2-168">b.</span><span class="sxs-lookup"><span data-stu-id="97aa2-168">b.</span></span> <span data-ttu-id="97aa2-169">Click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="97aa2-169">Click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>
     
1. <span data-ttu-id="97aa2-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="97aa2-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/formcom-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="97aa2-172">On the **Form.com Configuration** section, click **Configure Form.com** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="97aa2-172">On the **Form.com Configuration** section, click **Configure Form.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="97aa2-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="97aa2-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Form.com Configuration](./media/formcom-tutorial/tutorial_form.com_configure.png) 

1. <span data-ttu-id="97aa2-175">To configure single sign-on on **Form.com** side, you need to send the downloaded **Certificate (Base64)**, **App Federation Metadata Url**, and **SAML Single Sign-On Service URL** to [Form.com support team](https://form.com/about/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="97aa2-175">To configure single sign-on on **Form.com** side, you need to send the downloaded **Certificate (Base64)**, **App Federation Metadata Url**, and **SAML Single Sign-On Service URL** to [Form.com support team](https://form.com/about/company/contact-us/).</span></span> <span data-ttu-id="97aa2-176">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="97aa2-176">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="97aa2-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="97aa2-177">Create an Azure AD test user</span></span>

<span data-ttu-id="97aa2-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97aa2-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="97aa2-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="97aa2-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97aa2-181">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="97aa2-181">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/formcom-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="97aa2-183">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-183">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/formcom-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="97aa2-185">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="97aa2-185">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/formcom-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="97aa2-187">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="97aa2-187">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/formcom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="97aa2-189">a.</span><span class="sxs-lookup"><span data-stu-id="97aa2-189">a.</span></span> <span data-ttu-id="97aa2-190">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-190">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97aa2-191">b.</span><span class="sxs-lookup"><span data-stu-id="97aa2-191">b.</span></span> <span data-ttu-id="97aa2-192">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97aa2-192">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="97aa2-193">c.</span><span class="sxs-lookup"><span data-stu-id="97aa2-193">c.</span></span> <span data-ttu-id="97aa2-194">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="97aa2-194">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="97aa2-195">d.</span><span class="sxs-lookup"><span data-stu-id="97aa2-195">d.</span></span> <span data-ttu-id="97aa2-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-196">Click **Create**.</span></span>
 
### <a name="create-a-formcom-test-user"></a><span data-ttu-id="97aa2-197">Create a Form.com test user</span><span class="sxs-lookup"><span data-stu-id="97aa2-197">Create a Form.com test user</span></span>

<span data-ttu-id="97aa2-198">The objective of this section is to create a user called Britta Simon in Form.com.</span><span class="sxs-lookup"><span data-stu-id="97aa2-198">The objective of this section is to create a user called Britta Simon in Form.com.</span></span> <span data-ttu-id="97aa2-199">Work with [Form.com support team](https://form.com/about/company/contact-us/) to add the users in the Form.com account.</span><span class="sxs-lookup"><span data-stu-id="97aa2-199">Work with [Form.com support team](https://form.com/about/company/contact-us/) to add the users in the Form.com account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="97aa2-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="97aa2-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="97aa2-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Form.com.</span><span class="sxs-lookup"><span data-stu-id="97aa2-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Form.com.</span></span>

![Assign the user role][200] 

<span data-ttu-id="97aa2-203">**To assign Britta Simon to Form.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="97aa2-203">**To assign Britta Simon to Form.com, perform the following steps:**</span></span>

1. <span data-ttu-id="97aa2-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="97aa2-206">In the applications list, select **Form.com**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-206">In the applications list, select **Form.com**.</span></span>

    ![The Form.com link in the Applications list](./media/formcom-tutorial/tutorial_form.com_app.png)  

1. <span data-ttu-id="97aa2-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="97aa2-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="97aa2-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="97aa2-210">Click **Add** button.</span></span> <span data-ttu-id="97aa2-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="97aa2-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="97aa2-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="97aa2-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="97aa2-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="97aa2-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="97aa2-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="97aa2-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="97aa2-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="97aa2-216">Test single sign-on</span></span>

<span data-ttu-id="97aa2-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="97aa2-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="97aa2-218">When you click the Form.com tile in the Access Panel, you should get automatically signed-on to your Form.com application.</span><span class="sxs-lookup"><span data-stu-id="97aa2-218">When you click the Form.com tile in the Access Panel, you should get automatically signed-on to your Form.com application.</span></span>
<span data-ttu-id="97aa2-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97aa2-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="97aa2-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="97aa2-220">Additional resources</span></span>

* [<span data-ttu-id="97aa2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97aa2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="97aa2-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97aa2-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/formcom-tutorial/tutorial_general_01.png
[2]: ./media/formcom-tutorial/tutorial_general_02.png
[3]: ./media/formcom-tutorial/tutorial_general_03.png
[4]: ./media/formcom-tutorial/tutorial_general_04.png

[100]: ./media/formcom-tutorial/tutorial_general_100.png

[200]: ./media/formcom-tutorial/tutorial_general_200.png
[201]: ./media/formcom-tutorial/tutorial_general_201.png
[202]: ./media/formcom-tutorial/tutorial_general_202.png
[203]: ./media/formcom-tutorial/tutorial_general_203.png

