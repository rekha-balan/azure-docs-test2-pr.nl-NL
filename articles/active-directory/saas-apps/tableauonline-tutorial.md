---
title: 'Tutorial: Azure Active Directory integration with Tableau Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tableau Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: b0aaa27164c84a06c6fad92d5036a00ca5a319f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969186"
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="83348-103">Tutorial: Azure Active Directory integration with Tableau Online</span><span class="sxs-lookup"><span data-stu-id="83348-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="83348-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83348-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83348-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="83348-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83348-106">You can control in Azure AD who has access to Tableau Online</span><span class="sxs-lookup"><span data-stu-id="83348-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="83348-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="83348-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83348-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="83348-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="83348-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="83348-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83348-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="83348-110">Prerequisites</span></span>

<span data-ttu-id="83348-111">To configure Azure AD integration with Tableau Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="83348-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="83348-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="83348-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83348-113">A Tableau Online single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="83348-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83348-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="83348-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83348-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="83348-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83348-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="83348-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83348-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83348-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83348-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="83348-118">Scenario description</span></span>
<span data-ttu-id="83348-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="83348-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83348-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="83348-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83348-121">Adding Tableau Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="83348-121">Adding Tableau Online from the gallery</span></span>
1. <span data-ttu-id="83348-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="83348-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="83348-123">Adding Tableau Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="83348-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="83348-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="83348-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83348-125">**To add Tableau Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="83348-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83348-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="83348-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="83348-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="83348-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83348-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="83348-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="83348-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="83348-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="83348-133">In the search box, type **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="83348-133">In the search box, type **Tableau Online**.</span></span>

    ![Creating an Azure AD test user](./media/tableauonline-tutorial/tutorial_tableauonline_search.png)

1. <span data-ttu-id="83348-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="83348-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83348-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="83348-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83348-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="83348-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83348-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83348-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="83348-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="83348-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="83348-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="83348-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83348-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="83348-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83348-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="83348-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="83348-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83348-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="83348-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="83348-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="83348-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="83348-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="83348-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="83348-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83348-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="83348-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83348-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span><span class="sxs-lookup"><span data-stu-id="83348-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="83348-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="83348-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="83348-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="83348-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="83348-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="83348-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

1. <span data-ttu-id="83348-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="83348-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="83348-157">a.</span><span class="sxs-lookup"><span data-stu-id="83348-157">a.</span></span> <span data-ttu-id="83348-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="83348-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="83348-159">b.</span><span class="sxs-lookup"><span data-stu-id="83348-159">b.</span></span> <span data-ttu-id="83348-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/metadata?alias=<entityid> `</span><span class="sxs-lookup"><span data-stu-id="83348-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/metadata?alias=<entityid> `</span></span>

1. <span data-ttu-id="83348-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="83348-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

1. <span data-ttu-id="83348-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="83348-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="83348-165">In a different browser window, sign-on to your Tableau Online application.</span><span class="sxs-lookup"><span data-stu-id="83348-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="83348-166">Go to **Settings** and then **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="83348-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_09.png)
    
1. <span data-ttu-id="83348-168">To enable SAML, Under **Authentication Types** section.</span><span class="sxs-lookup"><span data-stu-id="83348-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="83348-169">Check the **Single sign-on with SAML** checkbox.</span><span class="sxs-lookup"><span data-stu-id="83348-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_12.png)

1. <span data-ttu-id="83348-171">Scroll down until **Import metadata file into Tableau Online** section.</span><span class="sxs-lookup"><span data-stu-id="83348-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="83348-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83348-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="83348-173">Then, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="83348-173">Then, click **Apply**.</span></span>
   
   ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_13.png)

1. <span data-ttu-id="83348-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span><span class="sxs-lookup"><span data-stu-id="83348-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="83348-176">To get this information from Azure AD:</span><span class="sxs-lookup"><span data-stu-id="83348-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="83348-177">a.</span><span class="sxs-lookup"><span data-stu-id="83348-177">a.</span></span> <span data-ttu-id="83348-178">In the Azure portal, go on the **Tableau Online** application integration page.</span><span class="sxs-lookup"><span data-stu-id="83348-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="83348-179">b.</span><span class="sxs-lookup"><span data-stu-id="83348-179">b.</span></span> <span data-ttu-id="83348-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span><span class="sxs-lookup"><span data-stu-id="83348-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configure Single Sign-On](./media/tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="83348-182">c.</span><span class="sxs-lookup"><span data-stu-id="83348-182">c.</span></span> <span data-ttu-id="83348-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="83348-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Azure AD Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="83348-185">d.</span><span class="sxs-lookup"><span data-stu-id="83348-185">d.</span></span> <span data-ttu-id="83348-186">Click **user.givenname** value</span><span class="sxs-lookup"><span data-stu-id="83348-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="83348-187">e.</span><span class="sxs-lookup"><span data-stu-id="83348-187">e.</span></span> <span data-ttu-id="83348-188">Copy the value from the **namespace** textbox.</span><span class="sxs-lookup"><span data-stu-id="83348-188">Copy the value from the **namespace** textbox.</span></span>

   ![Configure Single Sign-On](./media/tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="83348-190">f.</span><span class="sxs-lookup"><span data-stu-id="83348-190">f.</span></span> <span data-ttu-id="83348-191">To copy the namesapce values for the email and surname follow the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="83348-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="83348-192">g.</span><span class="sxs-lookup"><span data-stu-id="83348-192">g.</span></span> <span data-ttu-id="83348-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span><span class="sxs-lookup"><span data-stu-id="83348-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="83348-194">Email: **mail** or **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="83348-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="83348-195">First name: **givenname**</span><span class="sxs-lookup"><span data-stu-id="83348-195">First name: **givenname**</span></span>
     * <span data-ttu-id="83348-196">Last name: **surname**</span><span class="sxs-lookup"><span data-stu-id="83348-196">Last name: **surname**</span></span>
   
   ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_14.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83348-198">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="83348-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="83348-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83348-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="83348-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="83348-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83348-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="83348-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tableauonline-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="83348-204">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="83348-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/tableauonline-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="83348-206">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="83348-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/tableauonline-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="83348-208">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="83348-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83348-210">a.</span><span class="sxs-lookup"><span data-stu-id="83348-210">a.</span></span> <span data-ttu-id="83348-211">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83348-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83348-212">b.</span><span class="sxs-lookup"><span data-stu-id="83348-212">b.</span></span> <span data-ttu-id="83348-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83348-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83348-214">c.</span><span class="sxs-lookup"><span data-stu-id="83348-214">c.</span></span> <span data-ttu-id="83348-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="83348-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83348-216">d.</span><span class="sxs-lookup"><span data-stu-id="83348-216">d.</span></span> <span data-ttu-id="83348-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="83348-217">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="83348-218">Creating a Tableau Online test user</span><span class="sxs-lookup"><span data-stu-id="83348-218">Creating a Tableau Online test user</span></span>

<span data-ttu-id="83348-219">In this section, you create a user called Britta Simon in Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="83348-219">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="83348-220">On **Tableau Online**, click **Settings** and then **Authentication** section.</span><span class="sxs-lookup"><span data-stu-id="83348-220">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="83348-221">Scroll down to **Select Users** section.</span><span class="sxs-lookup"><span data-stu-id="83348-221">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="83348-222">Click **Add Users** and then **Enter Email Addresses**.</span><span class="sxs-lookup"><span data-stu-id="83348-222">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Creating an Azure AD test user](./media/tableauonline-tutorial/tutorial_tableauonline_15.png)
1. <span data-ttu-id="83348-224">Select **Add users for single sign-on (SSO) authentication**.</span><span class="sxs-lookup"><span data-stu-id="83348-224">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="83348-225">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="83348-225">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Creating an Azure AD test user](./media/tableauonline-tutorial/tutorial_tableauonline_11.png)
1. <span data-ttu-id="83348-227">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="83348-227">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="83348-228">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="83348-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="83348-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="83348-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Assign User][200] 

<span data-ttu-id="83348-231">**To assign Britta Simon to Tableau Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="83348-231">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="83348-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="83348-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="83348-234">In the applications list, select **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="83348-234">In the applications list, select **Tableau Online**.</span></span>

    ![Configure Single Sign-On](./media/tableauonline-tutorial/tutorial_tableauonline_app.png) 

1. <span data-ttu-id="83348-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="83348-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="83348-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="83348-238">Click **Add** button.</span></span> <span data-ttu-id="83348-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="83348-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="83348-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="83348-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="83348-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="83348-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="83348-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="83348-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83348-244">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="83348-244">Testing single sign-on</span></span>

<span data-ttu-id="83348-245">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="83348-245">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="83348-246">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span><span class="sxs-lookup"><span data-stu-id="83348-246">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83348-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="83348-247">Additional resources</span></span>

* [<span data-ttu-id="83348-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83348-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="83348-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83348-249">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/tableauonline-tutorial/tutorial_general_203.png
