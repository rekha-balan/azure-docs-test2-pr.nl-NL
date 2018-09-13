---
title: 'Tutorial: Azure Active Directory integration with Hackerone | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Hackerone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 4e33ad66fe0ced9a426a608f4193ff52dec4f7ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866619"
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="24325-103">Tutorial: Azure Active Directory integration with HackerOne</span><span class="sxs-lookup"><span data-stu-id="24325-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="24325-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24325-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24325-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="24325-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="24325-106">You can control in Azure AD who has access to HackerOne</span><span class="sxs-lookup"><span data-stu-id="24325-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="24325-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="24325-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24325-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="24325-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="24325-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="24325-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24325-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="24325-110">Prerequisites</span></span>

<span data-ttu-id="24325-111">To configure Azure AD integration with HackerOne, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="24325-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="24325-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="24325-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24325-113">A HackerOne single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="24325-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24325-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="24325-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24325-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="24325-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24325-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="24325-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24325-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24325-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24325-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="24325-118">Scenario description</span></span>
<span data-ttu-id="24325-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="24325-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24325-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="24325-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24325-121">Adding HackerOne from the gallery</span><span class="sxs-lookup"><span data-stu-id="24325-121">Adding HackerOne from the gallery</span></span>
1. <span data-ttu-id="24325-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="24325-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="24325-123">Adding HackerOne from the gallery</span><span class="sxs-lookup"><span data-stu-id="24325-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="24325-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="24325-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="24325-125">**To add HackerOne from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24325-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="24325-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="24325-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="24325-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="24325-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="24325-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="24325-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="24325-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="24325-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="24325-133">In the search box, type **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="24325-133">In the search box, type **HackerOne**.</span></span>

    ![Creating an Azure AD test user](./media/hackerone-tutorial/tutorial_hackerone_search.png)

1. <span data-ttu-id="24325-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="24325-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24325-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="24325-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="24325-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="24325-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="24325-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24325-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="24325-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span><span class="sxs-lookup"><span data-stu-id="24325-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="24325-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="24325-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="24325-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="24325-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="24325-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="24325-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="24325-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24325-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="24325-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="24325-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="24325-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="24325-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="24325-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="24325-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24325-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="24325-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24325-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span><span class="sxs-lookup"><span data-stu-id="24325-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="24325-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24325-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="24325-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="24325-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="24325-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="24325-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_samlbase.png)

1. <span data-ttu-id="24325-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24325-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="24325-157">a.</span><span class="sxs-lookup"><span data-stu-id="24325-157">a.</span></span> <span data-ttu-id="24325-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="24325-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="24325-159">b.</span><span class="sxs-lookup"><span data-stu-id="24325-159">b.</span></span> <span data-ttu-id="24325-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="24325-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="24325-161">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="24325-161">This value is not real.</span></span> <span data-ttu-id="24325-162">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="24325-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="24325-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="24325-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
1. <span data-ttu-id="24325-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="24325-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_certificate.png) 

1. <span data-ttu-id="24325-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="24325-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="24325-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="24325-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="24325-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="24325-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_configure.png) 

1. <span data-ttu-id="24325-171">Sign On to your HackerOne tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="24325-171">Sign On to your HackerOne tenant as an administrator.</span></span>

1. <span data-ttu-id="24325-172">In the menu on the top, click the "**Settings**."</span><span class="sxs-lookup"><span data-stu-id="24325-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_001.png) 

1. <span data-ttu-id="24325-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span><span class="sxs-lookup"><span data-stu-id="24325-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_003.png) 

1. <span data-ttu-id="24325-176">On the **SAML Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24325-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="24325-178">a.</span><span class="sxs-lookup"><span data-stu-id="24325-178">a.</span></span> <span data-ttu-id="24325-179">In the **Email Domain** textbox, type a registered domain.</span><span class="sxs-lookup"><span data-stu-id="24325-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="24325-180">b.</span><span class="sxs-lookup"><span data-stu-id="24325-180">b.</span></span> <span data-ttu-id="24325-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="24325-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="24325-182">c.</span><span class="sxs-lookup"><span data-stu-id="24325-182">c.</span></span> <span data-ttu-id="24325-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span><span class="sxs-lookup"><span data-stu-id="24325-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="24325-184">d.</span><span class="sxs-lookup"><span data-stu-id="24325-184">d.</span></span> <span data-ttu-id="24325-185">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="24325-185">Click **Save**.</span></span>

1. <span data-ttu-id="24325-186">On the Authentication Settings dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24325-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="24325-188">a.</span><span class="sxs-lookup"><span data-stu-id="24325-188">a.</span></span> <span data-ttu-id="24325-189">Click **Run test**.</span><span class="sxs-lookup"><span data-stu-id="24325-189">Click **Run test**.</span></span>

    <span data-ttu-id="24325-190">b.</span><span class="sxs-lookup"><span data-stu-id="24325-190">b.</span></span> <span data-ttu-id="24325-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span><span class="sxs-lookup"><span data-stu-id="24325-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="24325-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="24325-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="24325-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="24325-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="24325-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24325-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24325-195">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="24325-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="24325-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24325-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="24325-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24325-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="24325-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="24325-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="24325-201">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="24325-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="24325-203">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="24325-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="24325-205">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24325-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24325-207">a.</span><span class="sxs-lookup"><span data-stu-id="24325-207">a.</span></span> <span data-ttu-id="24325-208">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24325-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24325-209">b.</span><span class="sxs-lookup"><span data-stu-id="24325-209">b.</span></span> <span data-ttu-id="24325-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24325-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24325-211">c.</span><span class="sxs-lookup"><span data-stu-id="24325-211">c.</span></span> <span data-ttu-id="24325-212">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="24325-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="24325-213">d.</span><span class="sxs-lookup"><span data-stu-id="24325-213">d.</span></span> <span data-ttu-id="24325-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="24325-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="24325-215">Creating a HackerOne test user</span><span class="sxs-lookup"><span data-stu-id="24325-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="24325-216">Next, you create a user called Britta Simon in HackerOne.</span><span class="sxs-lookup"><span data-stu-id="24325-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="24325-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="24325-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="24325-218">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="24325-218">There is no action item for you in this section.</span></span> <span data-ttu-id="24325-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="24325-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="24325-220">If you need to create a user manually, you need to contact the Certify support team.</span><span class="sxs-lookup"><span data-stu-id="24325-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="24325-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="24325-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="24325-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span><span class="sxs-lookup"><span data-stu-id="24325-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Assign User][200] 

<span data-ttu-id="24325-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24325-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="24325-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="24325-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="24325-227">In the applications list, select **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="24325-227">In the applications list, select **HackerOne**.</span></span>

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_app.png) 

1. <span data-ttu-id="24325-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="24325-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="24325-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="24325-231">Click **Add** button.</span></span> <span data-ttu-id="24325-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="24325-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="24325-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="24325-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="24325-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="24325-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="24325-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="24325-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24325-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="24325-237">Testing single sign-on</span></span>

<span data-ttu-id="24325-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="24325-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="24325-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span><span class="sxs-lookup"><span data-stu-id="24325-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24325-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="24325-240">Additional resources</span></span>

* [<span data-ttu-id="24325-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24325-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="24325-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24325-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/hackerone-tutorial/tutorial_general_01.png
[2]: ./media/hackerone-tutorial/tutorial_general_02.png
[3]: ./media/hackerone-tutorial/tutorial_general_03.png
[4]: ./media/hackerone-tutorial/tutorial_general_04.png

[100]: ./media/hackerone-tutorial/tutorial_general_100.png

[200]: ./media/hackerone-tutorial/tutorial_general_200.png
[201]: ./media/hackerone-tutorial/tutorial_general_201.png
[202]: ./media/hackerone-tutorial/tutorial_general_202.png
[203]: ./media/hackerone-tutorial/tutorial_general_203.png

