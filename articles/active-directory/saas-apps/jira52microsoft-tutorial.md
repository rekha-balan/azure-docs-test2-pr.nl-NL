---
title: 'Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft (V5.2) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and JIRA SAML SSO by Microsoft (V5.2).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d0c00408-f9b8-4a79-bccc-c346a7331845
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: jeedes
ms.openlocfilehash: d7f53efd4b473f36aa03628da4992d1c4c2fb04b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865214"
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft-v52"></a><span data-ttu-id="8bf67-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft (V5.2)</span><span class="sxs-lookup"><span data-stu-id="8bf67-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft (V5.2)</span></span>

<span data-ttu-id="8bf67-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft (V5.2) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8bf67-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft (V5.2) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bf67-105">Integrating JIRA SAML SSO by Microsoft (V5.2) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8bf67-105">Integrating JIRA SAML SSO by Microsoft (V5.2) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8bf67-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft (V5.2).</span><span class="sxs-lookup"><span data-stu-id="8bf67-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft (V5.2).</span></span>
- <span data-ttu-id="8bf67-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (V5.2) (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8bf67-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (V5.2) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8bf67-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8bf67-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8bf67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8bf67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="description"></a><span data-ttu-id="8bf67-110">Description</span><span class="sxs-lookup"><span data-stu-id="8bf67-110">Description</span></span>

<span data-ttu-id="8bf67-111">Use your Microsoft Azure Active Directory account with Atlassian JIRA server to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8bf67-111">Use your Microsoft Azure Active Directory account with Atlassian JIRA server to enable single sign-on.</span></span> <span data-ttu-id="8bf67-112">This way all your organization users can use the Azure AD credentials to login into the JIRA application.</span><span class="sxs-lookup"><span data-stu-id="8bf67-112">This way all your organization users can use the Azure AD credentials to login into the JIRA application.</span></span> <span data-ttu-id="8bf67-113">This plugin uses SAML 2.0 for federation.</span><span class="sxs-lookup"><span data-stu-id="8bf67-113">This plugin uses SAML 2.0 for federation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bf67-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8bf67-114">Prerequisites</span></span>

<span data-ttu-id="8bf67-115">To configure Azure AD integration with JIRA SAML SSO by Microsoft (V5.2), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8bf67-115">To configure Azure AD integration with JIRA SAML SSO by Microsoft (V5.2), you need the following items:</span></span>

- <span data-ttu-id="8bf67-116">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8bf67-116">An Azure AD subscription</span></span>
- <span data-ttu-id="8bf67-117">JIRA Core and Software 5.2 should installed and configured on Windows 64-bit version</span><span class="sxs-lookup"><span data-stu-id="8bf67-117">JIRA Core and Software 5.2 should installed and configured on Windows 64-bit version</span></span>
- <span data-ttu-id="8bf67-118">JIRA server is HTTPS enabled</span><span class="sxs-lookup"><span data-stu-id="8bf67-118">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="8bf67-119">Note the supported versions for JIRA Plugin are mentioned in below section.</span><span class="sxs-lookup"><span data-stu-id="8bf67-119">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="8bf67-120">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bf67-120">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="8bf67-121">Admin credentials are set up in JIRA</span><span class="sxs-lookup"><span data-stu-id="8bf67-121">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="8bf67-122">WebSudo is disabled in JIRA</span><span class="sxs-lookup"><span data-stu-id="8bf67-122">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="8bf67-123">Test user created in the JIRA server application</span><span class="sxs-lookup"><span data-stu-id="8bf67-123">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="8bf67-124">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span><span class="sxs-lookup"><span data-stu-id="8bf67-124">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="8bf67-125">Test the integration first in development or staging environment of the application and then use the production environment.</span><span class="sxs-lookup"><span data-stu-id="8bf67-125">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="8bf67-126">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8bf67-126">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bf67-127">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8bf67-127">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bf67-128">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bf67-128">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="8bf67-129">**Supported Versions:**</span><span class="sxs-lookup"><span data-stu-id="8bf67-129">**Supported Versions:**</span></span>

*   <span data-ttu-id="8bf67-130">JIRA Core and Software: 5.2</span><span class="sxs-lookup"><span data-stu-id="8bf67-130">JIRA Core and Software: 5.2</span></span>
*   <span data-ttu-id="8bf67-131">JIRA also supports 6.0 and 7.8.</span><span class="sxs-lookup"><span data-stu-id="8bf67-131">JIRA also supports 6.0 and 7.8.</span></span> <span data-ttu-id="8bf67-132">For more details, click [JIRA SAML SSO by Microsoft](jiramicrosoft-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="8bf67-132">For more details, click [JIRA SAML SSO by Microsoft](jiramicrosoft-tutorial.md)</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bf67-133">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8bf67-133">Scenario description</span></span>
<span data-ttu-id="8bf67-134">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8bf67-134">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="8bf67-135">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8bf67-135">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bf67-136">Adding JIRA SAML SSO by Microsoft (V5.2) from the gallery</span><span class="sxs-lookup"><span data-stu-id="8bf67-136">Adding JIRA SAML SSO by Microsoft (V5.2) from the gallery</span></span>
2. <span data-ttu-id="8bf67-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8bf67-137">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-v52-from-the-gallery"></a><span data-ttu-id="8bf67-138">Adding JIRA SAML SSO by Microsoft (V5.2) from the gallery</span><span class="sxs-lookup"><span data-stu-id="8bf67-138">Adding JIRA SAML SSO by Microsoft (V5.2) from the gallery</span></span>
<span data-ttu-id="8bf67-139">To configure the integration of JIRA SAML SSO by Microsoft (V5.2) into Azure AD, you need to add JIRA SAML SSO by Microsoft (V5.2) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8bf67-139">To configure the integration of JIRA SAML SSO by Microsoft (V5.2) into Azure AD, you need to add JIRA SAML SSO by Microsoft (V5.2) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8bf67-140">**To add JIRA SAML SSO by Microsoft (V5.2) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8bf67-140">**To add JIRA SAML SSO by Microsoft (V5.2) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf67-141">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8bf67-141">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="8bf67-143">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-143">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8bf67-144">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-144">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="8bf67-146">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8bf67-146">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="8bf67-148">In the search box, type **JIRA SAML SSO by Microsoft (V5.2)**, select **JIRA SAML SSO by Microsoft (V5.2)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8bf67-148">In the search box, type **JIRA SAML SSO by Microsoft (V5.2)**, select **JIRA SAML SSO by Microsoft (V5.2)** from result panel then click **Add** button to add the application.</span></span>

    ![JIRA SAML SSO by Microsoft (V5.2) in the results list](./media/jira52microsoft-tutorial/tutorial_singlesign-onforjira5.2_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8bf67-150">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8bf67-150">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8bf67-151">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft (V5.2) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8bf67-151">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft (V5.2) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8bf67-152">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft (V5.2) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bf67-152">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft (V5.2) is to a user in Azure AD.</span></span> <span data-ttu-id="8bf67-153">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft (V5.2) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8bf67-153">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft (V5.2) needs to be established.</span></span>

<span data-ttu-id="8bf67-154">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft (V5.2), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8bf67-154">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft (V5.2), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8bf67-155">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8bf67-155">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8bf67-156">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bf67-156">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bf67-157">**[Create a JIRA SAML SSO by Microsoft (V5.2) test user](#create-a-jira-saml-sso-by-microsoft-v52-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft (V5.2) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8bf67-157">**[Create a JIRA SAML SSO by Microsoft (V5.2) test user](#create-a-jira-saml-sso-by-microsoft-v52-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft (V5.2) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bf67-158">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8bf67-158">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bf67-159">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8bf67-159">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8bf67-160">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8bf67-160">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8bf67-161">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft (V5.2) application.</span><span class="sxs-lookup"><span data-stu-id="8bf67-161">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft (V5.2) application.</span></span>

<span data-ttu-id="8bf67-162">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft (V5.2), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8bf67-162">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft (V5.2), perform the following steps:**</span></span>

1. <span data-ttu-id="8bf67-163">In the Azure portal, on the **JIRA SAML SSO by Microsoft (V5.2)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-163">In the Azure portal, on the **JIRA SAML SSO by Microsoft (V5.2)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="8bf67-165">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8bf67-165">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/jira52microsoft-tutorial/tutorial_singlesign-onforjira5.2_samlbase.png)

3. <span data-ttu-id="8bf67-167">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8bf67-167">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![JIRA SAML SSO by Microsoft Domain and URLs single sign-on information](./media/jira52microsoft-tutorial/tutorial_singlesign-onforjira5.2_url.png)

    <span data-ttu-id="8bf67-169">a.</span><span class="sxs-lookup"><span data-stu-id="8bf67-169">a.</span></span> <span data-ttu-id="8bf67-170">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="8bf67-170">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="8bf67-171">b.</span><span class="sxs-lookup"><span data-stu-id="8bf67-171">b.</span></span> <span data-ttu-id="8bf67-172">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="8bf67-172">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="8bf67-173">c.</span><span class="sxs-lookup"><span data-stu-id="8bf67-173">c.</span></span> <span data-ttu-id="8bf67-174">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="8bf67-174">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8bf67-175">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8bf67-175">These values are not real.</span></span> <span data-ttu-id="8bf67-176">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="8bf67-176">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8bf67-177">Port is optional in case it’s a named URL.</span><span class="sxs-lookup"><span data-stu-id="8bf67-177">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="8bf67-178">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="8bf67-178">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="8bf67-179">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="8bf67-179">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/tutorial_metadataurl.png)

5. <span data-ttu-id="8bf67-181">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8bf67-181">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bf67-183">In a different web browser window, log in to your JIRA instance as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8bf67-183">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

7. <span data-ttu-id="8bf67-184">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-184">Hover on cog and click the **Add-ons**.</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/addon1.png)

8. <span data-ttu-id="8bf67-186">Under Add-ons tab section, click **Manage add-ons**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-186">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/addon7.png)

9. <span data-ttu-id="8bf67-188">Download the plugin from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56521).</span><span class="sxs-lookup"><span data-stu-id="8bf67-188">Download the plugin from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56521).</span></span> <span data-ttu-id="8bf67-189">Manually upload the plugin provided by Microsoft using **Upload add-on** menu.</span><span class="sxs-lookup"><span data-stu-id="8bf67-189">Manually upload the plugin provided by Microsoft using **Upload add-on** menu.</span></span> <span data-ttu-id="8bf67-190">The download of plugin is covered under [Microsoft Service Agreement](https://www.microsoft.com/servicesagreement/).</span><span class="sxs-lookup"><span data-stu-id="8bf67-190">The download of plugin is covered under [Microsoft Service Agreement](https://www.microsoft.com/servicesagreement/).</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/addon12.png)

10. <span data-ttu-id="8bf67-192">Once the plugin is installed, it appears in **User Installed** add-ons section.</span><span class="sxs-lookup"><span data-stu-id="8bf67-192">Once the plugin is installed, it appears in **User Installed** add-ons section.</span></span> <span data-ttu-id="8bf67-193">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="8bf67-193">Click **Configure** to configure the new plugin.</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/addon13.png)

11. <span data-ttu-id="8bf67-195">Perform following steps on configuration page:</span><span class="sxs-lookup"><span data-stu-id="8bf67-195">Perform following steps on configuration page:</span></span>

    ![Configure Single Sign-On](./media/jira52microsoft-tutorial/addon52.png)

    > [!TIP]
    > <span data-ttu-id="8bf67-197">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span><span class="sxs-lookup"><span data-stu-id="8bf67-197">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="8bf67-198">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span><span class="sxs-lookup"><span data-stu-id="8bf67-198">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>

    <span data-ttu-id="8bf67-199">a.</span><span class="sxs-lookup"><span data-stu-id="8bf67-199">a.</span></span> <span data-ttu-id="8bf67-200">In **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal and click the **Resolve** button.</span><span class="sxs-lookup"><span data-stu-id="8bf67-200">In **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal and click the **Resolve** button.</span></span> <span data-ttu-id="8bf67-201">It reads the IdP metadata URL and populates all the fields information.</span><span class="sxs-lookup"><span data-stu-id="8bf67-201">It reads the IdP metadata URL and populates all the fields information.</span></span>

    <span data-ttu-id="8bf67-202">b.</span><span class="sxs-lookup"><span data-stu-id="8bf67-202">b.</span></span> <span data-ttu-id="8bf67-203">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft (V5.2) Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8bf67-203">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft (V5.2) Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="8bf67-204">c.</span><span class="sxs-lookup"><span data-stu-id="8bf67-204">c.</span></span> <span data-ttu-id="8bf67-205">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span><span class="sxs-lookup"><span data-stu-id="8bf67-205">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="8bf67-206">d.</span><span class="sxs-lookup"><span data-stu-id="8bf67-206">d.</span></span> <span data-ttu-id="8bf67-207">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-207">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="8bf67-208">This ID has to be the JIRA user id. If the user id is not matched, then system will not allow users to log in.</span><span class="sxs-lookup"><span data-stu-id="8bf67-208">This ID has to be the JIRA user id. If the user id is not matched, then system will not allow users to log in.</span></span>

    > [!Note]
    > <span data-ttu-id="8bf67-209">Default SAML User ID location is Name Identifier.</span><span class="sxs-lookup"><span data-stu-id="8bf67-209">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="8bf67-210">You can change this to an attribute option and enter the appropriate attribute name.</span><span class="sxs-lookup"><span data-stu-id="8bf67-210">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    <span data-ttu-id="8bf67-211">e.</span><span class="sxs-lookup"><span data-stu-id="8bf67-211">e.</span></span> <span data-ttu-id="8bf67-212">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span><span class="sxs-lookup"><span data-stu-id="8bf67-212">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="8bf67-213">f.</span><span class="sxs-lookup"><span data-stu-id="8bf67-213">f.</span></span> <span data-ttu-id="8bf67-214">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-214">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>

    <span data-ttu-id="8bf67-215">g.</span><span class="sxs-lookup"><span data-stu-id="8bf67-215">g.</span></span> <span data-ttu-id="8bf67-216">In **Domain Name** type the domain name here in case of the ADFS-based login.</span><span class="sxs-lookup"><span data-stu-id="8bf67-216">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="8bf67-217">h.</span><span class="sxs-lookup"><span data-stu-id="8bf67-217">h.</span></span> <span data-ttu-id="8bf67-218">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span><span class="sxs-lookup"><span data-stu-id="8bf67-218">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="8bf67-219">i.</span><span class="sxs-lookup"><span data-stu-id="8bf67-219">i.</span></span> <span data-ttu-id="8bf67-220">Click **Save** button to save the settings.</span><span class="sxs-lookup"><span data-stu-id="8bf67-220">Click **Save** button to save the settings.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8bf67-221">For more information about installation and troubleshooting, visit [MS JIRA SSO Connector Admin Guide](../ms-confluence-jira-plugin-adminguide.md) and there is also [FAQ](../ms-confluence-jira-plugin-faq.md) for your assistance</span><span class="sxs-lookup"><span data-stu-id="8bf67-221">For more information about installation and troubleshooting, visit [MS JIRA SSO Connector Admin Guide](../ms-confluence-jira-plugin-adminguide.md) and there is also [FAQ](../ms-confluence-jira-plugin-faq.md) for your assistance</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8bf67-222">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8bf67-222">Create an Azure AD test user</span></span>

<span data-ttu-id="8bf67-223">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bf67-223">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8bf67-225">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8bf67-225">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf67-226">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8bf67-226">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/jira52microsoft-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8bf67-228">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-228">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/jira52microsoft-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8bf67-230">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8bf67-230">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/jira52microsoft-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8bf67-232">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8bf67-232">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/jira52microsoft-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8bf67-234">a.</span><span class="sxs-lookup"><span data-stu-id="8bf67-234">a.</span></span> <span data-ttu-id="8bf67-235">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-235">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bf67-236">b.</span><span class="sxs-lookup"><span data-stu-id="8bf67-236">b.</span></span> <span data-ttu-id="8bf67-237">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bf67-237">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8bf67-238">c.</span><span class="sxs-lookup"><span data-stu-id="8bf67-238">c.</span></span> <span data-ttu-id="8bf67-239">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8bf67-239">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8bf67-240">d.</span><span class="sxs-lookup"><span data-stu-id="8bf67-240">d.</span></span> <span data-ttu-id="8bf67-241">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-241">Click **Create**.</span></span>

### <a name="create-a-jira-saml-sso-by-microsoft-v52-test-user"></a><span data-ttu-id="8bf67-242">Create a JIRA SAML SSO by Microsoft (V5.2) test user</span><span class="sxs-lookup"><span data-stu-id="8bf67-242">Create a JIRA SAML SSO by Microsoft (V5.2) test user</span></span>

<span data-ttu-id="8bf67-243">To enable Azure AD users to log in to JIRA on-premises server, they must be provisioned into JIRA on-premises server.</span><span class="sxs-lookup"><span data-stu-id="8bf67-243">To enable Azure AD users to log in to JIRA on-premises server, they must be provisioned into JIRA on-premises server.</span></span>

<span data-ttu-id="8bf67-244">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8bf67-244">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf67-245">Log in to your JIRA on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8bf67-245">Log in to your JIRA on-premises server as an administrator.</span></span>

2. <span data-ttu-id="8bf67-246">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-246">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/jira52microsoft-tutorial/user1.png)

3. <span data-ttu-id="8bf67-248">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span><span class="sxs-lookup"><span data-stu-id="8bf67-248">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Add Employee](./media/jira52microsoft-tutorial/user2.png)

4. <span data-ttu-id="8bf67-250">Under **User management** tab section, click **create user**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-250">Under **User management** tab section, click **create user**.</span></span>

    ![Add Employee](./media/jira52microsoft-tutorial/user3.png) 

5. <span data-ttu-id="8bf67-252">On the **“Create new user”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8bf67-252">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/jira52microsoft-tutorial/user4.png)

    <span data-ttu-id="8bf67-254">a.</span><span class="sxs-lookup"><span data-stu-id="8bf67-254">a.</span></span> <span data-ttu-id="8bf67-255">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8bf67-255">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="8bf67-256">b.</span><span class="sxs-lookup"><span data-stu-id="8bf67-256">b.</span></span> <span data-ttu-id="8bf67-257">In the **Full Name** textbox, type full name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bf67-257">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="8bf67-258">c.</span><span class="sxs-lookup"><span data-stu-id="8bf67-258">c.</span></span> <span data-ttu-id="8bf67-259">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8bf67-259">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="8bf67-260">d.</span><span class="sxs-lookup"><span data-stu-id="8bf67-260">d.</span></span> <span data-ttu-id="8bf67-261">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="8bf67-261">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="8bf67-262">e.</span><span class="sxs-lookup"><span data-stu-id="8bf67-262">e.</span></span> <span data-ttu-id="8bf67-263">Click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-263">Click **Create user**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8bf67-264">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8bf67-264">Assign the Azure AD test user</span></span>

<span data-ttu-id="8bf67-265">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft (V5.2).</span><span class="sxs-lookup"><span data-stu-id="8bf67-265">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft (V5.2).</span></span>

![Assign the user role][200]

<span data-ttu-id="8bf67-267">**To assign Britta Simon to JIRA SAML SSO by Microsoft (V5.2), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8bf67-267">**To assign Britta Simon to JIRA SAML SSO by Microsoft (V5.2), perform the following steps:**</span></span>

1. <span data-ttu-id="8bf67-268">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-268">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="8bf67-270">In the applications list, select **JIRA SAML SSO by Microsoft (V5.2)**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-270">In the applications list, select **JIRA SAML SSO by Microsoft (V5.2)**.</span></span>

    ![The JIRA SAML SSO by Microsoft (V5.2) link in the Applications list](./media/jira52microsoft-tutorial/tutorial_singlesign-onforjira5.2_app.png)

3. <span data-ttu-id="8bf67-272">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8bf67-272">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="8bf67-274">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8bf67-274">Click **Add** button.</span></span> <span data-ttu-id="8bf67-275">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8bf67-275">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="8bf67-277">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8bf67-277">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8bf67-278">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8bf67-278">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bf67-279">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8bf67-279">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="8bf67-280">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8bf67-280">Test single sign-on</span></span>

<span data-ttu-id="8bf67-281">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8bf67-281">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8bf67-282">When you click the JIRA SAML SSO by Microsoft (V5.2) tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft (V5.2) application.</span><span class="sxs-lookup"><span data-stu-id="8bf67-282">When you click the JIRA SAML SSO by Microsoft (V5.2) tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft (V5.2) application.</span></span>
<span data-ttu-id="8bf67-283">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8bf67-283">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8bf67-284">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8bf67-284">Additional resources</span></span>

* [<span data-ttu-id="8bf67-285">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bf67-285">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8bf67-286">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bf67-286">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/msaadssojira5.2-tutorial/tutorial_general_01.png
[2]: ./media/msaadssojira5.2-tutorial/tutorial_general_02.png
[3]: ./media/msaadssojira5.2-tutorial/tutorial_general_03.png
[4]: ./media/msaadssojira5.2-tutorial/tutorial_general_04.png

[100]: ./media/msaadssojira5.2-tutorial/tutorial_general_100.png

[200]: ./media/msaadssojira5.2-tutorial/tutorial_general_200.png
[201]: ./media/msaadssojira5.2-tutorial/tutorial_general_201.png
[202]: ./media/msaadssojira5.2-tutorial/tutorial_general_202.png
[203]: ./media/msaadssojira5.2-tutorial/tutorial_general_203.png