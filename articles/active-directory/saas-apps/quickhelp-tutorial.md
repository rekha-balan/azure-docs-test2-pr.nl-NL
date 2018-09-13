---
title: 'Tutorial: Azure Active Directory integration with QuickHelp | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and QuickHelp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: c99be60301085dddfd5c658ee1eed81b88238e54
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856058"
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="7f5b1-103">Tutorial: Azure Active Directory integration with QuickHelp</span><span class="sxs-lookup"><span data-stu-id="7f5b1-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="7f5b1-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f5b1-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f5b1-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f5b1-106">You can control in Azure AD who has access to QuickHelp</span><span class="sxs-lookup"><span data-stu-id="7f5b1-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="7f5b1-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7f5b1-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f5b1-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7f5b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7f5b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7f5b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f5b1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f5b1-110">Prerequisites</span></span>

<span data-ttu-id="7f5b1-111">To configure Azure AD integration with QuickHelp, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="7f5b1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7f5b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f5b1-113">A QuickHelp single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7f5b1-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f5b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f5b1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f5b1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f5b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f5b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f5b1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7f5b1-118">Scenario description</span></span>
<span data-ttu-id="7f5b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f5b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f5b1-121">Adding QuickHelp from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f5b1-121">Adding QuickHelp from the gallery</span></span>
1. <span data-ttu-id="7f5b1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f5b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="7f5b1-123">Adding QuickHelp from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f5b1-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="7f5b1-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f5b1-125">**To add QuickHelp from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f5b1-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f5b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7f5b1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f5b1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7f5b1-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7f5b1-133">In the search box, type **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-133">In the search box, type **QuickHelp**.</span></span>

    ![Creating an Azure AD test user](./media/quickhelp-tutorial/tutorial_quickhelp_search.png)

1. <span data-ttu-id="7f5b1-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f5b1-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f5b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f5b1-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7f5b1-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f5b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="7f5b1-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="7f5b1-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7f5b1-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f5b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7f5b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7f5b1-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7f5b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7f5b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f5b1-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f5b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f5b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="7f5b1-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f5b1-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="7f5b1-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7f5b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

1. <span data-ttu-id="7f5b1-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="7f5b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-157">a.</span></span> <span data-ttu-id="7f5b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<ROUTEURL>`</span><span class="sxs-lookup"><span data-stu-id="7f5b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<ROUTEURL>`</span></span>

    <span data-ttu-id="7f5b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-159">b.</span></span> <span data-ttu-id="7f5b1-160">In the **Identifier** textbox, type a URL: `https://auth.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="7f5b1-160">In the **Identifier** textbox, type a URL: `https://auth.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f5b1-161">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-161">The Sign-on URL value is not real.</span></span> <span data-ttu-id="7f5b1-162">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="7f5b1-163">Contact your organization’s QuickHelp administrator or your BrainStorm Client Success Manager to get the value.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-163">Contact your organization’s QuickHelp administrator or your BrainStorm Client Success Manager to get the value.</span></span>
 
1. <span data-ttu-id="7f5b1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

1. <span data-ttu-id="7f5b1-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_general_400.png) 

1. <span data-ttu-id="7f5b1-168">Sign-on to your QuickHelp company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-168">Sign-on to your QuickHelp company site as administrator.</span></span>

1. <span data-ttu-id="7f5b1-169">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configure Single Sign-On][21]

1. <span data-ttu-id="7f5b1-171">In the **QuickHelp Admin** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configure Single Sign-On][22]

1. <span data-ttu-id="7f5b1-173">Click **Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-173">Click **Authentication Settings**.</span></span>

1. <span data-ttu-id="7f5b1-174">On the **Authentication Settings** page, perform the following steps</span><span class="sxs-lookup"><span data-stu-id="7f5b1-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Configure Single Sign-On][23]
   
    <span data-ttu-id="7f5b1-176">a.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-176">a.</span></span> <span data-ttu-id="7f5b1-177">As **SSO Type**, select **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="7f5b1-178">b.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-178">b.</span></span> <span data-ttu-id="7f5b1-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="7f5b1-180">c.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-180">c.</span></span> <span data-ttu-id="7f5b1-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="7f5b1-182">d.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-182">d.</span></span> <span data-ttu-id="7f5b1-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="7f5b1-184">e.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-184">e.</span></span> <span data-ttu-id="7f5b1-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="7f5b1-186">f.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-186">f.</span></span> <span data-ttu-id="7f5b1-187">In the **Action Bar**, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-187">In the **Action Bar**, click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f5b1-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f5b1-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f5b1-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7f5b1-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f5b1-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f5b1-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/quickhelp-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7f5b1-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/quickhelp-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7f5b1-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/quickhelp-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7f5b1-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f5b1-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f5b1-200">a.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-200">a.</span></span> <span data-ttu-id="7f5b1-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f5b1-202">b.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-202">b.</span></span> <span data-ttu-id="7f5b1-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f5b1-204">c.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-204">c.</span></span> <span data-ttu-id="7f5b1-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7f5b1-206">d.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-206">d.</span></span> <span data-ttu-id="7f5b1-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-207">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="7f5b1-208">Creating a QuickHelp test user</span><span class="sxs-lookup"><span data-stu-id="7f5b1-208">Creating a QuickHelp test user</span></span>

<span data-ttu-id="7f5b1-209">The objective of this section is to create a user called Britta Simon in QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-209">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="7f5b1-210">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-210">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="7f5b1-211">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-211">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="7f5b1-212">QuickHelp supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-212">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="7f5b1-213">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-213">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="7f5b1-214">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-214">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7f5b1-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f5b1-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7f5b1-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Assign User][200] 

<span data-ttu-id="7f5b1-218">**To assign Britta Simon to QuickHelp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f5b1-218">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="7f5b1-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7f5b1-221">In the applications list, select **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-221">In the applications list, select **QuickHelp**.</span></span>

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_app.png) 

1. <span data-ttu-id="7f5b1-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7f5b1-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-225">Click **Add** button.</span></span> <span data-ttu-id="7f5b1-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7f5b1-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7f5b1-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7f5b1-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f5b1-231">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f5b1-231">Testing single sign-on</span></span>

<span data-ttu-id="7f5b1-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="7f5b1-233">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span><span class="sxs-lookup"><span data-stu-id="7f5b1-233">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7f5b1-234">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7f5b1-234">Additional resources</span></span>

* [<span data-ttu-id="7f5b1-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f5b1-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7f5b1-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f5b1-236">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/quickhelp-tutorial/tutorial_quickhelp_07.png
