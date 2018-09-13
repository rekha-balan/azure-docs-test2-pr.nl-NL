---
title: 'Tutorial: Azure Active Directory integration with HappyFox | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HappyFox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 95def1ce278b0a816f19e3cd4e1b47bd3f68f1a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968342"
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="0a5cd-103">Tutorial: Azure Active Directory integration with HappyFox</span><span class="sxs-lookup"><span data-stu-id="0a5cd-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="0a5cd-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a5cd-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a5cd-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a5cd-106">You can control in Azure AD who has access to HappyFox</span><span class="sxs-lookup"><span data-stu-id="0a5cd-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="0a5cd-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0a5cd-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a5cd-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0a5cd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a5cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0a5cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a5cd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a5cd-110">Prerequisites</span></span>

<span data-ttu-id="0a5cd-111">To configure Azure AD integration with HappyFox, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="0a5cd-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0a5cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a5cd-113">A HappyFox single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0a5cd-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a5cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a5cd-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a5cd-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a5cd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a5cd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a5cd-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0a5cd-118">Scenario description</span></span>
<span data-ttu-id="0a5cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a5cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a5cd-121">Adding HappyFox from the gallery</span><span class="sxs-lookup"><span data-stu-id="0a5cd-121">Adding HappyFox from the gallery</span></span>
1. <span data-ttu-id="0a5cd-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="0a5cd-123">Adding HappyFox from the gallery</span><span class="sxs-lookup"><span data-stu-id="0a5cd-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="0a5cd-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a5cd-125">**To add HappyFox from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5cd-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="0a5cd-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a5cd-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="0a5cd-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0a5cd-133">In the search box, type **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-133">In the search box, type **HappyFox**.</span></span>

    ![Creating an Azure AD test user](./media/happyfox-tutorial/tutorial_happyfox_search.png)

1. <span data-ttu-id="0a5cd-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a5cd-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5cd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a5cd-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0a5cd-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a5cd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="0a5cd-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="0a5cd-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a5cd-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a5cd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0a5cd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0a5cd-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0a5cd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0a5cd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a5cd-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5cd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a5cd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="0a5cd-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5cd-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5cd-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0a5cd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/happyfox-tutorial/tutorial_happyfox_samlbase.png)

1. <span data-ttu-id="0a5cd-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="0a5cd-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-157">a.</span></span> <span data-ttu-id="0a5cd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="0a5cd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="0a5cd-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-159">b.</span></span> <span data-ttu-id="0a5cd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="0a5cd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a5cd-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-161">These values are not real.</span></span> <span data-ttu-id="0a5cd-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0a5cd-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
1. <span data-ttu-id="0a5cd-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/tutorial_happyfox_certificate.png) 

1. <span data-ttu-id="0a5cd-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0a5cd-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a5cd-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/tutorial_happyfox_configure.png) 

1. <span data-ttu-id="0a5cd-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/header.png) 

1. <span data-ttu-id="0a5cd-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/configure.png) 

1. <span data-ttu-id="0a5cd-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/targeturl.png)

1. <span data-ttu-id="0a5cd-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configure Single Sign-On](./media/happyfox-tutorial/cert.png)

1. <span data-ttu-id="0a5cd-179">Click **Save Settings** button.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-179">Click **Save Settings** button.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="0a5cd-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0a5cd-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a5cd-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a5cd-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a5cd-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a5cd-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0a5cd-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a5cd-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0a5cd-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5cd-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5cd-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/happyfox-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="0a5cd-190">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/happyfox-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="0a5cd-192">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/happyfox-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="0a5cd-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5cd-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a5cd-196">a.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-196">a.</span></span> <span data-ttu-id="0a5cd-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a5cd-198">b.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-198">b.</span></span> <span data-ttu-id="0a5cd-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a5cd-200">c.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-200">c.</span></span> <span data-ttu-id="0a5cd-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a5cd-202">d.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-202">d.</span></span> <span data-ttu-id="0a5cd-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="0a5cd-204">Creating a HappyFox test user</span><span class="sxs-lookup"><span data-stu-id="0a5cd-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="0a5cd-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a5cd-206">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0a5cd-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a5cd-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Assign User][200] 

<span data-ttu-id="0a5cd-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5cd-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5cd-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0a5cd-212">In the applications list, select **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-212">In the applications list, select **HappyFox**.</span></span>

    ![Configure Single Sign-On](./media/happyfox-tutorial/tutorial_happyfox_app.png) 

1. <span data-ttu-id="0a5cd-214">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="0a5cd-216">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-216">Click **Add** button.</span></span> <span data-ttu-id="0a5cd-217">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0a5cd-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0a5cd-220">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-220">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0a5cd-221">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a5cd-222">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5cd-222">Testing single sign-on</span></span>

<span data-ttu-id="0a5cd-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="0a5cd-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="0a5cd-225">You should see the **‘SAML’** button on the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Plugin](./media/happyfox-tutorial/saml.png) 

1. <span data-ttu-id="0a5cd-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="0a5cd-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="0a5cd-228">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a5cd-228">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0a5cd-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0a5cd-229">Additional resources</span></span>

* [<span data-ttu-id="0a5cd-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a5cd-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0a5cd-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a5cd-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/happyfox-tutorial/tutorial_general_01.png
[2]: ./media/happyfox-tutorial/tutorial_general_02.png
[3]: ./media/happyfox-tutorial/tutorial_general_03.png
[4]: ./media/happyfox-tutorial/tutorial_general_04.png

[100]: ./media/happyfox-tutorial/tutorial_general_100.png

[200]: ./media/happyfox-tutorial/tutorial_general_200.png
[201]: ./media/happyfox-tutorial/tutorial_general_201.png
[202]: ./media/happyfox-tutorial/tutorial_general_202.png
[203]: ./media/happyfox-tutorial/tutorial_general_203.png

