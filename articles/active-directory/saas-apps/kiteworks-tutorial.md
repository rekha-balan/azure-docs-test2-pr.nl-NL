---
title: 'Tutorial: Azure Active Directory integration with Kiteworks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kiteworks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 88531ee1a98eefdf3ee85b4308150f10417858d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857861"
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="cd367-103">Tutorial: Azure Active Directory integration with Kiteworks</span><span class="sxs-lookup"><span data-stu-id="cd367-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="cd367-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd367-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd367-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cd367-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cd367-106">You can control in Azure AD who has access to Kiteworks</span><span class="sxs-lookup"><span data-stu-id="cd367-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="cd367-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cd367-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd367-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cd367-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cd367-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cd367-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd367-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd367-110">Prerequisites</span></span>

<span data-ttu-id="cd367-111">To configure Azure AD integration with Kiteworks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cd367-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="cd367-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cd367-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd367-113">A Kiteworks single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cd367-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd367-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cd367-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd367-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cd367-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd367-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cd367-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd367-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd367-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd367-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cd367-118">Scenario description</span></span>
<span data-ttu-id="cd367-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cd367-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd367-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cd367-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd367-121">Adding Kiteworks from the gallery</span><span class="sxs-lookup"><span data-stu-id="cd367-121">Adding Kiteworks from the gallery</span></span>
1. <span data-ttu-id="cd367-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cd367-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="cd367-123">Adding Kiteworks from the gallery</span><span class="sxs-lookup"><span data-stu-id="cd367-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="cd367-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cd367-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cd367-125">**To add Kiteworks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cd367-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cd367-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cd367-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cd367-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cd367-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cd367-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cd367-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cd367-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cd367-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cd367-133">In the search box, type **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="cd367-133">In the search box, type **Kiteworks**.</span></span>

    ![Creating an Azure AD test user](./media/kiteworks-tutorial/tutorial_kiteworks_search.png)

1. <span data-ttu-id="cd367-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cd367-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd367-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cd367-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd367-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cd367-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd367-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd367-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="cd367-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cd367-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="cd367-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cd367-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cd367-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cd367-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cd367-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cd367-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cd367-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd367-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cd367-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cd367-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cd367-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cd367-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cd367-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cd367-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd367-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cd367-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd367-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span><span class="sxs-lookup"><span data-stu-id="cd367-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="cd367-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cd367-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="cd367-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cd367-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cd367-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cd367-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

1. <span data-ttu-id="cd367-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cd367-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="cd367-157">a.</span><span class="sxs-lookup"><span data-stu-id="cd367-157">a.</span></span> <span data-ttu-id="cd367-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="cd367-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="cd367-159">b.</span><span class="sxs-lookup"><span data-stu-id="cd367-159">b.</span></span> <span data-ttu-id="cd367-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="cd367-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd367-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="cd367-161">These values are not real.</span></span> <span data-ttu-id="cd367-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="cd367-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cd367-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="cd367-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
1. <span data-ttu-id="cd367-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cd367-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

1. <span data-ttu-id="cd367-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cd367-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cd367-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cd367-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cd367-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="cd367-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_configure.png) 

1. <span data-ttu-id="cd367-171">Sign on to your Kiteworks company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cd367-171">Sign on to your Kiteworks company site as an administrator.</span></span>

1. <span data-ttu-id="cd367-172">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="cd367-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_06.png) 

1. <span data-ttu-id="cd367-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span><span class="sxs-lookup"><span data-stu-id="cd367-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_07.png)
 
1. <span data-ttu-id="cd367-176">On the SSO Setup page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cd367-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="cd367-178">a.</span><span class="sxs-lookup"><span data-stu-id="cd367-178">a.</span></span> <span data-ttu-id="cd367-179">Select **Authenticate via SSO**.</span><span class="sxs-lookup"><span data-stu-id="cd367-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="cd367-180">b.</span><span class="sxs-lookup"><span data-stu-id="cd367-180">b.</span></span> <span data-ttu-id="cd367-181">Select **Initiate AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="cd367-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="cd367-182">c.</span><span class="sxs-lookup"><span data-stu-id="cd367-182">c.</span></span> <span data-ttu-id="cd367-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd367-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="cd367-184">d.</span><span class="sxs-lookup"><span data-stu-id="cd367-184">d.</span></span> <span data-ttu-id="cd367-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd367-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cd367-186">e.</span><span class="sxs-lookup"><span data-stu-id="cd367-186">e.</span></span> <span data-ttu-id="cd367-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd367-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cd367-188">f.</span><span class="sxs-lookup"><span data-stu-id="cd367-188">f.</span></span> <span data-ttu-id="cd367-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="cd367-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="cd367-190">g.</span><span class="sxs-lookup"><span data-stu-id="cd367-190">g.</span></span> <span data-ttu-id="cd367-191">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cd367-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cd367-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cd367-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cd367-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cd367-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cd367-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd367-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd367-195">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cd367-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd367-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd367-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cd367-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cd367-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cd367-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cd367-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kiteworks-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cd367-201">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cd367-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kiteworks-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cd367-203">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cd367-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kiteworks-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cd367-205">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cd367-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd367-207">a.</span><span class="sxs-lookup"><span data-stu-id="cd367-207">a.</span></span> <span data-ttu-id="cd367-208">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd367-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd367-209">b.</span><span class="sxs-lookup"><span data-stu-id="cd367-209">b.</span></span> <span data-ttu-id="cd367-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cd367-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd367-211">c.</span><span class="sxs-lookup"><span data-stu-id="cd367-211">c.</span></span> <span data-ttu-id="cd367-212">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cd367-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cd367-213">d.</span><span class="sxs-lookup"><span data-stu-id="cd367-213">d.</span></span> <span data-ttu-id="cd367-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cd367-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="cd367-215">Creating a Kiteworks test user</span><span class="sxs-lookup"><span data-stu-id="cd367-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="cd367-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="cd367-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="cd367-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="cd367-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="cd367-218">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="cd367-218">There is no action item for you in this section.</span></span> <span data-ttu-id="cd367-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="cd367-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="cd367-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="cd367-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cd367-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cd367-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cd367-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="cd367-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Assign User][200] 

<span data-ttu-id="cd367-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cd367-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="cd367-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cd367-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cd367-227">In the applications list, select **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="cd367-227">In the applications list, select **Kiteworks**.</span></span>

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_app.png) 

1. <span data-ttu-id="cd367-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cd367-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cd367-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cd367-231">Click **Add** button.</span></span> <span data-ttu-id="cd367-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cd367-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cd367-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cd367-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cd367-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cd367-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cd367-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cd367-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd367-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cd367-237">Testing single sign-on</span></span>

<span data-ttu-id="cd367-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cd367-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="cd367-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span><span class="sxs-lookup"><span data-stu-id="cd367-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd367-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cd367-240">Additional resources</span></span>

* [<span data-ttu-id="cd367-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd367-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cd367-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd367-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/kiteworks-tutorial/tutorial_general_203.png

