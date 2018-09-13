---
title: 'Tutorial: Azure Active Directory integration with LockPath Keylight | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LockPath Keylight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 18fbcc785491ca8a0631f54750412bc0f12254c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857057"
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="6e9ca-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="6e9ca-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="6e9ca-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e9ca-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e9ca-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e9ca-106">You can control in Azure AD who has access to LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="6e9ca-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="6e9ca-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6e9ca-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e9ca-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e9ca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e9ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6e9ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e9ca-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6e9ca-110">Prerequisites</span></span>

<span data-ttu-id="6e9ca-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="6e9ca-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6e9ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e9ca-113">A LockPath Keylight single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6e9ca-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e9ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e9ca-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e9ca-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e9ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e9ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e9ca-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6e9ca-118">Scenario description</span></span>
<span data-ttu-id="6e9ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e9ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e9ca-121">Adding LockPath Keylight from the gallery</span><span class="sxs-lookup"><span data-stu-id="6e9ca-121">Adding LockPath Keylight from the gallery</span></span>
1. <span data-ttu-id="6e9ca-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e9ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="6e9ca-123">Adding LockPath Keylight from the gallery</span><span class="sxs-lookup"><span data-stu-id="6e9ca-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="6e9ca-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e9ca-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e9ca-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e9ca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="6e9ca-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e9ca-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="6e9ca-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="6e9ca-133">In the search box, type **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Creating an Azure AD test user](./media/keylight-tutorial/tutorial_keylight_search.png)

1. <span data-ttu-id="6e9ca-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e9ca-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e9ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e9ca-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6e9ca-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e9ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="6e9ca-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="6e9ca-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6e9ca-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e9ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6e9ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6e9ca-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6e9ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6e9ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e9ca-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e9ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e9ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="6e9ca-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e9ca-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="6e9ca-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="6e9ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/keylight-tutorial/tutorial_keylight_samlbase.png)

1. <span data-ttu-id="6e9ca-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span><span class="sxs-lookup"><span data-stu-id="6e9ca-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Configure Single Sign-On](./media/keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="6e9ca-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-157">a.</span></span> <span data-ttu-id="6e9ca-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="6e9ca-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="6e9ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-159">b.</span></span> <span data-ttu-id="6e9ca-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="6e9ca-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="6e9ca-161">c.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-161">c.</span></span> <span data-ttu-id="6e9ca-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="6e9ca-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="6e9ca-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-163">These values are not real.</span></span> <span data-ttu-id="6e9ca-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6e9ca-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

1. <span data-ttu-id="6e9ca-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/keylight-tutorial/tutorial_keylight_certificate.png) 

1. <span data-ttu-id="6e9ca-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/keylight-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="6e9ca-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e9ca-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="6e9ca-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/keylight-tutorial/tutorial_keylight_configure.png) 

1. <span data-ttu-id="6e9ca-173">To enable SSO in LockPath Keylight, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="6e9ca-174">a.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-174">a.</span></span> <span data-ttu-id="6e9ca-175">Sign-on to your LockPath Keylight account as administrator.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="6e9ca-176">b.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-176">b.</span></span> <span data-ttu-id="6e9ca-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configure Single Sign-On](./media/keylight-tutorial/401.png) 

    <span data-ttu-id="6e9ca-179">c.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-179">c.</span></span> <span data-ttu-id="6e9ca-180">In the treeview on the left, click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Configure Single Sign-On](./media/keylight-tutorial/402.png) 

    <span data-ttu-id="6e9ca-182">d.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-182">d.</span></span> <span data-ttu-id="6e9ca-183">On the **SAML Settings** dialog, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configure Single Sign-On](./media/keylight-tutorial/404.png) 

1. <span data-ttu-id="6e9ca-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/keylight-tutorial/405.png) 
   
    <span data-ttu-id="6e9ca-187">a.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-187">a.</span></span> <span data-ttu-id="6e9ca-188">Set **SAML authentication** to **Active**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="6e9ca-189">b.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-189">b.</span></span> <span data-ttu-id="6e9ca-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="6e9ca-191">c.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-191">c.</span></span> <span data-ttu-id="6e9ca-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="6e9ca-193">d.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-193">d.</span></span> <span data-ttu-id="6e9ca-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="6e9ca-195">e.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-195">e.</span></span> <span data-ttu-id="6e9ca-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="6e9ca-197">f.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-197">f.</span></span> <span data-ttu-id="6e9ca-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="6e9ca-199">g.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-199">g.</span></span> <span data-ttu-id="6e9ca-200">Set **Auto-provision users** to **Active**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="6e9ca-201">h.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-201">h.</span></span> <span data-ttu-id="6e9ca-202">Set **Auto-provision account type** to **Full User**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="6e9ca-203">i.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-203">i.</span></span> <span data-ttu-id="6e9ca-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="6e9ca-205">j.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-205">j.</span></span> <span data-ttu-id="6e9ca-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="6e9ca-207">k.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-207">k.</span></span> <span data-ttu-id="6e9ca-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="6e9ca-209">l.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-209">l.</span></span> <span data-ttu-id="6e9ca-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="6e9ca-211">m.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-211">m.</span></span> <span data-ttu-id="6e9ca-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="6e9ca-213">n.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-213">n.</span></span> <span data-ttu-id="6e9ca-214">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6e9ca-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6e9ca-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e9ca-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e9ca-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e9ca-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e9ca-218">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6e9ca-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e9ca-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="6e9ca-221">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e9ca-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e9ca-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/keylight-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="6e9ca-224">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/keylight-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="6e9ca-226">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/keylight-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="6e9ca-228">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e9ca-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e9ca-230">a.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-230">a.</span></span> <span data-ttu-id="6e9ca-231">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e9ca-232">b.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-232">b.</span></span> <span data-ttu-id="6e9ca-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e9ca-234">c.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-234">c.</span></span> <span data-ttu-id="6e9ca-235">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e9ca-236">d.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-236">d.</span></span> <span data-ttu-id="6e9ca-237">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="6e9ca-238">Creating a LockPath Keylight test user</span><span class="sxs-lookup"><span data-stu-id="6e9ca-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="6e9ca-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="6e9ca-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="6e9ca-241">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-241">There is no action item for you in this section.</span></span> <span data-ttu-id="6e9ca-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="6e9ca-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="6e9ca-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e9ca-244">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6e9ca-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e9ca-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Assign User][200] 

<span data-ttu-id="6e9ca-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e9ca-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="6e9ca-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6e9ca-250">In the applications list, select **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Configure Single Sign-On](./media/keylight-tutorial/tutorial_keylight_app.png) 

1. <span data-ttu-id="6e9ca-252">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="6e9ca-254">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-254">Click **Add** button.</span></span> <span data-ttu-id="6e9ca-255">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="6e9ca-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6e9ca-258">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-258">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6e9ca-259">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e9ca-260">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e9ca-260">Testing single sign-on</span></span>

<span data-ttu-id="6e9ca-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6e9ca-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span><span class="sxs-lookup"><span data-stu-id="6e9ca-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e9ca-263">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6e9ca-263">Additional resources</span></span>

* [<span data-ttu-id="6e9ca-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e9ca-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6e9ca-265">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e9ca-265">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/keylight-tutorial/tutorial_general_01.png
[2]: ./media/keylight-tutorial/tutorial_general_02.png
[3]: ./media/keylight-tutorial/tutorial_general_03.png
[4]: ./media/keylight-tutorial/tutorial_general_04.png

[100]: ./media/keylight-tutorial/tutorial_general_100.png

[200]: ./media/keylight-tutorial/tutorial_general_200.png
[201]: ./media/keylight-tutorial/tutorial_general_201.png
[202]: ./media/keylight-tutorial/tutorial_general_202.png
[203]: ./media/keylight-tutorial/tutorial_general_203.png

