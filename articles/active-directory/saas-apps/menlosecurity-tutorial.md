---
title: 'Tutorial: Azure Active Directory integration with Menlo Security | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Menlo Security.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: a1f7458d52ffdee4cb48e4be0f553e3d57413249
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867135"
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="274ea-103">Tutorial: Azure Active Directory integration with Menlo Security</span><span class="sxs-lookup"><span data-stu-id="274ea-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="274ea-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="274ea-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="274ea-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="274ea-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="274ea-106">You can control in Azure AD who has access to Menlo Security</span><span class="sxs-lookup"><span data-stu-id="274ea-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="274ea-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="274ea-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="274ea-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="274ea-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="274ea-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="274ea-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="274ea-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="274ea-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="274ea-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="274ea-111">Prerequisites</span></span>

<span data-ttu-id="274ea-112">To configure Azure AD integration with Menlo Security, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="274ea-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="274ea-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="274ea-113">An Azure AD subscription</span></span>
- <span data-ttu-id="274ea-114">A Menlo Security single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="274ea-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="274ea-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="274ea-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="274ea-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="274ea-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="274ea-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="274ea-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="274ea-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="274ea-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="274ea-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="274ea-119">Scenario description</span></span>
<span data-ttu-id="274ea-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="274ea-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="274ea-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="274ea-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="274ea-122">Adding Menlo Security from the gallery</span><span class="sxs-lookup"><span data-stu-id="274ea-122">Adding Menlo Security from the gallery</span></span>
1. <span data-ttu-id="274ea-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="274ea-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="274ea-124">Adding Menlo Security from the gallery</span><span class="sxs-lookup"><span data-stu-id="274ea-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="274ea-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="274ea-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="274ea-126">**To add Menlo Security from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="274ea-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="274ea-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="274ea-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="274ea-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="274ea-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="274ea-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="274ea-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="274ea-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="274ea-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="274ea-134">In the search box, type **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="274ea-134">In the search box, type **Menlo Security**.</span></span>

    ![Creating an Azure AD test user](./media/menlosecurity-tutorial/tutorial_menlosecurity_search.png)

1. <span data-ttu-id="274ea-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="274ea-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="274ea-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="274ea-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="274ea-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="274ea-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="274ea-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="274ea-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="274ea-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span><span class="sxs-lookup"><span data-stu-id="274ea-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="274ea-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="274ea-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="274ea-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="274ea-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="274ea-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="274ea-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="274ea-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="274ea-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="274ea-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="274ea-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="274ea-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="274ea-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="274ea-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="274ea-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="274ea-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="274ea-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="274ea-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span><span class="sxs-lookup"><span data-stu-id="274ea-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="274ea-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="274ea-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="274ea-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="274ea-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="274ea-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="274ea-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

1. <span data-ttu-id="274ea-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="274ea-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="274ea-158">a.</span><span class="sxs-lookup"><span data-stu-id="274ea-158">a.</span></span> <span data-ttu-id="274ea-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="274ea-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="274ea-160">b.</span><span class="sxs-lookup"><span data-stu-id="274ea-160">b.</span></span> <span data-ttu-id="274ea-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="274ea-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="274ea-162">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="274ea-162">These values are not the real.</span></span> <span data-ttu-id="274ea-163">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="274ea-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="274ea-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="274ea-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
1. <span data-ttu-id="274ea-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="274ea-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

1. <span data-ttu-id="274ea-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="274ea-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/menlosecurity-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="274ea-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="274ea-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="274ea-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="274ea-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

1. <span data-ttu-id="274ea-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span><span class="sxs-lookup"><span data-stu-id="274ea-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

1. <span data-ttu-id="274ea-173">Under **Settings** go to **Authentication** and perform following actions:</span><span class="sxs-lookup"><span data-stu-id="274ea-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Configure Single Sign-On](./media/menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="274ea-175">a.</span><span class="sxs-lookup"><span data-stu-id="274ea-175">a.</span></span> <span data-ttu-id="274ea-176">Tick the checkbox **Enable user authentication using SAML**.</span><span class="sxs-lookup"><span data-stu-id="274ea-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="274ea-177">b.</span><span class="sxs-lookup"><span data-stu-id="274ea-177">b.</span></span> <span data-ttu-id="274ea-178">Select **Allow External Access** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="274ea-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="274ea-179">c.</span><span class="sxs-lookup"><span data-stu-id="274ea-179">c.</span></span> <span data-ttu-id="274ea-180">Under **SAML Provider**, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="274ea-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="274ea-181">d.</span><span class="sxs-lookup"><span data-stu-id="274ea-181">d.</span></span> <span data-ttu-id="274ea-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="274ea-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="274ea-183">e.</span><span class="sxs-lookup"><span data-stu-id="274ea-183">e.</span></span> <span data-ttu-id="274ea-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="274ea-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="274ea-185">f.</span><span class="sxs-lookup"><span data-stu-id="274ea-185">f.</span></span> <span data-ttu-id="274ea-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span><span class="sxs-lookup"><span data-stu-id="274ea-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="274ea-187">g.</span><span class="sxs-lookup"><span data-stu-id="274ea-187">g.</span></span> <span data-ttu-id="274ea-188">Click **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="274ea-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="274ea-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="274ea-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="274ea-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="274ea-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="274ea-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="274ea-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="274ea-192">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="274ea-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="274ea-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="274ea-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="274ea-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="274ea-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="274ea-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="274ea-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/menlosecurity-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="274ea-198">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="274ea-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/menlosecurity-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="274ea-200">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="274ea-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/menlosecurity-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="274ea-202">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="274ea-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="274ea-204">a.</span><span class="sxs-lookup"><span data-stu-id="274ea-204">a.</span></span> <span data-ttu-id="274ea-205">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="274ea-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="274ea-206">b.</span><span class="sxs-lookup"><span data-stu-id="274ea-206">b.</span></span> <span data-ttu-id="274ea-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="274ea-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="274ea-208">c.</span><span class="sxs-lookup"><span data-stu-id="274ea-208">c.</span></span> <span data-ttu-id="274ea-209">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="274ea-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="274ea-210">d.</span><span class="sxs-lookup"><span data-stu-id="274ea-210">d.</span></span> <span data-ttu-id="274ea-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="274ea-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="274ea-212">Creating a Menlo Security test user</span><span class="sxs-lookup"><span data-stu-id="274ea-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="274ea-213">In this section, you create a user called Britta Simon in Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="274ea-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="274ea-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span><span class="sxs-lookup"><span data-stu-id="274ea-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="274ea-215">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="274ea-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="274ea-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="274ea-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="274ea-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="274ea-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Assign User][200] 

<span data-ttu-id="274ea-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="274ea-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="274ea-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="274ea-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="274ea-222">In the applications list, select **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="274ea-222">In the applications list, select **Menlo Security**.</span></span>

    ![Configure Single Sign-On](./media/menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

1. <span data-ttu-id="274ea-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="274ea-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="274ea-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="274ea-226">Click **Add** button.</span></span> <span data-ttu-id="274ea-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="274ea-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="274ea-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="274ea-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="274ea-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="274ea-230">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="274ea-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="274ea-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="274ea-232">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="274ea-232">Testing single sign-on</span></span>

<span data-ttu-id="274ea-233">In this section, you test your Azure AD single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="274ea-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="274ea-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span><span class="sxs-lookup"><span data-stu-id="274ea-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="274ea-235">In Internet Explorer, use Ctrl+Shift+P.</span><span class="sxs-lookup"><span data-stu-id="274ea-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="274ea-236">In Chrome, use Ctrl+Shift+N.</span><span class="sxs-lookup"><span data-stu-id="274ea-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="274ea-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span><span class="sxs-lookup"><span data-stu-id="274ea-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="274ea-238">Upon successful login, you will be taken to the requested site in an isolation session.</span><span class="sxs-lookup"><span data-stu-id="274ea-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="274ea-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="274ea-239">Additional resources</span></span>

* [<span data-ttu-id="274ea-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="274ea-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="274ea-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="274ea-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/menlosecurity-tutorial/tutorial_general_203.png

