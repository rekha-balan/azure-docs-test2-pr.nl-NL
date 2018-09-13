---
title: 'Tutorial: Azure Active Directory integration with Kantega SSO for Confluence | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kantega SSO for Confluence.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fd53a6814649b529e301c3135fb491c51a13bcb1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968818"
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a><span data-ttu-id="05ef9-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span><span class="sxs-lookup"><span data-stu-id="05ef9-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span></span>

<span data-ttu-id="05ef9-104">In this tutorial, you learn how to integrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05ef9-104">In this tutorial, you learn how to integrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05ef9-105">Integrating Kantega SSO for Confluence with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="05ef9-105">Integrating Kantega SSO for Confluence with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05ef9-106">You can control in Azure AD who has access to Kantega SSO for Confluence</span><span class="sxs-lookup"><span data-stu-id="05ef9-106">You can control in Azure AD who has access to Kantega SSO for Confluence</span></span>
- <span data-ttu-id="05ef9-107">You can enable your users to automatically get signed-on to Kantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="05ef9-107">You can enable your users to automatically get signed-on to Kantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05ef9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="05ef9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="05ef9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="05ef9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05ef9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05ef9-110">Prerequisites</span></span>

<span data-ttu-id="05ef9-111">To configure Azure AD integration with Kantega SSO for Confluence, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="05ef9-111">To configure Azure AD integration with Kantega SSO for Confluence, you need the following items:</span></span>

- <span data-ttu-id="05ef9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="05ef9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05ef9-113">A Kantega SSO for Confluence single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="05ef9-113">A Kantega SSO for Confluence single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05ef9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="05ef9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05ef9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="05ef9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05ef9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="05ef9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05ef9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05ef9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05ef9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="05ef9-118">Scenario description</span></span>
<span data-ttu-id="05ef9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="05ef9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05ef9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="05ef9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05ef9-121">Adding Kantega SSO for Confluence from the gallery</span><span class="sxs-lookup"><span data-stu-id="05ef9-121">Adding Kantega SSO for Confluence from the gallery</span></span>
1. <span data-ttu-id="05ef9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05ef9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-confluence-from-the-gallery"></a><span data-ttu-id="05ef9-123">Adding Kantega SSO for Confluence from the gallery</span><span class="sxs-lookup"><span data-stu-id="05ef9-123">Adding Kantega SSO for Confluence from the gallery</span></span>
<span data-ttu-id="05ef9-124">To configure the integration of Kantega SSO for Confluence into Azure AD, you need to add Kantega SSO for Confluence from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="05ef9-124">To configure the integration of Kantega SSO for Confluence into Azure AD, you need to add Kantega SSO for Confluence from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05ef9-125">**To add Kantega SSO for Confluence from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ef9-125">**To add Kantega SSO for Confluence from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05ef9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="05ef9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="05ef9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="05ef9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="05ef9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="05ef9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="05ef9-133">In the search box, type **Kantega SSO for Confluence**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-133">In the search box, type **Kantega SSO for Confluence**.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

1. <span data-ttu-id="05ef9-135">In the results panel, select **Kantega SSO for Confluence**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="05ef9-135">In the results panel, select **Kantega SSO for Confluence**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05ef9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05ef9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05ef9-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="05ef9-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05ef9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Confluence is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05ef9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Confluence is to a user in Azure AD.</span></span> <span data-ttu-id="05ef9-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Confluence needs to be established.</span><span class="sxs-lookup"><span data-stu-id="05ef9-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Confluence needs to be established.</span></span>

<span data-ttu-id="05ef9-141">In Kantega SSO for Confluence, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="05ef9-141">In Kantega SSO for Confluence, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="05ef9-142">To configure and test Azure AD single sign-on with Kantega SSO for Confluence, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="05ef9-142">To configure and test Azure AD single sign-on with Kantega SSO for Confluence, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05ef9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="05ef9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="05ef9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05ef9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="05ef9-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Confluence that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="05ef9-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Confluence that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="05ef9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05ef9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="05ef9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="05ef9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05ef9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05ef9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05ef9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span><span class="sxs-lookup"><span data-stu-id="05ef9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span></span>

<span data-ttu-id="05ef9-150">**To configure Azure AD single sign-on with Kantega SSO for Confluence, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ef9-150">**To configure Azure AD single sign-on with Kantega SSO for Confluence, perform the following steps:**</span></span>

1. <span data-ttu-id="05ef9-151">In the Azure portal, on the **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-151">In the Azure portal, on the **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="05ef9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05ef9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

1. <span data-ttu-id="05ef9-155">In **IDP** initiated mode, on the **Kantega SSO for Confluence Domain and URLs** section perform the following step:</span><span class="sxs-lookup"><span data-stu-id="05ef9-155">In **IDP** initiated mode, on the **Kantega SSO for Confluence Domain and URLs** section perform the following step:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    <span data-ttu-id="05ef9-157">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-157">a.</span></span> <span data-ttu-id="05ef9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="05ef9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="05ef9-159">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-159">b.</span></span> <span data-ttu-id="05ef9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="05ef9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

1. <span data-ttu-id="05ef9-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span><span class="sxs-lookup"><span data-stu-id="05ef9-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    <span data-ttu-id="05ef9-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="05ef9-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05ef9-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="05ef9-164">These values are not real.</span></span> <span data-ttu-id="05ef9-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="05ef9-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="05ef9-166">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="05ef9-166">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="05ef9-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="05ef9-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

1. <span data-ttu-id="05ef9-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="05ef9-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="05ef9-171">In a different web browser window, log in to your **Confluence admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="05ef9-171">In a different web browser window, log in to your **Confluence admin portal** as an administrator.</span></span>

1. <span data-ttu-id="05ef9-172">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-172">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon1.png)

1. <span data-ttu-id="05ef9-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon.png)

1. <span data-ttu-id="05ef9-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button to install the new SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="05ef9-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon2.png)

1. <span data-ttu-id="05ef9-178">The plugin installation starts.</span><span class="sxs-lookup"><span data-stu-id="05ef9-178">The plugin installation starts.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon3.png)

1. <span data-ttu-id="05ef9-180">Once the installation is complete.</span><span class="sxs-lookup"><span data-stu-id="05ef9-180">Once the installation is complete.</span></span> <span data-ttu-id="05ef9-181">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-181">Click **Close**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon33.png)

1.  <span data-ttu-id="05ef9-183">Click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-183">Click **Manage**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon34.png)
    
1. <span data-ttu-id="05ef9-185">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="05ef9-185">Click **Configure** to configure the new plugin.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon35.png)

1. <span data-ttu-id="05ef9-187">This new plugin can also be found under **USERS & SECURITY** tab.</span><span class="sxs-lookup"><span data-stu-id="05ef9-187">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon36.png)
    
1. <span data-ttu-id="05ef9-189">In the **SAML** section.</span><span class="sxs-lookup"><span data-stu-id="05ef9-189">In the **SAML** section.</span></span> <span data-ttu-id="05ef9-190">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span><span class="sxs-lookup"><span data-stu-id="05ef9-190">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon4.png)

1. <span data-ttu-id="05ef9-192">Select subscription level as **Basic**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-192">Select subscription level as **Basic**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon5.png)     

1. <span data-ttu-id="05ef9-194">On the **App properties** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-194">On the **App properties** section, perform following steps:</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon6.png)

    <span data-ttu-id="05ef9-196">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-196">a.</span></span> <span data-ttu-id="05ef9-197">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05ef9-197">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="05ef9-198">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-198">b.</span></span> <span data-ttu-id="05ef9-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-199">Click **Next**.</span></span>

1. <span data-ttu-id="05ef9-200">On the **Metadata import** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-200">On the **Metadata import** section, perform following steps:</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon7.png)

    <span data-ttu-id="05ef9-202">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-202">a.</span></span> <span data-ttu-id="05ef9-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05ef9-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="05ef9-204">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-204">b.</span></span> <span data-ttu-id="05ef9-205">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-205">Click **Next**.</span></span>

1. <span data-ttu-id="05ef9-206">On the **Name and SSO location** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-206">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon8.png)
    
    <span data-ttu-id="05ef9-208">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-208">a.</span></span> <span data-ttu-id="05ef9-209">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05ef9-209">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="05ef9-210">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-210">b.</span></span> <span data-ttu-id="05ef9-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-211">Click **Next**.</span></span>

1. <span data-ttu-id="05ef9-212">Verify the Signing certificate and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-212">Verify the Signing certificate and click **Next**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon9.png)

1. <span data-ttu-id="05ef9-214">On the **Confluence user accounts** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-214">On the **Confluence user accounts** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon10.png)

    <span data-ttu-id="05ef9-216">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-216">a.</span></span> <span data-ttu-id="05ef9-217">Select **Create users in Confluence's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span><span class="sxs-lookup"><span data-stu-id="05ef9-217">Select **Create users in Confluence's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="05ef9-218">of groups separated by comma).</span><span class="sxs-lookup"><span data-stu-id="05ef9-218">of groups separated by comma).</span></span>

    <span data-ttu-id="05ef9-219">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-219">b.</span></span> <span data-ttu-id="05ef9-220">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-220">Click **Next**.</span></span>

1. <span data-ttu-id="05ef9-221">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-221">Click **Finish**.</span></span>    

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon11.png)

1. <span data-ttu-id="05ef9-223">On the **Known domains for Azure AD** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-223">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/addon12.png)

    <span data-ttu-id="05ef9-225">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-225">a.</span></span> <span data-ttu-id="05ef9-226">Select **Known domains** from the left panel of the page.</span><span class="sxs-lookup"><span data-stu-id="05ef9-226">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="05ef9-227">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-227">b.</span></span> <span data-ttu-id="05ef9-228">Enter domain name in the **Known domains** textbox.</span><span class="sxs-lookup"><span data-stu-id="05ef9-228">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="05ef9-229">c.</span><span class="sxs-lookup"><span data-stu-id="05ef9-229">c.</span></span> <span data-ttu-id="05ef9-230">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-230">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="05ef9-231">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="05ef9-231">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05ef9-232">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="05ef9-232">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05ef9-233">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05ef9-233">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05ef9-234">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="05ef9-234">Creating an Azure AD test user</span></span>
<span data-ttu-id="05ef9-235">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05ef9-235">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="05ef9-237">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ef9-237">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05ef9-238">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="05ef9-238">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforconfluence-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="05ef9-240">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-240">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kantegassoforconfluence-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="05ef9-242">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="05ef9-242">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforconfluence-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="05ef9-244">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-244">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05ef9-246">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-246">a.</span></span> <span data-ttu-id="05ef9-247">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-247">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05ef9-248">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-248">b.</span></span> <span data-ttu-id="05ef9-249">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05ef9-249">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05ef9-250">c.</span><span class="sxs-lookup"><span data-stu-id="05ef9-250">c.</span></span> <span data-ttu-id="05ef9-251">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-251">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="05ef9-252">d.</span><span class="sxs-lookup"><span data-stu-id="05ef9-252">d.</span></span> <span data-ttu-id="05ef9-253">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-253">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a><span data-ttu-id="05ef9-254">Creating a Kantega SSO for Confluence test user</span><span class="sxs-lookup"><span data-stu-id="05ef9-254">Creating a Kantega SSO for Confluence test user</span></span>

<span data-ttu-id="05ef9-255">To enable Azure AD users to log in to Confluence, they must be provisioned into Confluence.</span><span class="sxs-lookup"><span data-stu-id="05ef9-255">To enable Azure AD users to log in to Confluence, they must be provisioned into Confluence.</span></span> <span data-ttu-id="05ef9-256">In the case of Kantega SSO for Confluence, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="05ef9-256">In the case of Kantega SSO for Confluence, provisioning is a manual task.</span></span>

<span data-ttu-id="05ef9-257">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ef9-257">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="05ef9-258">Log in to your Kantega SSO for Confluence company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="05ef9-258">Log in to your Kantega SSO for Confluence company site as an administrator.</span></span>

1. <span data-ttu-id="05ef9-259">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-259">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/kantegassoforconfluence-tutorial/user1.png) 

1. <span data-ttu-id="05ef9-261">Under Users section, click **Add Users** tab. On the **“Add a User”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ef9-261">Under Users section, click **Add Users** tab. On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/kantegassoforconfluence-tutorial/user2.png) 

    <span data-ttu-id="05ef9-263">a.</span><span class="sxs-lookup"><span data-stu-id="05ef9-263">a.</span></span> <span data-ttu-id="05ef9-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="05ef9-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="05ef9-265">b.</span><span class="sxs-lookup"><span data-stu-id="05ef9-265">b.</span></span> <span data-ttu-id="05ef9-266">In the **Full Name** textbox, type the full name of user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05ef9-266">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="05ef9-267">c.</span><span class="sxs-lookup"><span data-stu-id="05ef9-267">c.</span></span> <span data-ttu-id="05ef9-268">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="05ef9-268">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="05ef9-269">d.</span><span class="sxs-lookup"><span data-stu-id="05ef9-269">d.</span></span> <span data-ttu-id="05ef9-270">In the **Password** textbox, type the password for user.</span><span class="sxs-lookup"><span data-stu-id="05ef9-270">In the **Password** textbox, type the password for user.</span></span>

    <span data-ttu-id="05ef9-271">e.</span><span class="sxs-lookup"><span data-stu-id="05ef9-271">e.</span></span> <span data-ttu-id="05ef9-272">Click **Confirm Password** reenter the password.</span><span class="sxs-lookup"><span data-stu-id="05ef9-272">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="05ef9-273">f.</span><span class="sxs-lookup"><span data-stu-id="05ef9-273">f.</span></span> <span data-ttu-id="05ef9-274">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="05ef9-274">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05ef9-275">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="05ef9-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="05ef9-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Confluence.</span><span class="sxs-lookup"><span data-stu-id="05ef9-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Confluence.</span></span>

![Assign User][200] 

<span data-ttu-id="05ef9-278">**To assign Britta Simon to Kantega SSO for Confluence, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ef9-278">**To assign Britta Simon to Kantega SSO for Confluence, perform the following steps:**</span></span>

1. <span data-ttu-id="05ef9-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="05ef9-281">In the applications list, select **Kantega SSO for Confluence**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-281">In the applications list, select **Kantega SSO for Confluence**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

1. <span data-ttu-id="05ef9-283">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="05ef9-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="05ef9-285">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="05ef9-285">Click **Add** button.</span></span> <span data-ttu-id="05ef9-286">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="05ef9-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="05ef9-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="05ef9-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="05ef9-289">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="05ef9-289">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="05ef9-290">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="05ef9-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05ef9-291">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="05ef9-291">Testing single sign-on</span></span>

<span data-ttu-id="05ef9-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="05ef9-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="05ef9-293">When you click the Kantega SSO for Confluence tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Confluence application.</span><span class="sxs-lookup"><span data-stu-id="05ef9-293">When you click the Kantega SSO for Confluence tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Confluence application.</span></span>
<span data-ttu-id="05ef9-294">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05ef9-294">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05ef9-295">Additional resources</span><span class="sxs-lookup"><span data-stu-id="05ef9-295">Additional resources</span></span>

* [<span data-ttu-id="05ef9-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05ef9-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="05ef9-297">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05ef9-297">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/kantegassoforconfluence-tutorial/tutorial_general_203.png

