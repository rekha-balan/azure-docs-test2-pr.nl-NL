---
title: 'Tutorial: Azure Active Directory integration with XaitPorter | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and XaitPorter.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d33c7cb7-0550-425b-882a-619a713a71b7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: jeedes
ms.openlocfilehash: 12fb8e5b2b940c48de766a48f59ed0cc342b5356
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858073"
---
# <a name="tutorial-azure-active-directory-integration-with-xaitporter"></a><span data-ttu-id="a438d-103">Tutorial: Azure Active Directory integration with XaitPorter</span><span class="sxs-lookup"><span data-stu-id="a438d-103">Tutorial: Azure Active Directory integration with XaitPorter</span></span>

<span data-ttu-id="a438d-104">In this tutorial, you learn how to integrate XaitPorter with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a438d-104">In this tutorial, you learn how to integrate XaitPorter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a438d-105">Integrating XaitPorter with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a438d-105">Integrating XaitPorter with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a438d-106">You can control in Azure AD who has access to XaitPorter.</span><span class="sxs-lookup"><span data-stu-id="a438d-106">You can control in Azure AD who has access to XaitPorter.</span></span>
- <span data-ttu-id="a438d-107">You can enable your users to automatically get signed-on to XaitPorter (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a438d-107">You can enable your users to automatically get signed-on to XaitPorter (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a438d-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a438d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a438d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a438d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a438d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a438d-110">Prerequisites</span></span>

<span data-ttu-id="a438d-111">To configure Azure AD integration with XaitPorter, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a438d-111">To configure Azure AD integration with XaitPorter, you need the following items:</span></span>

- <span data-ttu-id="a438d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a438d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a438d-113">A XaitPorter single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a438d-113">A XaitPorter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a438d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a438d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a438d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a438d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a438d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a438d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a438d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a438d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a438d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a438d-118">Scenario description</span></span>
<span data-ttu-id="a438d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a438d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a438d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a438d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a438d-121">Adding XaitPorter from the gallery</span><span class="sxs-lookup"><span data-stu-id="a438d-121">Adding XaitPorter from the gallery</span></span>
1. <span data-ttu-id="a438d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a438d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xaitporter-from-the-gallery"></a><span data-ttu-id="a438d-123">Adding XaitPorter from the gallery</span><span class="sxs-lookup"><span data-stu-id="a438d-123">Adding XaitPorter from the gallery</span></span>
<span data-ttu-id="a438d-124">To configure the integration of XaitPorter into Azure AD, you need to add XaitPorter from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a438d-124">To configure the integration of XaitPorter into Azure AD, you need to add XaitPorter from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a438d-125">**To add XaitPorter from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a438d-125">**To add XaitPorter from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a438d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a438d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a438d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a438d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a438d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a438d-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a438d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a438d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a438d-133">In the search box, type **XaitPorter**, select **XaitPorter** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a438d-133">In the search box, type **XaitPorter**, select **XaitPorter** from result panel then click **Add** button to add the application.</span></span>

    ![XaitPorter in the results list](./media/xaitporter-tutorial/tutorial_xaitporter_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a438d-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a438d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a438d-136">In this section, you configure and test Azure AD single sign-on with XaitPorter based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a438d-136">In this section, you configure and test Azure AD single sign-on with XaitPorter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a438d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in XaitPorter is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a438d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in XaitPorter is to a user in Azure AD.</span></span> <span data-ttu-id="a438d-138">In other words, a link relationship between an Azure AD user and the related user in XaitPorter needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a438d-138">In other words, a link relationship between an Azure AD user and the related user in XaitPorter needs to be established.</span></span>

<span data-ttu-id="a438d-139">In XaitPorter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a438d-139">In XaitPorter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a438d-140">To configure and test Azure AD single sign-on with XaitPorter, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a438d-140">To configure and test Azure AD single sign-on with XaitPorter, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a438d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a438d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a438d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a438d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a438d-143">**[Create a XaitPorter test user](#create-a-xaitporter-test-user)** - to have a counterpart of Britta Simon in XaitPorter that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a438d-143">**[Create a XaitPorter test user](#create-a-xaitporter-test-user)** - to have a counterpart of Britta Simon in XaitPorter that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a438d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a438d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a438d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a438d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a438d-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a438d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a438d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your XaitPorter application.</span><span class="sxs-lookup"><span data-stu-id="a438d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your XaitPorter application.</span></span>

<span data-ttu-id="a438d-148">**To configure Azure AD single sign-on with XaitPorter, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a438d-148">**To configure Azure AD single sign-on with XaitPorter, perform the following steps:**</span></span>

1. <span data-ttu-id="a438d-149">In the Azure portal, on the **XaitPorter** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a438d-149">In the Azure portal, on the **XaitPorter** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a438d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a438d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/xaitporter-tutorial/tutorial_xaitporter_samlbase.png)

1. <span data-ttu-id="a438d-153">On the **XaitPorter Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a438d-153">On the **XaitPorter Domain and URLs** section, perform the following steps:</span></span>

    ![XaitPorter Domain and URLs single sign-on information](./media/xaitporter-tutorial/tutorial_xaitporter_url.png)

    <span data-ttu-id="a438d-155">a.</span><span class="sxs-lookup"><span data-stu-id="a438d-155">a.</span></span> <span data-ttu-id="a438d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.xaitporter.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="a438d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.xaitporter.com/saml/login`</span></span>

    <span data-ttu-id="a438d-157">b.</span><span class="sxs-lookup"><span data-stu-id="a438d-157">b.</span></span> <span data-ttu-id="a438d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.xaitporter.com`</span><span class="sxs-lookup"><span data-stu-id="a438d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.xaitporter.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a438d-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a438d-159">These values are not real.</span></span> <span data-ttu-id="a438d-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="a438d-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a438d-161">Contact [XaitPorter Client support team](https://www.xait.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a438d-161">Contact [XaitPorter Client support team](https://www.xait.com/support/) to get these values.</span></span>
     
1. <span data-ttu-id="a438d-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="a438d-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span> 

    ![The Certificate download link](./media/xaitporter-tutorial/tutorial_xaitporter_certificate.png) 

1. <span data-ttu-id="a438d-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a438d-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/xaitporter-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a438d-166">Provide the **IP address** or the **App Federation Metadata Url** to the [SmartRecruiters support team](https://www.smartrecruiters.com/about-us/contact-us/), so that XaitPorter can ensure that IP address is reachable from your XaitPorter instance configuring whitelist at their side.</span><span class="sxs-lookup"><span data-stu-id="a438d-166">Provide the **IP address** or the **App Federation Metadata Url** to the [SmartRecruiters support team](https://www.smartrecruiters.com/about-us/contact-us/), so that XaitPorter can ensure that IP address is reachable from your XaitPorter instance configuring whitelist at their side.</span></span> 

1. <span data-ttu-id="a438d-167">In a different web browser window, log in to your XaitPorter company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a438d-167">In a different web browser window, log in to your XaitPorter company site as an administrator.</span></span>

1. <span data-ttu-id="a438d-168">Click on **Admin**.</span><span class="sxs-lookup"><span data-stu-id="a438d-168">Click on **Admin**.</span></span>

    ![Configure Single Sign-On](./media/xaitporter-tutorial/user1.png)

1. <span data-ttu-id="a438d-170">Select **Manage Single Sign-On** from the **System Setup** dropdown list.</span><span class="sxs-lookup"><span data-stu-id="a438d-170">Select **Manage Single Sign-On** from the **System Setup** dropdown list.</span></span>

    ![Configure Single Sign-On](./media/xaitporter-tutorial/user2.png)

1. <span data-ttu-id="a438d-172">In the **MANAGE SINGLE SIGN-ON** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a438d-172">In the **MANAGE SINGLE SIGN-ON** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/xaitporter-tutorial/user3.png)

    <span data-ttu-id="a438d-174">a.</span><span class="sxs-lookup"><span data-stu-id="a438d-174">a.</span></span> <span data-ttu-id="a438d-175">Select **Enable Single Sign-On Authentication**.</span><span class="sxs-lookup"><span data-stu-id="a438d-175">Select **Enable Single Sign-On Authentication**.</span></span>

    <span data-ttu-id="a438d-176">b.</span><span class="sxs-lookup"><span data-stu-id="a438d-176">b.</span></span> <span data-ttu-id="a438d-177">In **Identity Provider Settings** textbox, paste **App Federation Metadata Url** which you have copied from the Azure portal and click **Fetch**.</span><span class="sxs-lookup"><span data-stu-id="a438d-177">In **Identity Provider Settings** textbox, paste **App Federation Metadata Url** which you have copied from the Azure portal and click **Fetch**.</span></span>

    <span data-ttu-id="a438d-178">c.</span><span class="sxs-lookup"><span data-stu-id="a438d-178">c.</span></span> <span data-ttu-id="a438d-179">Select **Enable Autocreation of Users**.</span><span class="sxs-lookup"><span data-stu-id="a438d-179">Select **Enable Autocreation of Users**.</span></span>

    <span data-ttu-id="a438d-180">d.</span><span class="sxs-lookup"><span data-stu-id="a438d-180">d.</span></span> <span data-ttu-id="a438d-181">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a438d-181">Click **OK**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a438d-182">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a438d-182">Create an Azure AD test user</span></span>

<span data-ttu-id="a438d-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a438d-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a438d-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a438d-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a438d-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a438d-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/xaitporter-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a438d-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a438d-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/xaitporter-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a438d-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a438d-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/xaitporter-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a438d-192">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a438d-192">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/xaitporter-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a438d-194">a.</span><span class="sxs-lookup"><span data-stu-id="a438d-194">a.</span></span> <span data-ttu-id="a438d-195">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a438d-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a438d-196">b.</span><span class="sxs-lookup"><span data-stu-id="a438d-196">b.</span></span> <span data-ttu-id="a438d-197">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a438d-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a438d-198">c.</span><span class="sxs-lookup"><span data-stu-id="a438d-198">c.</span></span> <span data-ttu-id="a438d-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a438d-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a438d-200">d.</span><span class="sxs-lookup"><span data-stu-id="a438d-200">d.</span></span> <span data-ttu-id="a438d-201">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a438d-201">Click **Create**.</span></span>
 
### <a name="create-a-xaitporter-test-user"></a><span data-ttu-id="a438d-202">Create a XaitPorter test user</span><span class="sxs-lookup"><span data-stu-id="a438d-202">Create a XaitPorter test user</span></span>

<span data-ttu-id="a438d-203">In this section, you create a user called Britta Simon in XaitPorter.</span><span class="sxs-lookup"><span data-stu-id="a438d-203">In this section, you create a user called Britta Simon in XaitPorter.</span></span> <span data-ttu-id="a438d-204">Work with [XaitPorter Client support team](https://www.xait.com/support/) to add the users in the XaitPorter platform.</span><span class="sxs-lookup"><span data-stu-id="a438d-204">Work with [XaitPorter Client support team](https://www.xait.com/support/) to add the users in the XaitPorter platform.</span></span> <span data-ttu-id="a438d-205">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a438d-205">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a438d-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a438d-206">Assign the Azure AD test user</span></span>

<span data-ttu-id="a438d-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to XaitPorter.</span><span class="sxs-lookup"><span data-stu-id="a438d-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to XaitPorter.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a438d-209">**To assign Britta Simon to XaitPorter, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a438d-209">**To assign Britta Simon to XaitPorter, perform the following steps:**</span></span>

1. <span data-ttu-id="a438d-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a438d-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a438d-212">In the applications list, select **XaitPorter**.</span><span class="sxs-lookup"><span data-stu-id="a438d-212">In the applications list, select **XaitPorter**.</span></span>

    ![The XaitPorter link in the Applications list](./media/xaitporter-tutorial/tutorial_xaitporter_app.png)  

1. <span data-ttu-id="a438d-214">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a438d-214">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a438d-216">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a438d-216">Click **Add** button.</span></span> <span data-ttu-id="a438d-217">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a438d-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a438d-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a438d-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a438d-220">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a438d-220">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a438d-221">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a438d-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a438d-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a438d-222">Test single sign-on</span></span>

<span data-ttu-id="a438d-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a438d-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a438d-224">When you click the XaitPorter tile in the Access Panel, you should get automatically signed-on to your XaitPorter application.</span><span class="sxs-lookup"><span data-stu-id="a438d-224">When you click the XaitPorter tile in the Access Panel, you should get automatically signed-on to your XaitPorter application.</span></span>
<span data-ttu-id="a438d-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a438d-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a438d-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a438d-226">Additional resources</span></span>

* [<span data-ttu-id="a438d-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a438d-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a438d-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a438d-228">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/xaitporter-tutorial/tutorial_general_01.png
[2]: ./media/xaitporter-tutorial/tutorial_general_02.png
[3]: ./media/xaitporter-tutorial/tutorial_general_03.png
[4]: ./media/xaitporter-tutorial/tutorial_general_04.png

[100]: ./media/xaitporter-tutorial/tutorial_general_100.png

[200]: ./media/xaitporter-tutorial/tutorial_general_200.png
[201]: ./media/xaitporter-tutorial/tutorial_general_201.png
[202]: ./media/xaitporter-tutorial/tutorial_general_202.png
[203]: ./media/xaitporter-tutorial/tutorial_general_203.png

