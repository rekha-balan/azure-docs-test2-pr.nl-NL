---
title: 'Tutorial: Azure Active Directory integration with Intacct | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: d834ca75085878350e257cc1c50e60fc1bf28484
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870685"
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="33ca4-103">Tutorial: Azure Active Directory integration with Intacct</span><span class="sxs-lookup"><span data-stu-id="33ca4-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="33ca4-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33ca4-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33ca4-105">Integrating Intacct with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="33ca4-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33ca4-106">You can control in Azure AD who has access to Intacct</span><span class="sxs-lookup"><span data-stu-id="33ca4-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="33ca4-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="33ca4-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33ca4-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="33ca4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="33ca4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="33ca4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33ca4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33ca4-110">Prerequisites</span></span>

<span data-ttu-id="33ca4-111">To configure Azure AD integration with Intacct, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="33ca4-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="33ca4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="33ca4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33ca4-113">An Intacct single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="33ca4-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33ca4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="33ca4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33ca4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="33ca4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33ca4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="33ca4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33ca4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33ca4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33ca4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="33ca4-118">Scenario description</span></span>
<span data-ttu-id="33ca4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="33ca4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33ca4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="33ca4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33ca4-121">Adding Intacct from the gallery</span><span class="sxs-lookup"><span data-stu-id="33ca4-121">Adding Intacct from the gallery</span></span>
1. <span data-ttu-id="33ca4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ca4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="33ca4-123">Adding Intacct from the gallery</span><span class="sxs-lookup"><span data-stu-id="33ca4-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="33ca4-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="33ca4-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33ca4-125">**To add Intacct from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ca4-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33ca4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="33ca4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="33ca4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33ca4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="33ca4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="33ca4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="33ca4-133">In the search box, type **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-133">In the search box, type **Intacct**.</span></span>

    ![Creating an Azure AD test user](./media/intacct-tutorial/tutorial_intacct_search.png)

1. <span data-ttu-id="33ca4-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="33ca4-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33ca4-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ca4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33ca4-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="33ca4-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33ca4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33ca4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="33ca4-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span><span class="sxs-lookup"><span data-stu-id="33ca4-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="33ca4-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="33ca4-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33ca4-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="33ca4-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33ca4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="33ca4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="33ca4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33ca4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="33ca4-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="33ca4-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="33ca4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="33ca4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="33ca4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="33ca4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33ca4-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ca4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33ca4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span><span class="sxs-lookup"><span data-stu-id="33ca4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="33ca4-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ca4-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="33ca4-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="33ca4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="33ca4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_samlbase.png)

1. <span data-ttu-id="33ca4-155">On the **Intacct Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ca4-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="33ca4-157">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="33ca4-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="33ca4-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="33ca4-158">This value is not real.</span></span> <span data-ttu-id="33ca4-159">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="33ca4-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="33ca4-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span><span class="sxs-lookup"><span data-stu-id="33ca4-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

1. <span data-ttu-id="33ca4-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="33ca4-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_certificate.png) 

1. <span data-ttu-id="33ca4-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="33ca4-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="33ca4-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="33ca4-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="33ca4-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="33ca4-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_configure.png) 

1. <span data-ttu-id="33ca4-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="33ca4-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

1. <span data-ttu-id="33ca4-169">Click the **Company** tab, and then click **Company Info**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="33ca4-170">![Company](./media/intacct-tutorial/ic790037.png "Company")</span><span class="sxs-lookup"><span data-stu-id="33ca4-170">![Company](./media/intacct-tutorial/ic790037.png "Company")</span></span>

1. <span data-ttu-id="33ca4-171">Click the **Security** tab, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="33ca4-172">![Security](./media/intacct-tutorial/ic790038.png "Security")</span><span class="sxs-lookup"><span data-stu-id="33ca4-172">![Security](./media/intacct-tutorial/ic790038.png "Security")</span></span>

1. <span data-ttu-id="33ca4-173">In the **Single sign on (SSO)** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ca4-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="33ca4-174">![Single sign on](./media/intacct-tutorial/ic790039.png "single sign on")</span><span class="sxs-lookup"><span data-stu-id="33ca4-174">![Single sign on](./media/intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="33ca4-175">a.</span><span class="sxs-lookup"><span data-stu-id="33ca4-175">a.</span></span> <span data-ttu-id="33ca4-176">Select **Enable single sign on**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="33ca4-177">b.</span><span class="sxs-lookup"><span data-stu-id="33ca4-177">b.</span></span> <span data-ttu-id="33ca4-178">As **Identity provider type**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="33ca4-179">c.</span><span class="sxs-lookup"><span data-stu-id="33ca4-179">c.</span></span> <span data-ttu-id="33ca4-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33ca4-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="33ca4-181">d.</span><span class="sxs-lookup"><span data-stu-id="33ca4-181">d.</span></span> <span data-ttu-id="33ca4-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33ca4-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="33ca4-183">e.</span><span class="sxs-lookup"><span data-stu-id="33ca4-183">e.</span></span> <span data-ttu-id="33ca4-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="33ca4-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="33ca4-185">f.</span><span class="sxs-lookup"><span data-stu-id="33ca4-185">f.</span></span> <span data-ttu-id="33ca4-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="33ca4-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="33ca4-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33ca4-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="33ca4-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33ca4-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33ca4-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33ca4-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="33ca4-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="33ca4-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33ca4-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="33ca4-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ca4-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33ca4-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="33ca4-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/intacct-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="33ca4-196">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/intacct-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="33ca4-198">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="33ca4-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/intacct-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="33ca4-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ca4-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33ca4-202">a.</span><span class="sxs-lookup"><span data-stu-id="33ca4-202">a.</span></span> <span data-ttu-id="33ca4-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33ca4-204">b.</span><span class="sxs-lookup"><span data-stu-id="33ca4-204">b.</span></span> <span data-ttu-id="33ca4-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="33ca4-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33ca4-206">c.</span><span class="sxs-lookup"><span data-stu-id="33ca4-206">c.</span></span> <span data-ttu-id="33ca4-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33ca4-208">d.</span><span class="sxs-lookup"><span data-stu-id="33ca4-208">d.</span></span> <span data-ttu-id="33ca4-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="33ca4-210">Creating an Intacct test user</span><span class="sxs-lookup"><span data-stu-id="33ca4-210">Creating an Intacct test user</span></span>

<span data-ttu-id="33ca4-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span><span class="sxs-lookup"><span data-stu-id="33ca4-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="33ca4-212">For Intacct, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="33ca4-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="33ca4-213">**To provision user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ca4-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="33ca4-214">Sign in to your **Intacct** tenant.</span><span class="sxs-lookup"><span data-stu-id="33ca4-214">Sign in to your **Intacct** tenant.</span></span>

1. <span data-ttu-id="33ca4-215">Click the **Company** tab, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="33ca4-216">![Users](./media/intacct-tutorial/ic790041.png "Users")</span><span class="sxs-lookup"><span data-stu-id="33ca4-216">![Users](./media/intacct-tutorial/ic790041.png "Users")</span></span>
1. <span data-ttu-id="33ca4-217">Click the **Add** tab.</span><span class="sxs-lookup"><span data-stu-id="33ca4-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="33ca4-218">![Add](./media/intacct-tutorial/ic790042.png "Add")</span><span class="sxs-lookup"><span data-stu-id="33ca4-218">![Add](./media/intacct-tutorial/ic790042.png "Add")</span></span>
1. <span data-ttu-id="33ca4-219">In the **User Information** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ca4-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="33ca4-220">![User Information](./media/intacct-tutorial/ic790043.png "User Information")</span><span class="sxs-lookup"><span data-stu-id="33ca4-220">![User Information](./media/intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="33ca4-221">a.</span><span class="sxs-lookup"><span data-stu-id="33ca4-221">a.</span></span> <span data-ttu-id="33ca4-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span><span class="sxs-lookup"><span data-stu-id="33ca4-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="33ca4-223">b.</span><span class="sxs-lookup"><span data-stu-id="33ca4-223">b.</span></span> <span data-ttu-id="33ca4-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span><span class="sxs-lookup"><span data-stu-id="33ca4-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="33ca4-225">c.</span><span class="sxs-lookup"><span data-stu-id="33ca4-225">c.</span></span> <span data-ttu-id="33ca4-226">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-226">Click **Save**.</span></span> <span data-ttu-id="33ca4-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="33ca4-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="33ca4-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span><span class="sxs-lookup"><span data-stu-id="33ca4-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33ca4-229">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="33ca4-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33ca4-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span><span class="sxs-lookup"><span data-stu-id="33ca4-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Assign User][200] 

<span data-ttu-id="33ca4-232">**To assign Britta Simon to Intacct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ca4-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="33ca4-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="33ca4-235">In the applications list, select **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-235">In the applications list, select **Intacct**.</span></span>

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_app.png) 

1. <span data-ttu-id="33ca4-237">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="33ca4-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="33ca4-239">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="33ca4-239">Click **Add** button.</span></span> <span data-ttu-id="33ca4-240">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="33ca4-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="33ca4-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="33ca4-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="33ca4-243">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="33ca4-243">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="33ca4-244">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="33ca4-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33ca4-245">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ca4-245">Testing single sign-on</span></span>

<span data-ttu-id="33ca4-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="33ca4-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="33ca4-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span><span class="sxs-lookup"><span data-stu-id="33ca4-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33ca4-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="33ca4-248">Additional resources</span></span>

* [<span data-ttu-id="33ca4-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33ca4-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="33ca4-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33ca4-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/intacct-tutorial/tutorial_general_01.png
[2]: ./media/intacct-tutorial/tutorial_general_02.png
[3]: ./media/intacct-tutorial/tutorial_general_03.png
[4]: ./media/intacct-tutorial/tutorial_general_04.png

[100]: ./media/intacct-tutorial/tutorial_general_100.png

[200]: ./media/intacct-tutorial/tutorial_general_200.png
[201]: ./media/intacct-tutorial/tutorial_general_201.png
[202]: ./media/intacct-tutorial/tutorial_general_202.png
[203]: ./media/intacct-tutorial/tutorial_general_203.png

