---
title: 'Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Confluence SAML SSO by Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 856809d6eb480d0112eb7ed85c33560950be7d64
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855793"
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="cee56-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="cee56-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="cee56-104">In this tutorial, you learn how to integrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cee56-104">In this tutorial, you learn how to integrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cee56-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cee56-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cee56-106">You can control in Azure AD who has access to Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="cee56-106">You can control in Azure AD who has access to Confluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="cee56-107">You can enable your users to automatically get signed-on to Confluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cee56-107">You can enable your users to automatically get signed-on to Confluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cee56-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cee56-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cee56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cee56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="description"></a><span data-ttu-id="cee56-110">Description:</span><span class="sxs-lookup"><span data-stu-id="cee56-110">Description:</span></span>

<span data-ttu-id="cee56-111">Use your Microsoft Azure Active Directory account with Atlassian Confluence server to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cee56-111">Use your Microsoft Azure Active Directory account with Atlassian Confluence server to enable single sign-on.</span></span> <span data-ttu-id="cee56-112">This way all your organization users can use the Azure AD credentials to login into the Confluence application.</span><span class="sxs-lookup"><span data-stu-id="cee56-112">This way all your organization users can use the Azure AD credentials to login into the Confluence application.</span></span> <span data-ttu-id="cee56-113">This plugin uses SAML 2.0 for federation.</span><span class="sxs-lookup"><span data-stu-id="cee56-113">This plugin uses SAML 2.0 for federation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cee56-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cee56-114">Prerequisites</span></span>

<span data-ttu-id="cee56-115">To configure Azure AD integration with Confluence SAML SSO by Microsoft, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cee56-115">To configure Azure AD integration with Confluence SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="cee56-116">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cee56-116">An Azure AD subscription</span></span>
- <span data-ttu-id="cee56-117">Confluence server application installed on a Windows 64-bit server (on-premises or on the cloud IaaS infrastructure)</span><span class="sxs-lookup"><span data-stu-id="cee56-117">Confluence server application installed on a Windows 64-bit server (on-premises or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="cee56-118">Confluence server is HTTPS enabled</span><span class="sxs-lookup"><span data-stu-id="cee56-118">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="cee56-119">Note the supported versions for Confluence Plugin are mentioned in below section.</span><span class="sxs-lookup"><span data-stu-id="cee56-119">Note the supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="cee56-120">Confluence server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span><span class="sxs-lookup"><span data-stu-id="cee56-120">Confluence server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="cee56-121">Admin credentials are set up in Confluence</span><span class="sxs-lookup"><span data-stu-id="cee56-121">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="cee56-122">WebSudo is disabled in Confluence</span><span class="sxs-lookup"><span data-stu-id="cee56-122">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="cee56-123">Test user created in the Confluence server application</span><span class="sxs-lookup"><span data-stu-id="cee56-123">Test user created in the Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="cee56-124">To test the steps in this tutorial, we do not recommend using a production environment of Confluence.</span><span class="sxs-lookup"><span data-stu-id="cee56-124">To test the steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="cee56-125">Test the integration first in development or staging environment of the application and then use the production environment.</span><span class="sxs-lookup"><span data-stu-id="cee56-125">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="cee56-126">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cee56-126">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cee56-127">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cee56-127">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cee56-128">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cee56-128">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="cee56-129">Supported versions of Confluence</span><span class="sxs-lookup"><span data-stu-id="cee56-129">Supported versions of Confluence</span></span> 

<span data-ttu-id="cee56-130">As of now, following versions of Confluence are supported:</span><span class="sxs-lookup"><span data-stu-id="cee56-130">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="cee56-131">Confluence: 5.0 to 5.10</span><span class="sxs-lookup"><span data-stu-id="cee56-131">Confluence: 5.0 to 5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cee56-132">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cee56-132">Scenario description</span></span>
<span data-ttu-id="cee56-133">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cee56-133">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cee56-134">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cee56-134">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cee56-135">Adding Confluence SAML SSO by Microsoft from the gallery</span><span class="sxs-lookup"><span data-stu-id="cee56-135">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
1. <span data-ttu-id="cee56-136">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cee56-136">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="cee56-137">Adding Confluence SAML SSO by Microsoft from the gallery</span><span class="sxs-lookup"><span data-stu-id="cee56-137">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="cee56-138">To configure the integration of Confluence SAML SSO by Microsoft into Azure AD, you need to add Confluence SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cee56-138">To configure the integration of Confluence SAML SSO by Microsoft into Azure AD, you need to add Confluence SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cee56-139">**To add Confluence SAML SSO by Microsoft from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cee56-139">**To add Confluence SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cee56-140">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cee56-140">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cee56-142">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cee56-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cee56-143">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cee56-143">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cee56-145">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cee56-145">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cee56-147">In the search box, type **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cee56-147">In the search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Creating an Azure AD test user](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

1. <span data-ttu-id="cee56-149">In the results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cee56-149">In the results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cee56-151">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cee56-151">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cee56-152">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cee56-152">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cee56-153">For single sign-on to work, Azure AD needs to know what the counterpart user in Confluence SAML SSO by Microsoft is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cee56-153">For single sign-on to work, Azure AD needs to know what the counterpart user in Confluence SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="cee56-154">In other words, a link relationship between an Azure AD user and the related user in Confluence SAML SSO by Microsoft needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cee56-154">In other words, a link relationship between an Azure AD user and the related user in Confluence SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="cee56-155">To configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cee56-155">To configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cee56-156">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cee56-156">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cee56-157">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cee56-157">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cee56-158">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cee56-158">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cee56-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cee56-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cee56-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cee56-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cee56-161">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cee56-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cee56-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="cee56-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="cee56-163">**To configure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cee56-163">**To configure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="cee56-164">In the Azure portal, on the **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cee56-164">In the Azure portal, on the **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cee56-166">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cee56-166">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

1. <span data-ttu-id="cee56-168">On the **Confluence SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cee56-168">On the **Confluence SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="cee56-170">a.</span><span class="sxs-lookup"><span data-stu-id="cee56-170">a.</span></span> <span data-ttu-id="cee56-171">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="cee56-171">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="cee56-172">b.</span><span class="sxs-lookup"><span data-stu-id="cee56-172">b.</span></span> <span data-ttu-id="cee56-173">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="cee56-173">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="cee56-174">c.</span><span class="sxs-lookup"><span data-stu-id="cee56-174">c.</span></span> <span data-ttu-id="cee56-175">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="cee56-175">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE]
    > <span data-ttu-id="cee56-176">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="cee56-176">These values are not real.</span></span> <span data-ttu-id="cee56-177">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="cee56-177">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cee56-178">Port is optional in case it’s a named URL.</span><span class="sxs-lookup"><span data-stu-id="cee56-178">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="cee56-179">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="cee56-179">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="cee56-180">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="cee56-180">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/tutorial_metadataurl.png)
     
1. <span data-ttu-id="cee56-182">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cee56-182">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cee56-184">In a different web browser window, log in to your Confluence instance as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cee56-184">In a different web browser window, log in to your Confluence instance as an administrator.</span></span>

1. <span data-ttu-id="cee56-185">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="cee56-185">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/addon1.png)

1. <span data-ttu-id="cee56-187">Download the plugin from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56503).</span><span class="sxs-lookup"><span data-stu-id="cee56-187">Download the plugin from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56503).</span></span> <span data-ttu-id="cee56-188">Manually upload the plugin provided by Microsoft using **Upload add-on** menu.</span><span class="sxs-lookup"><span data-stu-id="cee56-188">Manually upload the plugin provided by Microsoft using **Upload add-on** menu.</span></span> <span data-ttu-id="cee56-189">The download of plugin is covered under [Microsoft Service Agreement](https://www.microsoft.com/servicesagreement/).</span><span class="sxs-lookup"><span data-stu-id="cee56-189">The download of plugin is covered under [Microsoft Service Agreement](https://www.microsoft.com/servicesagreement/).</span></span> 
    
    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/addon12.png)

1. <span data-ttu-id="cee56-191">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span><span class="sxs-lookup"><span data-stu-id="cee56-191">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span> <span data-ttu-id="cee56-192">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="cee56-192">Click **Configure** to configure the new plugin.</span></span>
    
    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/addon13.png)

1. <span data-ttu-id="cee56-194">Perform following steps on configuration page:</span><span class="sxs-lookup"><span data-stu-id="cee56-194">Perform following steps on configuration page:</span></span>

    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/addon52.png)

    > [!TIP]
    > <span data-ttu-id="cee56-196">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span><span class="sxs-lookup"><span data-stu-id="cee56-196">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="cee56-197">If there are multiple certificates, admin gets an error upon resolving the metadata.</span><span class="sxs-lookup"><span data-stu-id="cee56-197">If there are multiple certificates, admin gets an error upon resolving the metadata.</span></span>

    <span data-ttu-id="cee56-198">a.</span><span class="sxs-lookup"><span data-stu-id="cee56-198">a.</span></span> <span data-ttu-id="cee56-199">In the **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal and click the **Resolve** button.</span><span class="sxs-lookup"><span data-stu-id="cee56-199">In the **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal and click the **Resolve** button.</span></span> <span data-ttu-id="cee56-200">It reads the IdP metadata URL and populates all the fields information.</span><span class="sxs-lookup"><span data-stu-id="cee56-200">It reads the IdP metadata URL and populates all the fields information.</span></span>

    <span data-ttu-id="cee56-201">b.</span><span class="sxs-lookup"><span data-stu-id="cee56-201">b.</span></span> <span data-ttu-id="cee56-202">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cee56-202">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="cee56-203">c.</span><span class="sxs-lookup"><span data-stu-id="cee56-203">c.</span></span> <span data-ttu-id="cee56-204">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span><span class="sxs-lookup"><span data-stu-id="cee56-204">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="cee56-205">d.</span><span class="sxs-lookup"><span data-stu-id="cee56-205">d.</span></span> <span data-ttu-id="cee56-206">In **SAML User ID Locations**, select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span><span class="sxs-lookup"><span data-stu-id="cee56-206">In **SAML User ID Locations**, select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="cee56-207">This ID has to be the Confluence user id. If the user id is not matched, then system will not allow users to log in.</span><span class="sxs-lookup"><span data-stu-id="cee56-207">This ID has to be the Confluence user id. If the user id is not matched, then system will not allow users to log in.</span></span> 

    > [!Note]
    > <span data-ttu-id="cee56-208">Default SAML User ID location is Name Identifier.</span><span class="sxs-lookup"><span data-stu-id="cee56-208">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="cee56-209">You can change this to an attribute option and enter the appropriate attribute name.</span><span class="sxs-lookup"><span data-stu-id="cee56-209">You can change this to an attribute option and enter the appropriate attribute name.</span></span>
    
    <span data-ttu-id="cee56-210">e.</span><span class="sxs-lookup"><span data-stu-id="cee56-210">e.</span></span> <span data-ttu-id="cee56-211">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span><span class="sxs-lookup"><span data-stu-id="cee56-211">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="cee56-212">f.</span><span class="sxs-lookup"><span data-stu-id="cee56-212">f.</span></span> <span data-ttu-id="cee56-213">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="cee56-213">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="cee56-214">g.</span><span class="sxs-lookup"><span data-stu-id="cee56-214">g.</span></span> <span data-ttu-id="cee56-215">In **Domain Name** type the domain name here in case of the ADFS-based login.</span><span class="sxs-lookup"><span data-stu-id="cee56-215">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="cee56-216">h.</span><span class="sxs-lookup"><span data-stu-id="cee56-216">h.</span></span> <span data-ttu-id="cee56-217">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from Confluence.</span><span class="sxs-lookup"><span data-stu-id="cee56-217">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="cee56-218">i.</span><span class="sxs-lookup"><span data-stu-id="cee56-218">i.</span></span> <span data-ttu-id="cee56-219">Click **Save** button to save the settings.</span><span class="sxs-lookup"><span data-stu-id="cee56-219">Click **Save** button to save the settings.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cee56-220">For more information about installation and troubleshooting, visit [MS Confluence SSO Connector Admin Guide](../ms-confluence-jira-plugin-adminguide.md) and there is also [FAQ](../ms-confluence-jira-plugin-faq.md) for your assistance</span><span class="sxs-lookup"><span data-stu-id="cee56-220">For more information about installation and troubleshooting, visit [MS Confluence SSO Connector Admin Guide](../ms-confluence-jira-plugin-adminguide.md) and there is also [FAQ](../ms-confluence-jira-plugin-faq.md) for your assistance</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cee56-221">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cee56-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="cee56-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cee56-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cee56-224">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cee56-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cee56-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cee56-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/confluencemicrosoft-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cee56-227">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cee56-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/confluencemicrosoft-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cee56-229">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cee56-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/confluencemicrosoft-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cee56-231">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cee56-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cee56-233">a.</span><span class="sxs-lookup"><span data-stu-id="cee56-233">a.</span></span> <span data-ttu-id="cee56-234">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cee56-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cee56-235">b.</span><span class="sxs-lookup"><span data-stu-id="cee56-235">b.</span></span> <span data-ttu-id="cee56-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cee56-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cee56-237">c.</span><span class="sxs-lookup"><span data-stu-id="cee56-237">c.</span></span> <span data-ttu-id="cee56-238">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cee56-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cee56-239">d.</span><span class="sxs-lookup"><span data-stu-id="cee56-239">d.</span></span> <span data-ttu-id="cee56-240">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cee56-240">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="cee56-241">Creating a Confluence SAML SSO by Microsoft test user</span><span class="sxs-lookup"><span data-stu-id="cee56-241">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="cee56-242">To enable Azure AD users to log in to Confluence on-premises server, they must be provisioned into Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cee56-242">To enable Azure AD users to log in to Confluence on-premises server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="cee56-243">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="cee56-243">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="cee56-244">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cee56-244">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cee56-245">Log in to your Confluence on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cee56-245">Log in to your Confluence on-premises server as an administrator.</span></span>

1. <span data-ttu-id="cee56-246">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="cee56-246">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/confluencemicrosoft-tutorial/user1.png) 

1. <span data-ttu-id="cee56-248">Under Users section, click **Add users** tab. On the **Add a User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cee56-248">Under Users section, click **Add users** tab. On the **Add a User** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="cee56-250">a.</span><span class="sxs-lookup"><span data-stu-id="cee56-250">a.</span></span> <span data-ttu-id="cee56-251">In the **Username** textbox, type the email of user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cee56-251">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="cee56-252">b.</span><span class="sxs-lookup"><span data-stu-id="cee56-252">b.</span></span> <span data-ttu-id="cee56-253">In the **Full Name** textbox, type the full name of user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cee56-253">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="cee56-254">c.</span><span class="sxs-lookup"><span data-stu-id="cee56-254">c.</span></span> <span data-ttu-id="cee56-255">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cee56-255">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="cee56-256">d.</span><span class="sxs-lookup"><span data-stu-id="cee56-256">d.</span></span> <span data-ttu-id="cee56-257">In the **Password** textbox, type the password for Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cee56-257">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="cee56-258">e.</span><span class="sxs-lookup"><span data-stu-id="cee56-258">e.</span></span> <span data-ttu-id="cee56-259">Click **Confirm Password** reenter the password.</span><span class="sxs-lookup"><span data-stu-id="cee56-259">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="cee56-260">f.</span><span class="sxs-lookup"><span data-stu-id="cee56-260">f.</span></span> <span data-ttu-id="cee56-261">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cee56-261">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cee56-262">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cee56-262">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cee56-263">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cee56-263">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Confluence SAML SSO by Microsoft.</span></span>

![Assign User][200] 

<span data-ttu-id="cee56-265">**To assign Britta Simon to Confluence SAML SSO by Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cee56-265">**To assign Britta Simon to Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="cee56-266">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cee56-266">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cee56-268">In the applications list, select **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cee56-268">In the applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Configure Single Sign-On](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

1. <span data-ttu-id="cee56-270">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cee56-270">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cee56-272">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cee56-272">Click **Add** button.</span></span> <span data-ttu-id="cee56-273">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cee56-273">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cee56-275">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cee56-275">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cee56-276">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cee56-276">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cee56-277">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cee56-277">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cee56-278">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cee56-278">Testing single sign-on</span></span>

<span data-ttu-id="cee56-279">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cee56-279">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cee56-280">When you click the Confluence SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your Confluence SAML SSO by Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="cee56-280">When you click the Confluence SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="cee56-281">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cee56-281">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cee56-282">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cee56-282">Additional resources</span></span>

* [<span data-ttu-id="cee56-283">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cee56-283">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cee56-284">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cee56-284">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/confluencemicrosoft-tutorial/tutorial_general_203.png
