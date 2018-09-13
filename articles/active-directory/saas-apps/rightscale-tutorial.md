---
title: 'Tutorial: Azure Active Directory integration with Rightscale | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Rightscale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 6d251400baed6b15d96eb7a2ef64d4217631613b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871060"
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="4c9da-103">Tutorial: Azure Active Directory integration with Rightscale</span><span class="sxs-lookup"><span data-stu-id="4c9da-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="4c9da-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c9da-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c9da-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4c9da-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c9da-106">You can control in Azure AD who has access to Rightscale</span><span class="sxs-lookup"><span data-stu-id="4c9da-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="4c9da-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4c9da-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c9da-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4c9da-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c9da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4c9da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c9da-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4c9da-110">Prerequisites</span></span>

<span data-ttu-id="4c9da-111">To configure Azure AD integration with Rightscale, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4c9da-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="4c9da-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4c9da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c9da-113">A Rightscale single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4c9da-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c9da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4c9da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c9da-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4c9da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c9da-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4c9da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c9da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c9da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c9da-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4c9da-118">Scenario description</span></span>
<span data-ttu-id="4c9da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4c9da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c9da-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4c9da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c9da-121">Adding Rightscale from the gallery</span><span class="sxs-lookup"><span data-stu-id="4c9da-121">Adding Rightscale from the gallery</span></span>
1. <span data-ttu-id="4c9da-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c9da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="4c9da-123">Adding Rightscale from the gallery</span><span class="sxs-lookup"><span data-stu-id="4c9da-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="4c9da-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4c9da-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c9da-125">**To add Rightscale from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c9da-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4c9da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4c9da-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c9da-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4c9da-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4c9da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4c9da-133">In the search box, type **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-133">In the search box, type **Rightscale**.</span></span>

    ![Creating an Azure AD test user](./media/rightscale-tutorial/tutorial_rightscale_search.png)

1. <span data-ttu-id="4c9da-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4c9da-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c9da-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c9da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c9da-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c9da-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c9da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c9da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="4c9da-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4c9da-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="4c9da-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4c9da-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c9da-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4c9da-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c9da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4c9da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4c9da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c9da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4c9da-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4c9da-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4c9da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c9da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4c9da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4c9da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c9da-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c9da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c9da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span><span class="sxs-lookup"><span data-stu-id="4c9da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="4c9da-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c9da-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9da-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4c9da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c9da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_samlbase.png)

1. <span data-ttu-id="4c9da-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9da-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_url.png)

1. <span data-ttu-id="4c9da-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c9da-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="4c9da-159">a.</span><span class="sxs-lookup"><span data-stu-id="4c9da-159">a.</span></span> <span data-ttu-id="4c9da-160">Click on the **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="4c9da-161">b.</span><span class="sxs-lookup"><span data-stu-id="4c9da-161">b.</span></span> <span data-ttu-id="4c9da-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="4c9da-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

1. <span data-ttu-id="4c9da-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4c9da-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_certificate.png) 

1. <span data-ttu-id="4c9da-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4c9da-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4c9da-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4c9da-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c9da-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4c9da-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="4c9da-169">![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="4c9da-169">![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
1. <span data-ttu-id="4c9da-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4c9da-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="4c9da-171">a.</span><span class="sxs-lookup"><span data-stu-id="4c9da-171">a.</span></span> <span data-ttu-id="4c9da-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="4c9da-174">b.</span><span class="sxs-lookup"><span data-stu-id="4c9da-174">b.</span></span> <span data-ttu-id="4c9da-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="4c9da-177">c.</span><span class="sxs-lookup"><span data-stu-id="4c9da-177">c.</span></span> <span data-ttu-id="4c9da-178">In the textbox of **Display Name**, input your company name.</span><span class="sxs-lookup"><span data-stu-id="4c9da-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="4c9da-180">d.</span><span class="sxs-lookup"><span data-stu-id="4c9da-180">d.</span></span> <span data-ttu-id="4c9da-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span><span class="sxs-lookup"><span data-stu-id="4c9da-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="4c9da-183">e.</span><span class="sxs-lookup"><span data-stu-id="4c9da-183">e.</span></span> <span data-ttu-id="4c9da-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="4c9da-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="4c9da-186">f.</span><span class="sxs-lookup"><span data-stu-id="4c9da-186">f.</span></span> <span data-ttu-id="4c9da-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="4c9da-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="4c9da-189">g.</span><span class="sxs-lookup"><span data-stu-id="4c9da-189">g.</span></span> <span data-ttu-id="4c9da-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4c9da-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="4c9da-192">h.</span><span class="sxs-lookup"><span data-stu-id="4c9da-192">h.</span></span> <span data-ttu-id="4c9da-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="4c9da-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4c9da-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c9da-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4c9da-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c9da-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c9da-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c9da-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4c9da-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c9da-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c9da-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4c9da-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c9da-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9da-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4c9da-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/rightscale-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4c9da-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/rightscale-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4c9da-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4c9da-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/rightscale-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4c9da-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c9da-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c9da-209">a.</span><span class="sxs-lookup"><span data-stu-id="4c9da-209">a.</span></span> <span data-ttu-id="4c9da-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c9da-211">b.</span><span class="sxs-lookup"><span data-stu-id="4c9da-211">b.</span></span> <span data-ttu-id="4c9da-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c9da-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c9da-213">c.</span><span class="sxs-lookup"><span data-stu-id="4c9da-213">c.</span></span> <span data-ttu-id="4c9da-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c9da-215">d.</span><span class="sxs-lookup"><span data-stu-id="4c9da-215">d.</span></span> <span data-ttu-id="4c9da-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="4c9da-217">Creating a Rightscale test user</span><span class="sxs-lookup"><span data-stu-id="4c9da-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="4c9da-218">In this section, you create a user called Britta Simon in RightScale.</span><span class="sxs-lookup"><span data-stu-id="4c9da-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="4c9da-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span><span class="sxs-lookup"><span data-stu-id="4c9da-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c9da-220">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4c9da-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c9da-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span><span class="sxs-lookup"><span data-stu-id="4c9da-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![Assign User][200] 

<span data-ttu-id="4c9da-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c9da-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9da-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4c9da-226">In the applications list, select **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-226">In the applications list, select **Rightscale**.</span></span>

    ![Configure Single Sign-On](./media/rightscale-tutorial/tutorial_rightscale_app.png) 

1. <span data-ttu-id="4c9da-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4c9da-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4c9da-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4c9da-230">Click **Add** button.</span></span> <span data-ttu-id="4c9da-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c9da-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4c9da-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4c9da-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4c9da-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c9da-234">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4c9da-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c9da-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c9da-236">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c9da-236">Testing single sign-on</span></span>

<span data-ttu-id="4c9da-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4c9da-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="4c9da-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span><span class="sxs-lookup"><span data-stu-id="4c9da-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c9da-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4c9da-239">Additional resources</span></span>

* [<span data-ttu-id="4c9da-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c9da-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4c9da-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c9da-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/rightscale-tutorial/tutorial_general_01.png
[2]: ./media/rightscale-tutorial/tutorial_general_02.png
[3]: ./media/rightscale-tutorial/tutorial_general_03.png
[4]: ./media/rightscale-tutorial/tutorial_general_04.png

[100]: ./media/rightscale-tutorial/tutorial_general_100.png

[200]: ./media/rightscale-tutorial/tutorial_general_200.png
[201]: ./media/rightscale-tutorial/tutorial_general_201.png
[202]: ./media/rightscale-tutorial/tutorial_general_202.png
[203]: ./media/rightscale-tutorial/tutorial_general_203.png

