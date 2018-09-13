---
title: 'Tutorial: Azure Active Directory integration with EverBridge | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EverBridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 283379131b02f4ea115052f051ef0114efab1997
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865194"
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="dc7f6-103">Tutorial: Azure Active Directory integration with EverBridge</span><span class="sxs-lookup"><span data-stu-id="dc7f6-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="dc7f6-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc7f6-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc7f6-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc7f6-106">You can control in Azure AD who has access to EverBridge</span><span class="sxs-lookup"><span data-stu-id="dc7f6-106">You can control in Azure AD who has access to EverBridge</span></span>
- <span data-ttu-id="dc7f6-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="dc7f6-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc7f6-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dc7f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc7f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dc7f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc7f6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dc7f6-110">Prerequisites</span></span>

<span data-ttu-id="dc7f6-111">To configure Azure AD integration with EverBridge, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-111">To configure Azure AD integration with EverBridge, you need the following items:</span></span>

- <span data-ttu-id="dc7f6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dc7f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc7f6-113">An EverBridge single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dc7f6-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc7f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc7f6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc7f6-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc7f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc7f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc7f6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dc7f6-118">Scenario description</span></span>
<span data-ttu-id="dc7f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc7f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc7f6-121">Adding EverBridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc7f6-121">Adding EverBridge from the gallery</span></span>
1. <span data-ttu-id="dc7f6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc7f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="dc7f6-123">Adding EverBridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc7f6-123">Adding EverBridge from the gallery</span></span>
<span data-ttu-id="dc7f6-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc7f6-125">**To add EverBridge from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc7f6-125">**To add EverBridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc7f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="dc7f6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc7f6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="dc7f6-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="dc7f6-133">In the search box, type **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-133">In the search box, type **EverBridge**.</span></span>

    ![Creating an Azure AD test user](./media/everbridge-tutorial/tutorial_everbridge_search.png)

1. <span data-ttu-id="dc7f6-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc7f6-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc7f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc7f6-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc7f6-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc7f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span></span> <span data-ttu-id="dc7f6-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span></span>

<span data-ttu-id="dc7f6-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc7f6-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc7f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dc7f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dc7f6-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="dc7f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dc7f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc7f6-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc7f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc7f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="dc7f6-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc7f6-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="dc7f6-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="dc7f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_samlbase.png)

1. <span data-ttu-id="dc7f6-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="dc7f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-157">a.</span></span> <span data-ttu-id="dc7f6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="dc7f6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="dc7f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-159">b.</span></span> <span data-ttu-id="dc7f6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="dc7f6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc7f6-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-161">These values are not real.</span></span> <span data-ttu-id="dc7f6-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="dc7f6-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span></span>
 
1. <span data-ttu-id="dc7f6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_certificate.png) 

1. <span data-ttu-id="dc7f6-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="dc7f6-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dc7f6-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="dc7f6-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_configure.png) 

1. <span data-ttu-id="dc7f6-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>

1. <span data-ttu-id="dc7f6-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="dc7f6-174">a.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-174">a.</span></span> <span data-ttu-id="dc7f6-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span><span class="sxs-lookup"><span data-stu-id="dc7f6-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="dc7f6-176">b.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-176">b.</span></span> <span data-ttu-id="dc7f6-177">In the **API Name** textbox, type the name of API.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="dc7f6-178">c.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-178">c.</span></span> <span data-ttu-id="dc7f6-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="dc7f6-180">d.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-180">d.</span></span> <span data-ttu-id="dc7f6-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
   
    <span data-ttu-id="dc7f6-182">e.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-182">e.</span></span> <span data-ttu-id="dc7f6-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="dc7f6-185">f.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-185">f.</span></span> <span data-ttu-id="dc7f6-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="dc7f6-187">g.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-187">g.</span></span> <span data-ttu-id="dc7f6-188">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="dc7f6-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="dc7f6-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="dc7f6-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc7f6-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc7f6-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc7f6-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc7f6-192">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc7f6-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc7f6-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="dc7f6-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc7f6-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc7f6-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="dc7f6-198">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="dc7f6-200">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="dc7f6-202">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc7f6-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc7f6-204">a.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-204">a.</span></span> <span data-ttu-id="dc7f6-205">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc7f6-206">b.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-206">b.</span></span> <span data-ttu-id="dc7f6-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc7f6-208">c.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-208">c.</span></span> <span data-ttu-id="dc7f6-209">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc7f6-210">d.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-210">d.</span></span> <span data-ttu-id="dc7f6-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="dc7f6-212">Creating an EverBridge test user</span><span class="sxs-lookup"><span data-stu-id="dc7f6-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="dc7f6-213">In this section, you create a user called Britta Simon in Everbridge.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="dc7f6-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc7f6-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc7f6-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc7f6-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span></span>

![Assign User][200] 

<span data-ttu-id="dc7f6-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc7f6-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="dc7f6-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="dc7f6-221">In the applications list, select **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-221">In the applications list, select **EverBridge**.</span></span>

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_app.png) 

1. <span data-ttu-id="dc7f6-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="dc7f6-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-225">Click **Add** button.</span></span> <span data-ttu-id="dc7f6-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="dc7f6-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="dc7f6-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="dc7f6-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc7f6-231">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc7f6-231">Testing single sign-on</span></span>

<span data-ttu-id="dc7f6-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc7f6-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span><span class="sxs-lookup"><span data-stu-id="dc7f6-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc7f6-234">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dc7f6-234">Additional resources</span></span>

* [<span data-ttu-id="dc7f6-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc7f6-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dc7f6-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc7f6-236">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/everbridge-tutorial/tutorial_general_01.png
[2]: ./media/everbridge-tutorial/tutorial_general_02.png
[3]: ./media/everbridge-tutorial/tutorial_general_03.png
[4]: ./media/everbridge-tutorial/tutorial_general_04.png

[100]: ./media/everbridge-tutorial/tutorial_general_100.png

[200]: ./media/everbridge-tutorial/tutorial_general_200.png
[201]: ./media/everbridge-tutorial/tutorial_general_201.png
[202]: ./media/everbridge-tutorial/tutorial_general_202.png
[203]: ./media/everbridge-tutorial/tutorial_general_203.png

