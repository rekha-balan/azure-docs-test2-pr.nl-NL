---
title: 'Tutorial: Azure Active Directory integration with HireVue | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HireVue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f208a0c1a5f2fd0c07e6df9e96004d481fd06870
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867131"
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="48f7d-103">Tutorial: Azure Active Directory integration with HireVue</span><span class="sxs-lookup"><span data-stu-id="48f7d-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="48f7d-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48f7d-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48f7d-105">Integrating HireVue with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="48f7d-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48f7d-106">You can control in Azure AD who has access to HireVue</span><span class="sxs-lookup"><span data-stu-id="48f7d-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="48f7d-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="48f7d-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48f7d-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="48f7d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48f7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="48f7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48f7d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48f7d-110">Prerequisites</span></span>

<span data-ttu-id="48f7d-111">To configure Azure AD integration with HireVue, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="48f7d-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="48f7d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="48f7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48f7d-113">A HireVue single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="48f7d-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48f7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="48f7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48f7d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="48f7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48f7d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="48f7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48f7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48f7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48f7d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="48f7d-118">Scenario description</span></span>
<span data-ttu-id="48f7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="48f7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48f7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="48f7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48f7d-121">Adding HireVue from the gallery</span><span class="sxs-lookup"><span data-stu-id="48f7d-121">Adding HireVue from the gallery</span></span>
1. <span data-ttu-id="48f7d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48f7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="48f7d-123">Adding HireVue from the gallery</span><span class="sxs-lookup"><span data-stu-id="48f7d-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="48f7d-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="48f7d-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48f7d-125">**To add HireVue from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48f7d-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48f7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48f7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="48f7d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48f7d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="48f7d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="48f7d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="48f7d-133">In the search box, type **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-133">In the search box, type **HireVue**.</span></span>

    ![Creating an Azure AD test user](./media/hirevue-tutorial/tutorial_hirevue_search.png)

1. <span data-ttu-id="48f7d-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="48f7d-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48f7d-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48f7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48f7d-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48f7d-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48f7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48f7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="48f7d-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span><span class="sxs-lookup"><span data-stu-id="48f7d-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="48f7d-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="48f7d-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48f7d-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="48f7d-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48f7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="48f7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="48f7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48f7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="48f7d-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="48f7d-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="48f7d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48f7d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="48f7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="48f7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48f7d-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48f7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48f7d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span><span class="sxs-lookup"><span data-stu-id="48f7d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="48f7d-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48f7d-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="48f7d-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="48f7d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48f7d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/hirevue-tutorial/tutorial_hirevue_samlbase.png)

1. <span data-ttu-id="48f7d-155">On the **HireVue Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48f7d-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="48f7d-157">a.</span><span class="sxs-lookup"><span data-stu-id="48f7d-157">a.</span></span> <span data-ttu-id="48f7d-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="48f7d-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="48f7d-159">Environment</span><span class="sxs-lookup"><span data-stu-id="48f7d-159">Environment</span></span> | <span data-ttu-id="48f7d-160">URL</span><span class="sxs-lookup"><span data-stu-id="48f7d-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="48f7d-161">Production</span><span class="sxs-lookup"><span data-stu-id="48f7d-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="48f7d-162">Staging</span><span class="sxs-lookup"><span data-stu-id="48f7d-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="48f7d-163">b.</span><span class="sxs-lookup"><span data-stu-id="48f7d-163">b.</span></span> <span data-ttu-id="48f7d-164">In the **Identifier** textbox, type a URL as:</span><span class="sxs-lookup"><span data-stu-id="48f7d-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="48f7d-165">Environment</span><span class="sxs-lookup"><span data-stu-id="48f7d-165">Environment</span></span> | <span data-ttu-id="48f7d-166">URN</span><span class="sxs-lookup"><span data-stu-id="48f7d-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="48f7d-167">Production</span><span class="sxs-lookup"><span data-stu-id="48f7d-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="48f7d-168">Staging</span><span class="sxs-lookup"><span data-stu-id="48f7d-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="48f7d-169">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="48f7d-169">These values are not real.</span></span> <span data-ttu-id="48f7d-170">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="48f7d-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48f7d-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="48f7d-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
1. <span data-ttu-id="48f7d-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="48f7d-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/hirevue-tutorial/tutorial_hirevue_certificate.png) 

1. <span data-ttu-id="48f7d-174">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="48f7d-174">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/hirevue-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="48f7d-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="48f7d-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48f7d-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="48f7d-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/hirevue-tutorial/tutorial_hirevue_configure.png) 

1. <span data-ttu-id="48f7d-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="48f7d-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="48f7d-180">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="48f7d-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="48f7d-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="48f7d-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48f7d-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="48f7d-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48f7d-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48f7d-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48f7d-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48f7d-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="48f7d-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48f7d-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="48f7d-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48f7d-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48f7d-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48f7d-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/hirevue-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="48f7d-190">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/hirevue-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="48f7d-192">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="48f7d-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/hirevue-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="48f7d-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48f7d-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48f7d-196">a.</span><span class="sxs-lookup"><span data-stu-id="48f7d-196">a.</span></span> <span data-ttu-id="48f7d-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48f7d-198">b.</span><span class="sxs-lookup"><span data-stu-id="48f7d-198">b.</span></span> <span data-ttu-id="48f7d-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48f7d-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48f7d-200">c.</span><span class="sxs-lookup"><span data-stu-id="48f7d-200">c.</span></span> <span data-ttu-id="48f7d-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48f7d-202">d.</span><span class="sxs-lookup"><span data-stu-id="48f7d-202">d.</span></span> <span data-ttu-id="48f7d-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="48f7d-204">Creating a HireVue test user</span><span class="sxs-lookup"><span data-stu-id="48f7d-204">Creating a HireVue test user</span></span>

<span data-ttu-id="48f7d-205">In this section, you create a user called Britta Simon in HireVue.</span><span class="sxs-lookup"><span data-stu-id="48f7d-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="48f7d-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span><span class="sxs-lookup"><span data-stu-id="48f7d-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48f7d-207">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48f7d-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48f7d-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span><span class="sxs-lookup"><span data-stu-id="48f7d-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Assign User][200] 

<span data-ttu-id="48f7d-210">**To assign Britta Simon to HireVue, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48f7d-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="48f7d-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="48f7d-213">In the applications list, select **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-213">In the applications list, select **HireVue**.</span></span>

    ![Configure Single Sign-On](./media/hirevue-tutorial/tutorial_hirevue_app.png) 

1. <span data-ttu-id="48f7d-215">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="48f7d-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="48f7d-217">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="48f7d-217">Click **Add** button.</span></span> <span data-ttu-id="48f7d-218">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48f7d-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="48f7d-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="48f7d-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="48f7d-221">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="48f7d-221">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="48f7d-222">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48f7d-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48f7d-223">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="48f7d-223">Testing single sign-on</span></span>

<span data-ttu-id="48f7d-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="48f7d-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48f7d-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span><span class="sxs-lookup"><span data-stu-id="48f7d-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48f7d-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="48f7d-226">Additional resources</span></span>

* [<span data-ttu-id="48f7d-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f7d-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="48f7d-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48f7d-228">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hirevue-tutorial/tutorial_general_01.png
[2]: ./media/hirevue-tutorial/tutorial_general_02.png
[3]: ./media/hirevue-tutorial/tutorial_general_03.png
[4]: ./media/hirevue-tutorial/tutorial_general_04.png

[100]: ./media/hirevue-tutorial/tutorial_general_100.png

[200]: ./media/hirevue-tutorial/tutorial_general_200.png
[201]: ./media/hirevue-tutorial/tutorial_general_201.png
[202]: ./media/hirevue-tutorial/tutorial_general_202.png
[203]: ./media/hirevue-tutorial/tutorial_general_203.png

