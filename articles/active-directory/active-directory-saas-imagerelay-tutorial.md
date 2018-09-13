---
title: 'Tutorial: Azure Active Directory integration with Image Relay | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Image Relay.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4bf6539fa0a6eab028925372498fbdd17fb05fc2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551821"
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="fe39b-103">Tutorial: Azure Active Directory integration with Image Relay</span><span class="sxs-lookup"><span data-stu-id="fe39b-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>
<span data-ttu-id="fe39b-104">The objective of this tutorial is to show you how to integrate Image Relay with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe39b-104">The objective of this tutorial is to show you how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="fe39b-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fe39b-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="fe39b-106">You can control in Azure AD who has access to Image Relay</span><span class="sxs-lookup"><span data-stu-id="fe39b-106">You can control in Azure AD who has access to Image Relay</span></span>
* <span data-ttu-id="fe39b-107">You can enable your users to automatically get signed-on to Image Relay (single sign-on) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="fe39b-107">You can enable your users to automatically get signed-on to Image Relay (single sign-on) with their Azure AD accounts</span></span>
* <span data-ttu-id="fe39b-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="fe39b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="fe39b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe39b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe39b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe39b-110">Prerequisites</span></span>
<span data-ttu-id="fe39b-111">To configure Azure AD integration with Image Relay, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fe39b-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

* <span data-ttu-id="fe39b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fe39b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="fe39b-113">An Image Relay single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fe39b-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe39b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fe39b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="fe39b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fe39b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="fe39b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="fe39b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="fe39b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe39b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe39b-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="fe39b-118">Scenario Description</span></span>
<span data-ttu-id="fe39b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fe39b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="fe39b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fe39b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe39b-121">Adding Image Relay from the gallery</span><span class="sxs-lookup"><span data-stu-id="fe39b-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="fe39b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fe39b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="fe39b-123">Adding Image Relay from the gallery</span><span class="sxs-lookup"><span data-stu-id="fe39b-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="fe39b-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fe39b-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fe39b-125">**To add Image Relay from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe39b-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fe39b-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="fe39b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="fe39b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="fe39b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fe39b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="fe39b-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="fe39b-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="fe39b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="fe39b-135">In the search box, type **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-135">In the search box, type **Image Relay**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_01.png)
7. <span data-ttu-id="fe39b-137">In the results pane, select **Image Relay**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="fe39b-137">In the results pane, select **Image Relay**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fe39b-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fe39b-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fe39b-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with ImageRelay based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fe39b-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with ImageRelay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe39b-141">For single sign-on to work, Azure AD needs a user account that represents the related user in Image Relay.</span><span class="sxs-lookup"><span data-stu-id="fe39b-141">For single sign-on to work, Azure AD needs a user account that represents the related user in Image Relay.</span></span>  <span data-ttu-id="fe39b-142">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fe39b-142">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>  
<span data-ttu-id="fe39b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Image Relay.</span><span class="sxs-lookup"><span data-stu-id="fe39b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Image Relay.</span></span>

<span data-ttu-id="fe39b-144">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fe39b-144">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fe39b-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fe39b-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fe39b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe39b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe39b-147">**[Creating an Image Relay test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="fe39b-147">**[Creating an Image Relay test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="fe39b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe39b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe39b-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fe39b-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fe39b-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fe39b-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="fe39b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Image Relay application.</span><span class="sxs-lookup"><span data-stu-id="fe39b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="fe39b-152">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe39b-152">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="fe39b-153">In the Azure classic portal, on the **Image Relay** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="fe39b-153">In the Azure classic portal, on the **Image Relay** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>
   
     ![Configure Single Sign-On][6] 
2. <span data-ttu-id="fe39b-155">On the **How would you like users to sign on to Image Relay** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-155">On the **How would you like users to sign on to Image Relay** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_03.png) 
3. <span data-ttu-id="fe39b-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe39b-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_04.png) 
   
    <span data-ttu-id="fe39b-159">a.</span><span class="sxs-lookup"><span data-stu-id="fe39b-159">a.</span></span> <span data-ttu-id="fe39b-160">In the **Sign On URL** textbox, type the URL used by your users to sign on to your ImageRelay application (for example: *https://fabrikam.ImageRelay.com/*).</span><span class="sxs-lookup"><span data-stu-id="fe39b-160">In the **Sign On URL** textbox, type the URL used by your users to sign on to your ImageRelay application (for example: *https://fabrikam.ImageRelay.com/*).</span></span>
   
    <span data-ttu-id="fe39b-161">b.</span><span class="sxs-lookup"><span data-stu-id="fe39b-161">b.</span></span> <span data-ttu-id="fe39b-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-162">Click **Next**.</span></span>
4. <span data-ttu-id="fe39b-163">On the **Configure single sign-on at Image Relay** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe39b-163">On the **Configure single sign-on at Image Relay** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_05.png) 
   
    <span data-ttu-id="fe39b-165">a.</span><span class="sxs-lookup"><span data-stu-id="fe39b-165">a.</span></span> <span data-ttu-id="fe39b-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="fe39b-166">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="fe39b-167">b.</span><span class="sxs-lookup"><span data-stu-id="fe39b-167">b.</span></span> <span data-ttu-id="fe39b-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-168">Click **Next**.</span></span>
5. <span data-ttu-id="fe39b-169">In another browser window, sign in to your Image Relay company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fe39b-169">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>
6. <span data-ttu-id="fe39b-170">In the toolbar on the top, click the **Users & Permissions** workload.</span><span class="sxs-lookup"><span data-stu-id="fe39b-170">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 
7. <span data-ttu-id="fe39b-172">Click **Create New Permission**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-172">Click **Create New Permission**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png) 
8. <span data-ttu-id="fe39b-174">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-174">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 
9. <span data-ttu-id="fe39b-176">Go to **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-176">Go to **Account Settings**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 
10. <span data-ttu-id="fe39b-178">Go to the **Single Sign On Settings** workload.</span><span class="sxs-lookup"><span data-stu-id="fe39b-178">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)
11. <span data-ttu-id="fe39b-180">On the **SAML Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe39b-180">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="fe39b-182">a.</span><span class="sxs-lookup"><span data-stu-id="fe39b-182">a.</span></span> <span data-ttu-id="fe39b-183">In the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="fe39b-183">In the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the **Login URL** textbox.</span></span>

    <span data-ttu-id="fe39b-184">b.</span><span class="sxs-lookup"><span data-stu-id="fe39b-184">b.</span></span> <span data-ttu-id="fe39b-185">In the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="fe39b-185">In the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="fe39b-186">c.</span><span class="sxs-lookup"><span data-stu-id="fe39b-186">c.</span></span> <span data-ttu-id="fe39b-187">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-187">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="fe39b-188">d.</span><span class="sxs-lookup"><span data-stu-id="fe39b-188">d.</span></span> <span data-ttu-id="fe39b-189">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-189">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="fe39b-190">e.</span><span class="sxs-lookup"><span data-stu-id="fe39b-190">e.</span></span> <span data-ttu-id="fe39b-191">Under **x.509 Certificate**, click **Update Certificate**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-191">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="fe39b-193">f.</span><span class="sxs-lookup"><span data-stu-id="fe39b-193">f.</span></span> <span data-ttu-id="fe39b-194">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span><span class="sxs-lookup"><span data-stu-id="fe39b-194">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="fe39b-196">g.</span><span class="sxs-lookup"><span data-stu-id="fe39b-196">g.</span></span> <span data-ttu-id="fe39b-197">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-197">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="fe39b-199">h.</span><span class="sxs-lookup"><span data-stu-id="fe39b-199">h.</span></span> <span data-ttu-id="fe39b-200">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe39b-200">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="fe39b-202">i.</span><span class="sxs-lookup"><span data-stu-id="fe39b-202">i.</span></span> <span data-ttu-id="fe39b-203">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-203">Click **Save**.</span></span>

1. <span data-ttu-id="fe39b-204">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-204">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
2. <span data-ttu-id="fe39b-206">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-206">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fe39b-208">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fe39b-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="fe39b-209">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe39b-209">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="fe39b-211">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe39b-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fe39b-212">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-212">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="fe39b-214">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="fe39b-214">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="fe39b-215">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-215">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="fe39b-217">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-217">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="fe39b-219">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe39b-219">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="fe39b-221">a.</span><span class="sxs-lookup"><span data-stu-id="fe39b-221">a.</span></span> <span data-ttu-id="fe39b-222">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="fe39b-222">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="fe39b-223">b.</span><span class="sxs-lookup"><span data-stu-id="fe39b-223">b.</span></span> <span data-ttu-id="fe39b-224">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-224">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="fe39b-225">c.</span><span class="sxs-lookup"><span data-stu-id="fe39b-225">c.</span></span> <span data-ttu-id="fe39b-226">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-226">Click **Next**.</span></span>
6. <span data-ttu-id="fe39b-227">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe39b-227">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="fe39b-229">a.</span><span class="sxs-lookup"><span data-stu-id="fe39b-229">a.</span></span> <span data-ttu-id="fe39b-230">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-230">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="fe39b-231">b.</span><span class="sxs-lookup"><span data-stu-id="fe39b-231">b.</span></span> <span data-ttu-id="fe39b-232">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-232">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="fe39b-233">c.</span><span class="sxs-lookup"><span data-stu-id="fe39b-233">c.</span></span> <span data-ttu-id="fe39b-234">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-234">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="fe39b-235">d.</span><span class="sxs-lookup"><span data-stu-id="fe39b-235">d.</span></span> <span data-ttu-id="fe39b-236">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-236">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="fe39b-237">e.</span><span class="sxs-lookup"><span data-stu-id="fe39b-237">e.</span></span> <span data-ttu-id="fe39b-238">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-238">Click **Next**.</span></span>

7. <span data-ttu-id="fe39b-239">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-239">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="fe39b-241">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe39b-241">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="fe39b-243">a.</span><span class="sxs-lookup"><span data-stu-id="fe39b-243">a.</span></span> <span data-ttu-id="fe39b-244">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-244">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="fe39b-245">b.</span><span class="sxs-lookup"><span data-stu-id="fe39b-245">b.</span></span> <span data-ttu-id="fe39b-246">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-246">Click **Complete**.</span></span>   

### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="fe39b-247">Creating an Image Relay test user</span><span class="sxs-lookup"><span data-stu-id="fe39b-247">Creating an Image Relay test user</span></span>
<span data-ttu-id="fe39b-248">The objective of this section is to create a user called Britta Simon in Image Relay.</span><span class="sxs-lookup"><span data-stu-id="fe39b-248">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="fe39b-249">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe39b-249">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="fe39b-250">Sign-on to your Image Relay company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fe39b-250">Sign-on to your Image Relay company site as an administrator.</span></span>
2. <span data-ttu-id="fe39b-251">Go to **Users & Permissions**     and select **Create SSO User**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-251">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 
3. <span data-ttu-id="fe39b-253">Enter the **Email**, **First Name**, **Last Name** and **Company** of the user you want to provision and select the permission group (for example, SSO Basic ) which is the group that can sign in only through single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe39b-253">Enter the **Email**, **First Name**, **Last Name** and **Company** of the user you want to provision and select the permission group (for example, SSO Basic ) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 
4. <span data-ttu-id="fe39b-255">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-255">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fe39b-256">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fe39b-256">Assigning the Azure AD test user</span></span>
<span data-ttu-id="fe39b-257">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Image Relay.</span><span class="sxs-lookup"><span data-stu-id="fe39b-257">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Image Relay.</span></span>

![Assign User][200] 

<span data-ttu-id="fe39b-259">**To assign Britta Simon to Image Relay, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe39b-259">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="fe39b-260">In the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fe39b-260">In the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="fe39b-262">In the applications list, select **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-262">In the applications list, select **Image Relay**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_23.png) 
3. <span data-ttu-id="fe39b-264">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-264">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="fe39b-266">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-266">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="fe39b-267">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="fe39b-267">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="fe39b-269">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fe39b-269">Testing Single Sign-On</span></span>
<span data-ttu-id="fe39b-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fe39b-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="fe39b-271">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span><span class="sxs-lookup"><span data-stu-id="fe39b-271">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe39b-272">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="fe39b-272">Additional Resources</span></span>
* [<span data-ttu-id="fe39b-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe39b-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe39b-274">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fe39b-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-imagerelay-tutorial/tutorial_general_205.png





































