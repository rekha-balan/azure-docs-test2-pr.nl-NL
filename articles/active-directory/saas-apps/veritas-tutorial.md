---
title: 'Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Veritas Enterprise Vault.cloud SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: jeedes
ms.openlocfilehash: 4ff282b3db4689ceaf5fa27b57c82cb05025712e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869023"
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="cc148-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="cc148-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="cc148-104">In this tutorial, you learn how to integrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc148-104">In this tutorial, you learn how to integrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc148-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cc148-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc148-106">You can control in Azure AD who has access to Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="cc148-106">You can control in Azure AD who has access to Veritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="cc148-107">You can enable your users to automatically get signed-on to Veritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cc148-107">You can enable your users to automatically get signed-on to Veritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc148-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cc148-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc148-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cc148-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc148-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc148-110">Prerequisites</span></span>

<span data-ttu-id="cc148-111">To configure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cc148-111">To configure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need the following items:</span></span>

- <span data-ttu-id="cc148-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cc148-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc148-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cc148-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc148-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cc148-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc148-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cc148-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc148-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cc148-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc148-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc148-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc148-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cc148-118">Scenario description</span></span>
<span data-ttu-id="cc148-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cc148-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc148-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc148-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc148-121">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc148-121">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
1. <span data-ttu-id="cc148-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc148-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-the-gallery"></a><span data-ttu-id="cc148-123">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc148-123">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
<span data-ttu-id="cc148-124">To configure the integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need to add Veritas Enterprise Vault.cloud SSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cc148-124">To configure the integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need to add Veritas Enterprise Vault.cloud SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc148-125">**To add Veritas Enterprise Vault.cloud SSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc148-125">**To add Veritas Enterprise Vault.cloud SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc148-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc148-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cc148-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cc148-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc148-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc148-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cc148-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cc148-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cc148-133">In the search box, type **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="cc148-133">In the search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Creating an Azure AD test user](./media/veritas-tutorial/tutorial_veritas_search.png)

1. <span data-ttu-id="cc148-135">In the results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cc148-135">In the results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc148-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc148-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc148-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc148-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc148-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Veritas Enterprise Vault.cloud SSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc148-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Veritas Enterprise Vault.cloud SSO is to a user in Azure AD.</span></span> <span data-ttu-id="cc148-140">In other words, a link relationship between an Azure AD user and the related user in Veritas Enterprise Vault.cloud SSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cc148-140">In other words, a link relationship between an Azure AD user and the related user in Veritas Enterprise Vault.cloud SSO needs to be established.</span></span>

<span data-ttu-id="cc148-141">In Veritas Enterprise Vault.cloud SSO, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cc148-141">In Veritas Enterprise Vault.cloud SSO, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc148-142">To configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc148-142">To configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc148-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cc148-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cc148-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc148-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cc148-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - to have a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cc148-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - to have a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cc148-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc148-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cc148-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cc148-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc148-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc148-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc148-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span><span class="sxs-lookup"><span data-stu-id="cc148-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>

<span data-ttu-id="cc148-150">**To configure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc148-150">**To configure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="cc148-151">In the Azure portal, on the **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc148-151">In the Azure portal, on the **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cc148-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc148-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/veritas-tutorial/tutorial_veritas_samlbase.png)

1. <span data-ttu-id="cc148-155">On the **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc148-155">On the **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/veritas-tutorial/tutorial_veritas_url.png)

    <span data-ttu-id="cc148-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc148-157">a.</span></span> <span data-ttu-id="cc148-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="cc148-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>

    <span data-ttu-id="cc148-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc148-159">b.</span></span> <span data-ttu-id="cc148-160">In the **Identifier** textbox, use the URL as per the Datacenter</span><span class="sxs-lookup"><span data-stu-id="cc148-160">In the **Identifier** textbox, use the URL as per the Datacenter</span></span>

    | <span data-ttu-id="cc148-161">Datacenter</span><span class="sxs-lookup"><span data-stu-id="cc148-161">Datacenter</span></span>| <span data-ttu-id="cc148-162">URL</span><span class="sxs-lookup"><span data-stu-id="cc148-162">URL</span></span> |
    |----------|----|
    | <span data-ttu-id="cc148-163">North America</span><span class="sxs-lookup"><span data-stu-id="cc148-163">North America</span></span>| `https://auth.lax.archivecloud.net` |
    | <span data-ttu-id="cc148-164">Europe</span><span class="sxs-lookup"><span data-stu-id="cc148-164">Europe</span></span> | `https://auth.ams.archivecloud.net` |
    | <span data-ttu-id="cc148-165">Asia Pacific</span><span class="sxs-lookup"><span data-stu-id="cc148-165">Asia Pacific</span></span>| `https://auth.syd.archivecloud.net`|

    <span data-ttu-id="cc148-166">c.</span><span class="sxs-lookup"><span data-stu-id="cc148-166">c.</span></span> <span data-ttu-id="cc148-167">In the **Reply URL** textbox, use the URL as per the Datacenter</span><span class="sxs-lookup"><span data-stu-id="cc148-167">In the **Reply URL** textbox, use the URL as per the Datacenter</span></span>

    | <span data-ttu-id="cc148-168">Datacenter</span><span class="sxs-lookup"><span data-stu-id="cc148-168">Datacenter</span></span>| <span data-ttu-id="cc148-169">URL</span><span class="sxs-lookup"><span data-stu-id="cc148-169">URL</span></span> |
    |----------|----|
    | <span data-ttu-id="cc148-170">North America</span><span class="sxs-lookup"><span data-stu-id="cc148-170">North America</span></span>| `https://auth.lax.archivecloud.net` |
    | <span data-ttu-id="cc148-171">Europe</span><span class="sxs-lookup"><span data-stu-id="cc148-171">Europe</span></span> | `https://auth.ams.archivecloud.net` |
    | <span data-ttu-id="cc148-172">Asia Pacific</span><span class="sxs-lookup"><span data-stu-id="cc148-172">Asia Pacific</span></span>| `https://auth.syd.archivecloud.net`|
    
    > [!NOTE] 
    > <span data-ttu-id="cc148-173">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="cc148-173">This value is not real.</span></span> <span data-ttu-id="cc148-174">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="cc148-174">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="cc148-175">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) to get this value.</span><span class="sxs-lookup"><span data-stu-id="cc148-175">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) to get this value.</span></span> 

1. <span data-ttu-id="cc148-176">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cc148-176">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/veritas-tutorial/tutorial_veritas_certificate.png) 

1. <span data-ttu-id="cc148-178">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cc148-178">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/veritas-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cc148-180">On the **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cc148-180">On the **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cc148-181">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="cc148-181">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/veritas-tutorial/tutorial_veritas_configure.png) 

1. <span data-ttu-id="cc148-183">To configure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span><span class="sxs-lookup"><span data-stu-id="cc148-183">To configure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span></span>

> [!TIP]
> <span data-ttu-id="cc148-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cc148-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc148-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cc148-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc148-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc148-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc148-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc148-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc148-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc148-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cc148-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc148-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc148-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc148-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/veritas-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cc148-193">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cc148-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/veritas-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cc148-195">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cc148-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/veritas-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cc148-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc148-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/veritas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc148-199">a.</span><span class="sxs-lookup"><span data-stu-id="cc148-199">a.</span></span> <span data-ttu-id="cc148-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc148-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc148-201">b.</span><span class="sxs-lookup"><span data-stu-id="cc148-201">b.</span></span> <span data-ttu-id="cc148-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc148-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc148-203">c.</span><span class="sxs-lookup"><span data-stu-id="cc148-203">c.</span></span> <span data-ttu-id="cc148-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc148-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc148-205">d.</span><span class="sxs-lookup"><span data-stu-id="cc148-205">d.</span></span> <span data-ttu-id="cc148-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc148-206">Click **Create**.</span></span>
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="cc148-207">Creating a Veritas Enterprise Vault.cloud SSO test user</span><span class="sxs-lookup"><span data-stu-id="cc148-207">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="cc148-208">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="cc148-208">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="cc148-209">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add the users in the Enterprise Vault.cloud SSO platform.</span><span class="sxs-lookup"><span data-stu-id="cc148-209">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add the users in the Enterprise Vault.cloud SSO platform.</span></span> <span data-ttu-id="cc148-210">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc148-210">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc148-211">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc148-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc148-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="cc148-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veritas Enterprise Vault.cloud SSO.</span></span>

![Assign User][200] 

<span data-ttu-id="cc148-214">**To assign Britta Simon to Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc148-214">**To assign Britta Simon to Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="cc148-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc148-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cc148-217">In the applications list, select **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="cc148-217">In the applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Configure Single Sign-On](./media/veritas-tutorial/tutorial_veritas_app.png) 

1. <span data-ttu-id="cc148-219">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cc148-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cc148-221">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cc148-221">Click **Add** button.</span></span> <span data-ttu-id="cc148-222">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc148-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cc148-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cc148-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cc148-225">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc148-225">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cc148-226">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc148-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc148-227">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc148-227">Testing single sign-on</span></span>

<span data-ttu-id="cc148-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cc148-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc148-229">When you click the Veritas Enterprise Vault.cloud SSO tile in the Access Panel, you should get automatically signed-on to your Veritas Enterprise Vault.cloud SSO application.</span><span class="sxs-lookup"><span data-stu-id="cc148-229">When you click the Veritas Enterprise Vault.cloud SSO tile in the Access Panel, you should get automatically signed-on to your Veritas Enterprise Vault.cloud SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc148-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cc148-230">Additional resources</span></span>

* [<span data-ttu-id="cc148-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc148-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cc148-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc148-232">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/veritas-tutorial/tutorial_general_01.png
[2]: ./media/veritas-tutorial/tutorial_general_02.png
[3]: ./media/veritas-tutorial/tutorial_general_03.png
[4]: ./media/veritas-tutorial/tutorial_general_04.png

[100]: ./media/veritas-tutorial/tutorial_general_100.png

[200]: ./media/veritas-tutorial/tutorial_general_200.png
[201]: ./media/veritas-tutorial/tutorial_general_201.png
[202]: ./media/veritas-tutorial/tutorial_general_202.png
[203]: ./media/veritas-tutorial/tutorial_general_203.png

