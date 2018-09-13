---
title: 'Tutorial: Azure Active Directory integration with Sprinklr | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: e2dc9b7e7cf5964c36b21418a0162c1c2ef92dc8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858072"
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="4dfb3-103">Tutorial: Azure Active Directory integration with Sprinklr</span><span class="sxs-lookup"><span data-stu-id="4dfb3-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="4dfb3-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4dfb3-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dfb3-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4dfb3-106">You can control in Azure AD who has access to Sprinklr</span><span class="sxs-lookup"><span data-stu-id="4dfb3-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="4dfb3-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4dfb3-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4dfb3-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4dfb3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4dfb3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4dfb3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dfb3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4dfb3-110">Prerequisites</span></span>

<span data-ttu-id="4dfb3-111">To configure Azure AD integration with Sprinklr, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="4dfb3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4dfb3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4dfb3-113">A Sprinklr single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4dfb3-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4dfb3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4dfb3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4dfb3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4dfb3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dfb3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dfb3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4dfb3-118">Scenario description</span></span>
<span data-ttu-id="4dfb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4dfb3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dfb3-121">Adding Sprinklr from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dfb3-121">Adding Sprinklr from the gallery</span></span>
1. <span data-ttu-id="4dfb3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dfb3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="4dfb3-123">Adding Sprinklr from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dfb3-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="4dfb3-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4dfb3-125">**To add Sprinklr from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dfb3-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfb3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4dfb3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4dfb3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4dfb3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4dfb3-133">In the search box, type **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-133">In the search box, type **Sprinklr**.</span></span>

    ![Creating an Azure AD test user](./media/sprinklr-tutorial/tutorial_sprinklr_search.png)

1. <span data-ttu-id="4dfb3-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4dfb3-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dfb3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4dfb3-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4dfb3-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4dfb3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="4dfb3-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="4dfb3-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4dfb3-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4dfb3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4dfb3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4dfb3-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4dfb3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4dfb3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4dfb3-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dfb3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4dfb3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="4dfb3-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dfb3-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfb3-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4dfb3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

1. <span data-ttu-id="4dfb3-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="4dfb3-157">a.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-157">a.</span></span> <span data-ttu-id="4dfb3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="4dfb3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="4dfb3-159">b.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-159">b.</span></span> <span data-ttu-id="4dfb3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="4dfb3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dfb3-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-161">These values are not real.</span></span> <span data-ttu-id="4dfb3-162">Update the value with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4dfb3-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
1. <span data-ttu-id="4dfb3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

1. <span data-ttu-id="4dfb3-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sprinklr-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4dfb3-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4dfb3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4dfb3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

1. <span data-ttu-id="4dfb3-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

1. <span data-ttu-id="4dfb3-171">Go to **Administration \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="4dfb3-172">![Administration](./media/sprinklr-tutorial/ic782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-172">![Administration](./media/sprinklr-tutorial/ic782907.png "Administration")</span></span>

1. <span data-ttu-id="4dfb3-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="4dfb3-174">![Manage Partner](./media/sprinklr-tutorial/ic782908.png "Manage Partner")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-174">![Manage Partner](./media/sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

1. <span data-ttu-id="4dfb3-175">Click **+Add Single Sign Ons**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="4dfb3-176">![Single Sign-Ons](./media/sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-176">![Single Sign-Ons](./media/sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

1. <span data-ttu-id="4dfb3-177">On the **Single Sign on** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4dfb3-178">![Single Sign-Ons](./media/sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-178">![Single Sign-Ons](./media/sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="4dfb3-179">a.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-179">a.</span></span> <span data-ttu-id="4dfb3-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="4dfb3-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="4dfb3-181">b.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-181">b.</span></span> <span data-ttu-id="4dfb3-182">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-182">Select **Enabled**.</span></span>

    <span data-ttu-id="4dfb3-183">c.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-183">c.</span></span> <span data-ttu-id="4dfb3-184">Select **Use new SSO Certificate**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="4dfb3-185">e.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-185">e.</span></span> <span data-ttu-id="4dfb3-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="4dfb3-187">f.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-187">f.</span></span> <span data-ttu-id="4dfb3-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="4dfb3-189">g.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-189">g.</span></span> <span data-ttu-id="4dfb3-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="4dfb3-191">h.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-191">h.</span></span> <span data-ttu-id="4dfb3-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="4dfb3-193">i.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-193">i.</span></span> <span data-ttu-id="4dfb3-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="4dfb3-195">j.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-195">j.</span></span> <span data-ttu-id="4dfb3-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="4dfb3-197">k.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-197">k.</span></span> <span data-ttu-id="4dfb3-198">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-198">Click **Save**.</span></span>
       
    <span data-ttu-id="4dfb3-199">![SAML](./media/sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-199">![SAML](./media/sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="4dfb3-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4dfb3-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4dfb3-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4dfb3-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4dfb3-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4dfb3-203">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dfb3-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="4dfb3-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4dfb3-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dfb3-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfb3-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sprinklr-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4dfb3-209">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sprinklr-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4dfb3-211">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sprinklr-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4dfb3-213">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4dfb3-215">a.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-215">a.</span></span> <span data-ttu-id="4dfb3-216">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4dfb3-217">b.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-217">b.</span></span> <span data-ttu-id="4dfb3-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4dfb3-219">c.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-219">c.</span></span> <span data-ttu-id="4dfb3-220">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4dfb3-221">d.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-221">d.</span></span> <span data-ttu-id="4dfb3-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="4dfb3-223">Creating a Sprinklr test user</span><span class="sxs-lookup"><span data-stu-id="4dfb3-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="4dfb3-224">Log in to your Sprinklr company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-224">Log in to your Sprinklr company site as an administrator.</span></span>

1. <span data-ttu-id="4dfb3-225">Go to **Administration \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="4dfb3-226">![Administration](./media/sprinklr-tutorial/ic782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-226">![Administration](./media/sprinklr-tutorial/ic782907.png "Administration")</span></span>

1. <span data-ttu-id="4dfb3-227">Go to **Manage Client \> Users** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="4dfb3-228">![Settings](./media/sprinklr-tutorial/ic782914.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-228">![Settings](./media/sprinklr-tutorial/ic782914.png "Settings")</span></span>

1. <span data-ttu-id="4dfb3-229">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="4dfb3-230">![Settings](./media/sprinklr-tutorial/ic782915.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-230">![Settings](./media/sprinklr-tutorial/ic782915.png "Settings")</span></span>

1. <span data-ttu-id="4dfb3-231">On the **Edit user** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="4dfb3-232">![Edit user](./media/sprinklr-tutorial/ic782916.png "Edit user")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-232">![Edit user](./media/sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="4dfb3-233">a.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-233">a.</span></span> <span data-ttu-id="4dfb3-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="4dfb3-235">b.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-235">b.</span></span> <span data-ttu-id="4dfb3-236">Select **Password Disabled**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="4dfb3-237">c.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-237">c.</span></span> <span data-ttu-id="4dfb3-238">Select **Language**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-238">Select **Language**.</span></span>

    <span data-ttu-id="4dfb3-239">d.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-239">d.</span></span> <span data-ttu-id="4dfb3-240">Select **User Type**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-240">Select **User Type**.</span></span>

    <span data-ttu-id="4dfb3-241">e.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-241">e.</span></span> <span data-ttu-id="4dfb3-242">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="4dfb3-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
1. <span data-ttu-id="4dfb3-244">Go to **Role**, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dfb3-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="4dfb3-245">![Partner Roles](./media/sprinklr-tutorial/ic782917.png "Partner Roles")</span><span class="sxs-lookup"><span data-stu-id="4dfb3-245">![Partner Roles](./media/sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="4dfb3-246">a.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-246">a.</span></span> <span data-ttu-id="4dfb3-247">From the **Global** list, select **ALL\_Permissions**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="4dfb3-248">b.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-248">b.</span></span> <span data-ttu-id="4dfb3-249">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="4dfb3-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4dfb3-251">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dfb3-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4dfb3-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Assign User][200] 

<span data-ttu-id="4dfb3-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dfb3-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfb3-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4dfb3-257">In the applications list, select **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-257">In the applications list, select **Sprinklr**.</span></span>

    ![Configure Single Sign-On](./media/sprinklr-tutorial/tutorial_sprinklr_app.png) 

1. <span data-ttu-id="4dfb3-259">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4dfb3-261">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-261">Click **Add** button.</span></span> <span data-ttu-id="4dfb3-262">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4dfb3-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4dfb3-265">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-265">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4dfb3-266">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4dfb3-267">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dfb3-267">Testing single sign-on</span></span>

<span data-ttu-id="4dfb3-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4dfb3-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4dfb3-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4dfb3-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4dfb3-270">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4dfb3-270">Additional resources</span></span>

* [<span data-ttu-id="4dfb3-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dfb3-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4dfb3-272">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dfb3-272">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/sprinklr-tutorial/tutorial_general_203.png

