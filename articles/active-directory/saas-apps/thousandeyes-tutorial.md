---
title: 'Tutorial: Azure Active Directory integration with ThousandEyes | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: b6af7a3322b1a01c1d822df78d827121c19e21e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866723"
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="ff086-103">Tutorial: Azure Active Directory integration with ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="ff086-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="ff086-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff086-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff086-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ff086-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff086-106">You can control in Azure AD who has access to ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="ff086-106">You can control in Azure AD who has access to ThousandEyes</span></span>
- <span data-ttu-id="ff086-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ff086-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff086-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ff086-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ff086-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ff086-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff086-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff086-110">Prerequisites</span></span>

<span data-ttu-id="ff086-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ff086-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span></span>

- <span data-ttu-id="ff086-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ff086-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff086-113">A ThousandEyes single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ff086-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff086-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ff086-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff086-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ff086-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff086-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ff086-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff086-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff086-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff086-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ff086-118">Scenario description</span></span>
<span data-ttu-id="ff086-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ff086-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff086-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff086-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff086-121">Adding ThousandEyes from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff086-121">Adding ThousandEyes from the gallery</span></span>
1. <span data-ttu-id="ff086-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff086-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-the-gallery"></a><span data-ttu-id="ff086-123">Adding ThousandEyes from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff086-123">Adding ThousandEyes from the gallery</span></span>
<span data-ttu-id="ff086-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ff086-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff086-125">**To add ThousandEyes from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff086-125">**To add ThousandEyes from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff086-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ff086-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="ff086-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ff086-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff086-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ff086-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="ff086-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ff086-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="ff086-133">In the search box, type **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="ff086-133">In the search box, type **ThousandEyes**.</span></span>

    ![Creating an Azure AD test user](./media/thousandeyes-tutorial/tutorial_thousandeyes_search.png)

1. <span data-ttu-id="ff086-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ff086-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff086-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff086-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff086-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ff086-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff086-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff086-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span></span> <span data-ttu-id="ff086-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ff086-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span></span>

<span data-ttu-id="ff086-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ff086-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ff086-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff086-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff086-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ff086-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ff086-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff086-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ff086-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ff086-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ff086-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ff086-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ff086-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ff086-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff086-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff086-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff086-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span><span class="sxs-lookup"><span data-stu-id="ff086-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="ff086-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff086-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="ff086-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ff086-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="ff086-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ff086-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

1. <span data-ttu-id="ff086-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff086-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="ff086-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="ff086-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

1. <span data-ttu-id="ff086-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ff086-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/thousandeyes-tutorial/tutorial_thousandeyes_certificate.png)

1. <span data-ttu-id="ff086-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ff086-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/thousandeyes-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ff086-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ff086-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ff086-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="ff086-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

1. <span data-ttu-id="ff086-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ff086-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

1. <span data-ttu-id="ff086-166">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ff086-166">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="ff086-167">![Settings](./media/thousandeyes-tutorial/ic790066.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="ff086-167">![Settings](./media/thousandeyes-tutorial/ic790066.png "Settings")</span></span>

1. <span data-ttu-id="ff086-168">Click **Account**</span><span class="sxs-lookup"><span data-stu-id="ff086-168">Click **Account**</span></span>

    <span data-ttu-id="ff086-169">![Account](./media/thousandeyes-tutorial/ic790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="ff086-169">![Account](./media/thousandeyes-tutorial/ic790067.png "Account")</span></span>

1. <span data-ttu-id="ff086-170">Click the **Security & Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="ff086-170">Click the **Security & Authentication** tab.</span></span>

    <span data-ttu-id="ff086-171">![Security & Authentication](./media/thousandeyes-tutorial/ic790068.png "Security & Authentication")</span><span class="sxs-lookup"><span data-stu-id="ff086-171">![Security & Authentication](./media/thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

1. <span data-ttu-id="ff086-172">In the **Setup Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff086-172">In the **Setup Single Sign-On** section, perform the following steps:</span></span>

    <span data-ttu-id="ff086-173">![Setup Single Sign-On](./media/thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ff086-173">![Setup Single Sign-On](./media/thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>

    <span data-ttu-id="ff086-174">a.</span><span class="sxs-lookup"><span data-stu-id="ff086-174">a.</span></span> <span data-ttu-id="ff086-175">Select **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ff086-175">Select **Enable Single Sign-On**.</span></span>

    <span data-ttu-id="ff086-176">b.</span><span class="sxs-lookup"><span data-stu-id="ff086-176">b.</span></span> <span data-ttu-id="ff086-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff086-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ff086-178">c.</span><span class="sxs-lookup"><span data-stu-id="ff086-178">c.</span></span> <span data-ttu-id="ff086-179">In **Logout Page URL** textbox, paste **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff086-179">In **Logout Page URL** textbox, paste **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ff086-180">d.</span><span class="sxs-lookup"><span data-stu-id="ff086-180">d.</span></span> <span data-ttu-id="ff086-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff086-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ff086-182">e.</span><span class="sxs-lookup"><span data-stu-id="ff086-182">e.</span></span> <span data-ttu-id="ff086-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff086-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="ff086-184">f.</span><span class="sxs-lookup"><span data-stu-id="ff086-184">f.</span></span> <span data-ttu-id="ff086-185">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff086-185">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff086-186">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff086-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff086-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff086-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ff086-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff086-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff086-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ff086-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/thousandeyes-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="ff086-192">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ff086-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/thousandeyes-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="ff086-194">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ff086-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/thousandeyes-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="ff086-196">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff086-196">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/thousandeyes-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ff086-198">a.</span><span class="sxs-lookup"><span data-stu-id="ff086-198">a.</span></span> <span data-ttu-id="ff086-199">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff086-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff086-200">b.</span><span class="sxs-lookup"><span data-stu-id="ff086-200">b.</span></span> <span data-ttu-id="ff086-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff086-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff086-202">c.</span><span class="sxs-lookup"><span data-stu-id="ff086-202">c.</span></span> <span data-ttu-id="ff086-203">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ff086-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff086-204">d.</span><span class="sxs-lookup"><span data-stu-id="ff086-204">d.</span></span> <span data-ttu-id="ff086-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff086-205">Click **Create**.</span></span>

### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="ff086-206">Creating a ThousandEyes test user</span><span class="sxs-lookup"><span data-stu-id="ff086-206">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="ff086-207">The objective of this section is to create a user called Britta Simon in ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="ff086-207">The objective of this section is to create a user called Britta Simon in ThousandEyes.</span></span> <span data-ttu-id="ff086-208">ThousandEyes supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ff086-208">ThousandEyes supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="ff086-209">You can find more details [here](thousandeyes-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="ff086-209">You can find more details [here](thousandeyes-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="ff086-210">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff086-210">**If you need to create user manually, perform following steps:**</span></span>

1. <span data-ttu-id="ff086-211">Log into your ThousandEyes company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ff086-211">Log into your ThousandEyes company site as an administrator.</span></span>

1. <span data-ttu-id="ff086-212">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ff086-212">Click **Settings**.</span></span>

    <span data-ttu-id="ff086-213">![Settings](./media/thousandeyes-tutorial/IC790066.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="ff086-213">![Settings](./media/thousandeyes-tutorial/IC790066.png "Settings")</span></span>

1. <span data-ttu-id="ff086-214">Click **Account**.</span><span class="sxs-lookup"><span data-stu-id="ff086-214">Click **Account**.</span></span>

    <span data-ttu-id="ff086-215">![Account](./media/thousandeyes-tutorial/IC790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="ff086-215">![Account](./media/thousandeyes-tutorial/IC790067.png "Account")</span></span>

1. <span data-ttu-id="ff086-216">Click the **Accounts & Users** tab.</span><span class="sxs-lookup"><span data-stu-id="ff086-216">Click the **Accounts & Users** tab.</span></span>

    <span data-ttu-id="ff086-217">![Accounts & Users](./media/thousandeyes-tutorial/IC790073.png "Accounts & Users")</span><span class="sxs-lookup"><span data-stu-id="ff086-217">![Accounts & Users](./media/thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

1. <span data-ttu-id="ff086-218">In the **Add Users & Accounts** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff086-218">In the **Add Users & Accounts** section, perform the following steps:</span></span>

    <span data-ttu-id="ff086-219">![Add User Accounts](./media/thousandeyes-tutorial/IC790074.png "Add User Accounts")</span><span class="sxs-lookup"><span data-stu-id="ff086-219">![Add User Accounts](./media/thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>

    <span data-ttu-id="ff086-220">a.</span><span class="sxs-lookup"><span data-stu-id="ff086-220">a.</span></span> <span data-ttu-id="ff086-221">In **Name** textbox, type the name of user like **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff086-221">In **Name** textbox, type the name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="ff086-222">b.</span><span class="sxs-lookup"><span data-stu-id="ff086-222">b.</span></span> <span data-ttu-id="ff086-223">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ff086-223">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="ff086-224">b.</span><span class="sxs-lookup"><span data-stu-id="ff086-224">b.</span></span> <span data-ttu-id="ff086-225">Click **Add New User to Account**.</span><span class="sxs-lookup"><span data-stu-id="ff086-225">Click **Add New User to Account**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff086-226">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span><span class="sxs-lookup"><span data-stu-id="ff086-226">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span></span>

> [!NOTE]
> <span data-ttu-id="ff086-227">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="ff086-227">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff086-228">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff086-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff086-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="ff086-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span></span>

![Assign User][200] 

<span data-ttu-id="ff086-231">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff086-231">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="ff086-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ff086-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ff086-234">In the applications list, select **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="ff086-234">In the applications list, select **ThousandEyes**.</span></span>

    ![Configure Single Sign-On](./media/thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

1. <span data-ttu-id="ff086-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ff086-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="ff086-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ff086-238">Click **Add** button.</span></span> <span data-ttu-id="ff086-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ff086-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="ff086-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ff086-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ff086-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ff086-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ff086-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ff086-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff086-244">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff086-244">Testing single sign-on</span></span>

<span data-ttu-id="ff086-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ff086-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff086-246">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span><span class="sxs-lookup"><span data-stu-id="ff086-246">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span></span>

<span data-ttu-id="ff086-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff086-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff086-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ff086-248">Additional resources</span></span>

* [<span data-ttu-id="ff086-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff086-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ff086-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff086-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="ff086-251">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="ff086-251">Configure User Provisioning</span></span>](thousandeyes-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/thousandeyes-tutorial/tutorial_general_203.png
