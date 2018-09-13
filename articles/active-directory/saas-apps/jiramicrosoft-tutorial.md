---
title: 'Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and JIRA SAML SSO by Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4b663047-7f88-443b-97bd-54224b232815
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: jeedes
ms.openlocfilehash: cc87985404ef8c9ee625f32b359e6ac1a29e73ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865542"
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="61c2f-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="61c2f-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="61c2f-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61c2f-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61c2f-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="61c2f-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61c2f-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="61c2f-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft.</span></span>
- <span data-ttu-id="61c2f-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="61c2f-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="61c2f-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="61c2f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="61c2f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="61c2f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="description"></a><span data-ttu-id="61c2f-110">Description</span><span class="sxs-lookup"><span data-stu-id="61c2f-110">Description</span></span>

<span data-ttu-id="61c2f-111">Use your Microsoft Azure Active Directory account with Atlassian JIRA server to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61c2f-111">Use your Microsoft Azure Active Directory account with Atlassian JIRA server to enable single sign-on.</span></span> <span data-ttu-id="61c2f-112">This way all your organization users can use the Azure AD credentials to login into the JIRA application.</span><span class="sxs-lookup"><span data-stu-id="61c2f-112">This way all your organization users can use the Azure AD credentials to login into the JIRA application.</span></span> <span data-ttu-id="61c2f-113">This plugin uses SAML 2.0 for federation.</span><span class="sxs-lookup"><span data-stu-id="61c2f-113">This plugin uses SAML 2.0 for federation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61c2f-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61c2f-114">Prerequisites</span></span>

<span data-ttu-id="61c2f-115">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="61c2f-115">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="61c2f-116">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="61c2f-116">An Azure AD subscription</span></span>
- <span data-ttu-id="61c2f-117">JIRA Core and Software 6.0 to 7.8 or JIRA Service Desk 3.0 to 3.2 should installed and configured on Windows 64-bit version</span><span class="sxs-lookup"><span data-stu-id="61c2f-117">JIRA Core and Software 6.0 to 7.8 or JIRA Service Desk 3.0 to 3.2 should installed and configured on Windows 64-bit version</span></span>
- <span data-ttu-id="61c2f-118">JIRA server is HTTPS enabled</span><span class="sxs-lookup"><span data-stu-id="61c2f-118">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="61c2f-119">Note the supported versions for JIRA Plugin are mentioned in below section.</span><span class="sxs-lookup"><span data-stu-id="61c2f-119">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="61c2f-120">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span><span class="sxs-lookup"><span data-stu-id="61c2f-120">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="61c2f-121">Admin credentials are set up in JIRA</span><span class="sxs-lookup"><span data-stu-id="61c2f-121">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="61c2f-122">WebSudo is disabled in JIRA</span><span class="sxs-lookup"><span data-stu-id="61c2f-122">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="61c2f-123">Test user created in the JIRA server application</span><span class="sxs-lookup"><span data-stu-id="61c2f-123">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="61c2f-124">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span><span class="sxs-lookup"><span data-stu-id="61c2f-124">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="61c2f-125">Test the integration first in development or staging environment of the application and then use the production environment.</span><span class="sxs-lookup"><span data-stu-id="61c2f-125">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="61c2f-126">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="61c2f-126">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61c2f-127">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="61c2f-127">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61c2f-128">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61c2f-128">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="61c2f-129">Supported versions of JIRA</span><span class="sxs-lookup"><span data-stu-id="61c2f-129">Supported versions of JIRA</span></span>

*   <span data-ttu-id="61c2f-130">JIRA Core and Software: 6.0 to 7.8</span><span class="sxs-lookup"><span data-stu-id="61c2f-130">JIRA Core and Software: 6.0 to 7.8</span></span>
*   <span data-ttu-id="61c2f-131">JIRA Service Desk 3.0 to 3.2</span><span class="sxs-lookup"><span data-stu-id="61c2f-131">JIRA Service Desk 3.0 to 3.2</span></span>
*   <span data-ttu-id="61c2f-132">JIRA also supports 5.2.</span><span class="sxs-lookup"><span data-stu-id="61c2f-132">JIRA also supports 5.2.</span></span> <span data-ttu-id="61c2f-133">For more details, click [Microsoft Azure Active Directory single sign-on for JIRA 5.2](jira52microsoft-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="61c2f-133">For more details, click [Microsoft Azure Active Directory single sign-on for JIRA 5.2](jira52microsoft-tutorial.md)</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61c2f-134">Scenario description</span><span class="sxs-lookup"><span data-stu-id="61c2f-134">Scenario description</span></span>
<span data-ttu-id="61c2f-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="61c2f-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="61c2f-136">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="61c2f-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61c2f-137">Adding JIRA SAML SSO by Microsoft from the gallery</span><span class="sxs-lookup"><span data-stu-id="61c2f-137">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="61c2f-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61c2f-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="61c2f-139">Adding JIRA SAML SSO by Microsoft from the gallery</span><span class="sxs-lookup"><span data-stu-id="61c2f-139">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="61c2f-140">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="61c2f-140">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61c2f-141">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61c2f-141">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61c2f-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61c2f-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="61c2f-144">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61c2f-145">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-145">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="61c2f-147">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="61c2f-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="61c2f-149">In the search box, type **JIRA SAML SSO by Microsoft**, select **JIRA SAML SSO by Microsoft** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="61c2f-149">In the search box, type **JIRA SAML SSO by Microsoft**, select **JIRA SAML SSO by Microsoft** from result panel then click **Add** button to add the application.</span></span>

    ![JIRA SAML SSO by Microsoft in the results list](./media/jiramicrosoft-tutorial/tutorial_singlesign-onforjira_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="61c2f-151">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61c2f-151">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="61c2f-152">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="61c2f-152">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61c2f-153">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61c2f-153">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="61c2f-154">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span><span class="sxs-lookup"><span data-stu-id="61c2f-154">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="61c2f-155">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="61c2f-155">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61c2f-156">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="61c2f-156">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="61c2f-157">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61c2f-157">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61c2f-158">**[Create a JIRA SAML SSO by Microsoft test user](#create-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="61c2f-158">**[Create a JIRA SAML SSO by Microsoft test user](#create-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="61c2f-159">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61c2f-159">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61c2f-160">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="61c2f-160">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="61c2f-161">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61c2f-161">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="61c2f-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="61c2f-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="61c2f-163">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61c2f-163">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="61c2f-164">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-164">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="61c2f-166">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61c2f-166">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/jiramicrosoft-tutorial/tutorial_singlesign-onforjira_samlbase.png)

3. <span data-ttu-id="61c2f-168">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61c2f-168">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![JIRA SAML SSO by Microsoft Domain and URLs single sign-on information](./media/jiramicrosoft-tutorial/tutorial_singlesign-onforjira_url.png)

    <span data-ttu-id="61c2f-170">a.</span><span class="sxs-lookup"><span data-stu-id="61c2f-170">a.</span></span> <span data-ttu-id="61c2f-171">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="61c2f-171">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="61c2f-172">b.</span><span class="sxs-lookup"><span data-stu-id="61c2f-172">b.</span></span> <span data-ttu-id="61c2f-173">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="61c2f-173">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="61c2f-174">c.</span><span class="sxs-lookup"><span data-stu-id="61c2f-174">c.</span></span> <span data-ttu-id="61c2f-175">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="61c2f-175">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE]
    > <span data-ttu-id="61c2f-176">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="61c2f-176">These values are not real.</span></span> <span data-ttu-id="61c2f-177">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="61c2f-177">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="61c2f-178">Port is optional in case it’s a named URL.</span><span class="sxs-lookup"><span data-stu-id="61c2f-178">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="61c2f-179">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="61c2f-179">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="61c2f-180">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="61c2f-180">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![Configure Single Sign-On](./media/jiramicrosoft-tutorial/tutorial_metadataurl.png)

5. <span data-ttu-id="61c2f-182">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="61c2f-182">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61c2f-184">In a different web browser window, log in to your JIRA instance as an administrator.</span><span class="sxs-lookup"><span data-stu-id="61c2f-184">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

7. <span data-ttu-id="61c2f-185">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-185">Hover on cog and click the **Add-ons**.</span></span>

    ![Configure Single Sign-On](./media/jiramicrosoft-tutorial/addon1.png)

8. <span data-ttu-id="61c2f-187">Download the plugin from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56506).</span><span class="sxs-lookup"><span data-stu-id="61c2f-187">Download the plugin from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56506).</span></span> <span data-ttu-id="61c2f-188">Manually upload the plugin provided by Microsoft using **Upload add-on** menu.</span><span class="sxs-lookup"><span data-stu-id="61c2f-188">Manually upload the plugin provided by Microsoft using **Upload add-on** menu.</span></span> <span data-ttu-id="61c2f-189">The download of plugin is covered under [Microsoft Service Agreement](https://www.microsoft.com/servicesagreement/).</span><span class="sxs-lookup"><span data-stu-id="61c2f-189">The download of plugin is covered under [Microsoft Service Agreement](https://www.microsoft.com/servicesagreement/).</span></span>

    ![Configure Single Sign-On](./media/jiramicrosoft-tutorial/addon12.png)

9. <span data-ttu-id="61c2f-191">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span><span class="sxs-lookup"><span data-stu-id="61c2f-191">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span> <span data-ttu-id="61c2f-192">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="61c2f-192">Click **Configure** to configure the new plugin.</span></span>

    ![Configure Single Sign-On](./media/jiramicrosoft-tutorial/addon13.png)

10. <span data-ttu-id="61c2f-194">Perform following steps on configuration page:</span><span class="sxs-lookup"><span data-stu-id="61c2f-194">Perform following steps on configuration page:</span></span>

    ![Configure Single Sign-On](./media/jiramicrosoft-tutorial/addon52.png)

    > [!TIP]
    > <span data-ttu-id="61c2f-196">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span><span class="sxs-lookup"><span data-stu-id="61c2f-196">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="61c2f-197">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span><span class="sxs-lookup"><span data-stu-id="61c2f-197">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>

    <span data-ttu-id="61c2f-198">a.</span><span class="sxs-lookup"><span data-stu-id="61c2f-198">a.</span></span> <span data-ttu-id="61c2f-199">In the **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal and click the **Resolve** button.</span><span class="sxs-lookup"><span data-stu-id="61c2f-199">In the **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal and click the **Resolve** button.</span></span> <span data-ttu-id="61c2f-200">It reads the IdP metadata URL and populates all the fields information.</span><span class="sxs-lookup"><span data-stu-id="61c2f-200">It reads the IdP metadata URL and populates all the fields information.</span></span>

    <span data-ttu-id="61c2f-201">b.</span><span class="sxs-lookup"><span data-stu-id="61c2f-201">b.</span></span> <span data-ttu-id="61c2f-202">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="61c2f-202">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="61c2f-203">c.</span><span class="sxs-lookup"><span data-stu-id="61c2f-203">c.</span></span> <span data-ttu-id="61c2f-204">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span><span class="sxs-lookup"><span data-stu-id="61c2f-204">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="61c2f-205">d.</span><span class="sxs-lookup"><span data-stu-id="61c2f-205">d.</span></span> <span data-ttu-id="61c2f-206">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-206">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="61c2f-207">This ID has to be the JIRA user id. If the user id is not matched, then system will not allow users to log in.</span><span class="sxs-lookup"><span data-stu-id="61c2f-207">This ID has to be the JIRA user id. If the user id is not matched, then system will not allow users to log in.</span></span>

    > [!Note]
    > <span data-ttu-id="61c2f-208">Default SAML User ID location is Name Identifier.</span><span class="sxs-lookup"><span data-stu-id="61c2f-208">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="61c2f-209">You can change this to an attribute option and enter the appropriate attribute name.</span><span class="sxs-lookup"><span data-stu-id="61c2f-209">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    <span data-ttu-id="61c2f-210">e.</span><span class="sxs-lookup"><span data-stu-id="61c2f-210">e.</span></span> <span data-ttu-id="61c2f-211">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span><span class="sxs-lookup"><span data-stu-id="61c2f-211">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span>

    <span data-ttu-id="61c2f-212">f.</span><span class="sxs-lookup"><span data-stu-id="61c2f-212">f.</span></span> <span data-ttu-id="61c2f-213">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-213">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>

    <span data-ttu-id="61c2f-214">g.</span><span class="sxs-lookup"><span data-stu-id="61c2f-214">g.</span></span> <span data-ttu-id="61c2f-215">In **Domain Name** type the domain name here in case of the ADFS-based login.</span><span class="sxs-lookup"><span data-stu-id="61c2f-215">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="61c2f-216">h.</span><span class="sxs-lookup"><span data-stu-id="61c2f-216">h.</span></span> <span data-ttu-id="61c2f-217">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span><span class="sxs-lookup"><span data-stu-id="61c2f-217">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span>

    <span data-ttu-id="61c2f-218">i.</span><span class="sxs-lookup"><span data-stu-id="61c2f-218">i.</span></span> <span data-ttu-id="61c2f-219">Click **Save** button to save the settings.</span><span class="sxs-lookup"><span data-stu-id="61c2f-219">Click **Save** button to save the settings.</span></span>

    > [!NOTE]
    > <span data-ttu-id="61c2f-220">For more information about installation and troubleshooting, visit [MS JIRA SSO Connector Admin Guide](../ms-confluence-jira-plugin-adminguide.md) and there is also [FAQ](../ms-confluence-jira-plugin-faq.md) for your assistance</span><span class="sxs-lookup"><span data-stu-id="61c2f-220">For more information about installation and troubleshooting, visit [MS JIRA SSO Connector Admin Guide](../ms-confluence-jira-plugin-adminguide.md) and there is also [FAQ](../ms-confluence-jira-plugin-faq.md) for your assistance</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="61c2f-221">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61c2f-221">Create an Azure AD test user</span></span>

<span data-ttu-id="61c2f-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61c2f-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="61c2f-224">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61c2f-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61c2f-225">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="61c2f-225">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/jiramicrosoft-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="61c2f-227">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-227">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/jiramicrosoft-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="61c2f-229">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="61c2f-229">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/jiramicrosoft-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="61c2f-231">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61c2f-231">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/jiramicrosoft-tutorial/create_aaduser_04.png)

    <span data-ttu-id="61c2f-233">a.</span><span class="sxs-lookup"><span data-stu-id="61c2f-233">a.</span></span> <span data-ttu-id="61c2f-234">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-234">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61c2f-235">b.</span><span class="sxs-lookup"><span data-stu-id="61c2f-235">b.</span></span> <span data-ttu-id="61c2f-236">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61c2f-236">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="61c2f-237">c.</span><span class="sxs-lookup"><span data-stu-id="61c2f-237">c.</span></span> <span data-ttu-id="61c2f-238">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="61c2f-238">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="61c2f-239">d.</span><span class="sxs-lookup"><span data-stu-id="61c2f-239">d.</span></span> <span data-ttu-id="61c2f-240">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-240">Click **Create**.</span></span>

### <a name="create-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="61c2f-241">Create a JIRA SAML SSO by Microsoft test user</span><span class="sxs-lookup"><span data-stu-id="61c2f-241">Create a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="61c2f-242">To enable Azure AD users to log in to JIRA on-premises server, they must be provisioned into JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="61c2f-242">To enable Azure AD users to log in to JIRA on-premises server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="61c2f-243">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="61c2f-243">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="61c2f-244">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61c2f-244">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="61c2f-245">Log in to your JIRA on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="61c2f-245">Log in to your JIRA on-premises server as an administrator.</span></span>

2. <span data-ttu-id="61c2f-246">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-246">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/jiramicrosoft-tutorial/user1.png)

3. <span data-ttu-id="61c2f-248">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span><span class="sxs-lookup"><span data-stu-id="61c2f-248">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Add Employee](./media/jiramicrosoft-tutorial/user2.png)

4. <span data-ttu-id="61c2f-250">Under **User management** tab section, click **create user**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-250">Under **User management** tab section, click **create user**.</span></span>

    ![Add Employee](./media/jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="61c2f-252">On the **“Create new user”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61c2f-252">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="61c2f-254">a.</span><span class="sxs-lookup"><span data-stu-id="61c2f-254">a.</span></span> <span data-ttu-id="61c2f-255">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="61c2f-255">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="61c2f-256">b.</span><span class="sxs-lookup"><span data-stu-id="61c2f-256">b.</span></span> <span data-ttu-id="61c2f-257">In the **Full Name** textbox, type full name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61c2f-257">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="61c2f-258">c.</span><span class="sxs-lookup"><span data-stu-id="61c2f-258">c.</span></span> <span data-ttu-id="61c2f-259">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="61c2f-259">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="61c2f-260">d.</span><span class="sxs-lookup"><span data-stu-id="61c2f-260">d.</span></span> <span data-ttu-id="61c2f-261">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="61c2f-261">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="61c2f-262">e.</span><span class="sxs-lookup"><span data-stu-id="61c2f-262">e.</span></span> <span data-ttu-id="61c2f-263">Click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-263">Click **Create user**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="61c2f-264">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61c2f-264">Assign the Azure AD test user</span></span>

<span data-ttu-id="61c2f-265">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="61c2f-265">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Assign the user role][200] 

<span data-ttu-id="61c2f-267">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61c2f-267">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="61c2f-268">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-268">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="61c2f-270">In the applications list, select **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-270">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![The JIRA SAML SSO by Microsoft link in the Applications list](./media/jiramicrosoft-tutorial/tutorial_singlesign-onforjira_app.png)

3. <span data-ttu-id="61c2f-272">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="61c2f-272">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="61c2f-274">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="61c2f-274">Click **Add** button.</span></span> <span data-ttu-id="61c2f-275">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61c2f-275">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="61c2f-277">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="61c2f-277">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="61c2f-278">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="61c2f-278">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61c2f-279">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61c2f-279">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="61c2f-280">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="61c2f-280">Test single sign-on</span></span>

<span data-ttu-id="61c2f-281">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="61c2f-281">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61c2f-282">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="61c2f-282">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="61c2f-283">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61c2f-283">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61c2f-284">Additional resources</span><span class="sxs-lookup"><span data-stu-id="61c2f-284">Additional resources</span></span>

* [<span data-ttu-id="61c2f-285">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61c2f-285">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="61c2f-286">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61c2f-286">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/msaadssojira-tutorial/tutorial_general_01.png
[2]: ./media/msaadssojira-tutorial/tutorial_general_02.png
[3]: ./media/msaadssojira-tutorial/tutorial_general_03.png
[4]: ./media/msaadssojira-tutorial/tutorial_general_04.png

[100]: ./media/msaadssojira-tutorial/tutorial_general_100.png

[200]: ./media/msaadssojira-tutorial\tutorial_general_200.png
[201]: ./media/msaadssojira-tutorial\tutorial_general_201.png
[202]: ./media/msaadssojira-tutorial\tutorial_general_202.png
[203]: ./media/msaadssojira-tutorial\tutorial_general_203.png