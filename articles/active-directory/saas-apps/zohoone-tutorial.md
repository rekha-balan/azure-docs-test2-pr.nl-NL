---
title: 'Tutorial: Azure Active Directory integration with Zoho One | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zoho One.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bbc3038c-0d8b-45dd-9645-368bd3d01a0f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: jeedes
ms.openlocfilehash: 81e86df270a7286426363c26a0e8a87b99082428
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856889"
---
# <a name="tutorial-azure-active-directory-integration-with-zoho-one"></a><span data-ttu-id="0c88b-103">Tutorial: Azure Active Directory integration with Zoho One</span><span class="sxs-lookup"><span data-stu-id="0c88b-103">Tutorial: Azure Active Directory integration with Zoho One</span></span>

<span data-ttu-id="0c88b-104">In this tutorial, you learn how to integrate Zoho One with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c88b-104">In this tutorial, you learn how to integrate Zoho One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c88b-105">Integrating Zoho One with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0c88b-105">Integrating Zoho One with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0c88b-106">You can control in Azure AD who has access to Zoho One.</span><span class="sxs-lookup"><span data-stu-id="0c88b-106">You can control in Azure AD who has access to Zoho One.</span></span>
- <span data-ttu-id="0c88b-107">You can enable your users to automatically get signed-on to Zoho One (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="0c88b-107">You can enable your users to automatically get signed-on to Zoho One (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0c88b-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c88b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0c88b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0c88b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c88b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c88b-110">Prerequisites</span></span>

<span data-ttu-id="0c88b-111">To configure Azure AD integration with Zoho One, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0c88b-111">To configure Azure AD integration with Zoho One, you need the following items:</span></span>

- <span data-ttu-id="0c88b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0c88b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c88b-113">A Zoho One single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0c88b-113">A Zoho One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c88b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0c88b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c88b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0c88b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c88b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0c88b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c88b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c88b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c88b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0c88b-118">Scenario description</span></span>
<span data-ttu-id="0c88b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0c88b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c88b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0c88b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c88b-121">Adding Zoho One from the gallery</span><span class="sxs-lookup"><span data-stu-id="0c88b-121">Adding Zoho One from the gallery</span></span>
1. <span data-ttu-id="0c88b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c88b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-one-from-the-gallery"></a><span data-ttu-id="0c88b-123">Adding Zoho One from the gallery</span><span class="sxs-lookup"><span data-stu-id="0c88b-123">Adding Zoho One from the gallery</span></span>
<span data-ttu-id="0c88b-124">To configure the integration of Zoho One into Azure AD, you need to add Zoho One from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0c88b-124">To configure the integration of Zoho One into Azure AD, you need to add Zoho One from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0c88b-125">**To add Zoho One from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c88b-125">**To add Zoho One from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0c88b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0c88b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="0c88b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0c88b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="0c88b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0c88b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="0c88b-133">In the search box, type **Zoho One**, select **Zoho One** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0c88b-133">In the search box, type **Zoho One**, select **Zoho One** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho One in the results list](./media/zohoone-tutorial/tutorial_zohoone_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0c88b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c88b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0c88b-136">In this section, you configure and test Azure AD single sign-on with Zoho One based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0c88b-136">In this section, you configure and test Azure AD single sign-on with Zoho One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0c88b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho One is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c88b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho One is to a user in Azure AD.</span></span> <span data-ttu-id="0c88b-138">In other words, a link relationship between an Azure AD user and the related user in Zoho One needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0c88b-138">In other words, a link relationship between an Azure AD user and the related user in Zoho One needs to be established.</span></span>

<span data-ttu-id="0c88b-139">To configure and test Azure AD single sign-on with Zoho One, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0c88b-139">To configure and test Azure AD single sign-on with Zoho One, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0c88b-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0c88b-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0c88b-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c88b-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0c88b-142">**[Create a Zoho One test user](#create-a-zoho-one-test-user)** - to have a counterpart of Britta Simon in Zoho One that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0c88b-142">**[Create a Zoho One test user](#create-a-zoho-one-test-user)** - to have a counterpart of Britta Simon in Zoho One that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0c88b-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0c88b-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0c88b-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0c88b-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0c88b-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c88b-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0c88b-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho One application.</span><span class="sxs-lookup"><span data-stu-id="0c88b-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho One application.</span></span>

<span data-ttu-id="0c88b-147">**To configure Azure AD single sign-on with Zoho One, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c88b-147">**To configure Azure AD single sign-on with Zoho One, perform the following steps:**</span></span>

1. <span data-ttu-id="0c88b-148">In the Azure portal, on the **Zoho One** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-148">In the Azure portal, on the **Zoho One** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="0c88b-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0c88b-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/zohoone-tutorial/tutorial_zohoone_samlbase.png)

1. <span data-ttu-id="0c88b-152">On the **Zoho One Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="0c88b-152">On the **Zoho One Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Zoho One Domain and URLs single sign-on information](./media/zohoone-tutorial/tutorial_zohoone_url.png)

    <span data-ttu-id="0c88b-154">a.</span><span class="sxs-lookup"><span data-stu-id="0c88b-154">a.</span></span> <span data-ttu-id="0c88b-155">In the **Identifier (Entity ID)** textbox, type a URL: `one.zoho.com`</span><span class="sxs-lookup"><span data-stu-id="0c88b-155">In the **Identifier (Entity ID)** textbox, type a URL: `one.zoho.com`</span></span>

    <span data-ttu-id="0c88b-156">b.</span><span class="sxs-lookup"><span data-stu-id="0c88b-156">b.</span></span> <span data-ttu-id="0c88b-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://accounts.zoho.com/samlresponse/<saml-identifier>`</span><span class="sxs-lookup"><span data-stu-id="0c88b-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://accounts.zoho.com/samlresponse/<saml-identifier>`</span></span>

    <span data-ttu-id="0c88b-158">c.</span><span class="sxs-lookup"><span data-stu-id="0c88b-158">c.</span></span> <span data-ttu-id="0c88b-159">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-159">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="0c88b-160">d.</span><span class="sxs-lookup"><span data-stu-id="0c88b-160">d.</span></span> <span data-ttu-id="0c88b-161">In the **Relay State** textbox, type a URL:`https://one.zoho.com`</span><span class="sxs-lookup"><span data-stu-id="0c88b-161">In the **Relay State** textbox, type a URL:`https://one.zoho.com`</span></span>

1. <span data-ttu-id="0c88b-162">If you wish to configure the application in **SP** initiated mode perform the following step:</span><span class="sxs-lookup"><span data-stu-id="0c88b-162">If you wish to configure the application in **SP** initiated mode perform the following step:</span></span>

    <span data-ttu-id="0c88b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://accounts.zoho.com/samlauthrequest/<domain_name>?serviceurl=https://one.zoho.com`</span><span class="sxs-lookup"><span data-stu-id="0c88b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://accounts.zoho.com/samlauthrequest/<domain_name>?serviceurl=https://one.zoho.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0c88b-164">The preceding **Reply URL** and **Sign-on URL** value is not real.</span><span class="sxs-lookup"><span data-stu-id="0c88b-164">The preceding **Reply URL** and **Sign-on URL** value is not real.</span></span> <span data-ttu-id="0c88b-165">You will update the value with the actual Reply URL and Sign-On URL which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0c88b-165">You will update the value with the actual Reply URL and Sign-On URL which is explained later in the tutorial.</span></span> 

1. <span data-ttu-id="0c88b-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0c88b-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/zohoone-tutorial/tutorial_zohoone_certificate.png) 

1. <span data-ttu-id="0c88b-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0c88b-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zohoone-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="0c88b-170">On the **Zoho One Configuration** section, click **Configure Zoho One** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0c88b-170">On the **Zoho One Configuration** section, click **Configure Zoho One** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0c88b-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="0c88b-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoho One Configuration](./media/zohoone-tutorial/tutorial_zohoone_configure.png) 

1. <span data-ttu-id="0c88b-173">In a different web browser window, log in to your Zoho One company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0c88b-173">In a different web browser window, log in to your Zoho One company site as an administrator.</span></span>

1. <span data-ttu-id="0c88b-174">On the **Organization** tab, Click **Setup** under **SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-174">On the **Organization** tab, Click **Setup** under **SAML Authentication**.</span></span>

    ![Zoho One org](./media/zohoone-tutorial/tutorial_zohoone_setup.png)

1. <span data-ttu-id="0c88b-176">On the Pop-up page perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c88b-176">On the Pop-up page perform the following steps:</span></span>

    ![Zoho One sig](./media/zohoone-tutorial/tutorial_zohoone_save.png)

    <span data-ttu-id="0c88b-178">a.</span><span class="sxs-lookup"><span data-stu-id="0c88b-178">a.</span></span> <span data-ttu-id="0c88b-179">In the **Sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c88b-179">In the **Sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0c88b-180">b.</span><span class="sxs-lookup"><span data-stu-id="0c88b-180">b.</span></span> <span data-ttu-id="0c88b-181">In the **Sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c88b-181">In the **Sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0c88b-182">c.</span><span class="sxs-lookup"><span data-stu-id="0c88b-182">c.</span></span> <span data-ttu-id="0c88b-183">Click **Browse** to upload the **Certificate (Base64)** which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c88b-183">Click **Browse** to upload the **Certificate (Base64)** which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="0c88b-184">d.</span><span class="sxs-lookup"><span data-stu-id="0c88b-184">d.</span></span> <span data-ttu-id="0c88b-185">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-185">Click **Save**.</span></span>

1. <span data-ttu-id="0c88b-186">After saving the SAML Authentication setup, copy the **SAML-Identfier** value and use this value in the **Reply URL** in the Azure portal, under **Zoho One Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="0c88b-186">After saving the SAML Authentication setup, copy the **SAML-Identfier** value and use this value in the **Reply URL** in the Azure portal, under **Zoho One Domain and URLs** section.</span></span>

    ![Zoho One saml](./media/zohoone-tutorial/tutorial_zohoone_samlidenti.png)

1. <span data-ttu-id="0c88b-188">Go to the **Domains** tab and then click **Add Domain**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-188">Go to the **Domains** tab and then click **Add Domain**.</span></span>

    ![Zoho One domain](./media/zohoone-tutorial/tutorial_zohoone_domain.png)

1. <span data-ttu-id="0c88b-190">On the **Add Domain** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c88b-190">On the **Add Domain** page, perform the following steps:</span></span>

    ![Zoho One add domain](./media/zohoone-tutorial/tutorial_zohoone_adddomain.png)

    <span data-ttu-id="0c88b-192">a.</span><span class="sxs-lookup"><span data-stu-id="0c88b-192">a.</span></span> <span data-ttu-id="0c88b-193">In the **Domain Name** textbox, type domain like **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-193">In the **Domain Name** textbox, type domain like **contoso.com**.</span></span>

    <span data-ttu-id="0c88b-194">b.</span><span class="sxs-lookup"><span data-stu-id="0c88b-194">b.</span></span> <span data-ttu-id="0c88b-195">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-195">Click **Add**.</span></span>

    >[!Note]
    ><span data-ttu-id="0c88b-196">After adding the domain follow [these](https://www.zoho.com/one/help/admin-guide/domain-verification.html) steps to verify your domain.</span><span class="sxs-lookup"><span data-stu-id="0c88b-196">After adding the domain follow [these](https://www.zoho.com/one/help/admin-guide/domain-verification.html) steps to verify your domain.</span></span> <span data-ttu-id="0c88b-197">Once the domain is verfified, use your domain name in **Sign-on URL** in **Zoho One Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c88b-197">Once the domain is verfified, use your domain name in **Sign-on URL** in **Zoho One Domain and URLs** section in Azure portal.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0c88b-198">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0c88b-198">Create an Azure AD test user</span></span>

<span data-ttu-id="0c88b-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c88b-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="0c88b-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c88b-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0c88b-202">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="0c88b-202">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zohoone-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="0c88b-204">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-204">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zohoone-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="0c88b-206">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="0c88b-206">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zohoone-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="0c88b-208">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c88b-208">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zohoone-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0c88b-210">a.</span><span class="sxs-lookup"><span data-stu-id="0c88b-210">a.</span></span> <span data-ttu-id="0c88b-211">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-211">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c88b-212">b.</span><span class="sxs-lookup"><span data-stu-id="0c88b-212">b.</span></span> <span data-ttu-id="0c88b-213">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c88b-213">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0c88b-214">c.</span><span class="sxs-lookup"><span data-stu-id="0c88b-214">c.</span></span> <span data-ttu-id="0c88b-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="0c88b-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0c88b-216">d.</span><span class="sxs-lookup"><span data-stu-id="0c88b-216">d.</span></span> <span data-ttu-id="0c88b-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-217">Click **Create**.</span></span>
 
### <a name="create-a-zoho-one-test-user"></a><span data-ttu-id="0c88b-218">Create a Zoho One test user</span><span class="sxs-lookup"><span data-stu-id="0c88b-218">Create a Zoho One test user</span></span>

<span data-ttu-id="0c88b-219">To enable Azure AD users to log in to Zoho One, they must be provisioned into Zoho One.</span><span class="sxs-lookup"><span data-stu-id="0c88b-219">To enable Azure AD users to log in to Zoho One, they must be provisioned into Zoho One.</span></span> <span data-ttu-id="0c88b-220">In Zoho One, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="0c88b-220">In Zoho One, provisioning is a manual task.</span></span>

<span data-ttu-id="0c88b-221">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c88b-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0c88b-222">Log in to Zoho One as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="0c88b-222">Log in to Zoho One as a Security Administrator.</span></span>

1. <span data-ttu-id="0c88b-223">On the **Users** tab, Click on **user logo**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-223">On the **Users** tab, Click on **user logo**.</span></span>

    ![Zoho One user](./media/zohoone-tutorial/tutorial_zohoone_users.png)

1. <span data-ttu-id="0c88b-225">On the **Add User** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c88b-225">On the **Add User** page, perform the following steps:</span></span>

    ![Zoho One add user](./media/zohoone-tutorial/tutorial_zohoone_adduser.png)
    
    <span data-ttu-id="0c88b-227">a.</span><span class="sxs-lookup"><span data-stu-id="0c88b-227">a.</span></span> <span data-ttu-id="0c88b-228">In **Name** text box, enter the name of user like **Britta simon**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-228">In **Name** text box, enter the name of user like **Britta simon**.</span></span>
    
    <span data-ttu-id="0c88b-229">b.</span><span class="sxs-lookup"><span data-stu-id="0c88b-229">b.</span></span> <span data-ttu-id="0c88b-230">In **Email Address** text box, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-230">In **Email Address** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    >[!Note]
    ><span data-ttu-id="0c88b-231">Select your verified domain from the domain list.</span><span class="sxs-lookup"><span data-stu-id="0c88b-231">Select your verified domain from the domain list.</span></span>

    <span data-ttu-id="0c88b-232">c.</span><span class="sxs-lookup"><span data-stu-id="0c88b-232">c.</span></span> <span data-ttu-id="0c88b-233">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-233">Click **Add**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0c88b-234">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0c88b-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="0c88b-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho One.</span><span class="sxs-lookup"><span data-stu-id="0c88b-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho One.</span></span>

![Assign the user role][200] 

<span data-ttu-id="0c88b-237">**To assign Britta Simon to Zoho One, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c88b-237">**To assign Britta Simon to Zoho One, perform the following steps:**</span></span>

1. <span data-ttu-id="0c88b-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0c88b-240">In the applications list, select **Zoho One**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-240">In the applications list, select **Zoho One**.</span></span>

    ![The Zoho One link in the Applications list](./media/zohoone-tutorial/tutorial_zohoone_app.png)  

1. <span data-ttu-id="0c88b-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-242">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="0c88b-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0c88b-244">Click **Add** button.</span></span> <span data-ttu-id="0c88b-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c88b-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="0c88b-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0c88b-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0c88b-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c88b-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0c88b-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c88b-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0c88b-250">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c88b-250">Test single sign-on</span></span>

<span data-ttu-id="0c88b-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0c88b-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0c88b-252">When you click the Zoho One tile in the Access Panel, you should get automatically signed-on to your Zoho One application.</span><span class="sxs-lookup"><span data-stu-id="0c88b-252">When you click the Zoho One tile in the Access Panel, you should get automatically signed-on to your Zoho One application.</span></span>
<span data-ttu-id="0c88b-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0c88b-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0c88b-254">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0c88b-254">Additional resources</span></span>

* [<span data-ttu-id="0c88b-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c88b-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0c88b-256">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c88b-256">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/zohoone-tutorial/tutorial_general_01.png
[2]: ./media/zohoone-tutorial/tutorial_general_02.png
[3]: ./media/zohoone-tutorial/tutorial_general_03.png
[4]: ./media/zohoone-tutorial/tutorial_general_04.png

[100]: ./media/zohoone-tutorial/tutorial_general_100.png

[200]: ./media/zohoone-tutorial/tutorial_general_200.png
[201]: ./media/zohoone-tutorial/tutorial_general_201.png
[202]: ./media/zohoone-tutorial/tutorial_general_202.png
[203]: ./media/zohoone-tutorial/tutorial_general_203.png

