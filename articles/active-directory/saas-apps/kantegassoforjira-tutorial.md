---
title: 'Tutorial: Azure Active Directory integration with Kantega SSO for JIRA | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kantega SSO for JIRA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b498c0406c70da253ae79d4fbb98d4af1d954175
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871318"
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="9e11f-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="9e11f-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="9e11f-104">In this tutorial, you learn how to integrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e11f-104">In this tutorial, you learn how to integrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e11f-105">Integrating Kantega SSO for JIRA with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9e11f-105">Integrating Kantega SSO for JIRA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e11f-106">You can control in Azure AD who has access to Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="9e11f-106">You can control in Azure AD who has access to Kantega SSO for JIRA</span></span>
- <span data-ttu-id="9e11f-107">You can enable your users to automatically get signed-on to Kantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9e11f-107">You can enable your users to automatically get signed-on to Kantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e11f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9e11f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9e11f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9e11f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e11f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9e11f-110">Prerequisites</span></span>

<span data-ttu-id="9e11f-111">To configure Azure AD integration with Kantega SSO for JIRA, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9e11f-111">To configure Azure AD integration with Kantega SSO for JIRA, you need the following items:</span></span>

- <span data-ttu-id="9e11f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9e11f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e11f-113">A Kantega SSO for JIRA single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9e11f-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e11f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9e11f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e11f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9e11f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e11f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9e11f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e11f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e11f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e11f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9e11f-118">Scenario description</span></span>
<span data-ttu-id="9e11f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9e11f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e11f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9e11f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e11f-121">Adding Kantega SSO for JIRA from the gallery</span><span class="sxs-lookup"><span data-stu-id="9e11f-121">Adding Kantega SSO for JIRA from the gallery</span></span>
1. <span data-ttu-id="9e11f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e11f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-the-gallery"></a><span data-ttu-id="9e11f-123">Adding Kantega SSO for JIRA from the gallery</span><span class="sxs-lookup"><span data-stu-id="9e11f-123">Adding Kantega SSO for JIRA from the gallery</span></span>
<span data-ttu-id="9e11f-124">To configure the integration of Kantega SSO for JIRA into Azure AD, you need to add Kantega SSO for JIRA from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9e11f-124">To configure the integration of Kantega SSO for JIRA into Azure AD, you need to add Kantega SSO for JIRA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e11f-125">**To add Kantega SSO for JIRA from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e11f-125">**To add Kantega SSO for JIRA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e11f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9e11f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="9e11f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e11f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="9e11f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9e11f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="9e11f-133">In the search box, type **Kantega SSO for JIRA**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-133">In the search box, type **Kantega SSO for JIRA**.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

1. <span data-ttu-id="9e11f-135">In the results panel, select **Kantega SSO for JIRA**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9e11f-135">In the results panel, select **Kantega SSO for JIRA**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e11f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e11f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e11f-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9e11f-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e11f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for JIRA is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e11f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for JIRA is to a user in Azure AD.</span></span> <span data-ttu-id="9e11f-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for JIRA needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9e11f-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for JIRA needs to be established.</span></span>

<span data-ttu-id="9e11f-141">In Kantega SSO for JIRA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9e11f-141">In Kantega SSO for JIRA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e11f-142">To configure and test Azure AD single sign-on with Kantega SSO for JIRA, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9e11f-142">To configure and test Azure AD single sign-on with Kantega SSO for JIRA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e11f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9e11f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9e11f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e11f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9e11f-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for JIRA that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9e11f-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for JIRA that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9e11f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9e11f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9e11f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9e11f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e11f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e11f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e11f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span><span class="sxs-lookup"><span data-stu-id="9e11f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="9e11f-150">**To configure Azure AD single sign-on with Kantega SSO for JIRA, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e11f-150">**To configure Azure AD single sign-on with Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="9e11f-151">In the Azure portal, on the **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-151">In the Azure portal, on the **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="9e11f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9e11f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

1. <span data-ttu-id="9e11f-155">In **IDP** initiated mode, on the **Kantega SSO for JIRA Domain and URLs** section perform the following step:</span><span class="sxs-lookup"><span data-stu-id="9e11f-155">In **IDP** initiated mode, on the **Kantega SSO for JIRA Domain and URLs** section perform the following step:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="9e11f-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-157">a.</span></span> <span data-ttu-id="9e11f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9e11f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="9e11f-159">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-159">b.</span></span> <span data-ttu-id="9e11f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9e11f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

1. <span data-ttu-id="9e11f-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span><span class="sxs-lookup"><span data-stu-id="9e11f-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="9e11f-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9e11f-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e11f-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9e11f-164">These values are not real.</span></span> <span data-ttu-id="9e11f-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="9e11f-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9e11f-166">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="9e11f-166">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="9e11f-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9e11f-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

1. <span data-ttu-id="9e11f-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9e11f-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="9e11f-171">In a different web browser window, log in to your JIRA on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9e11f-171">In a different web browser window, log in to your JIRA on-premises server as an administrator.</span></span>

1. <span data-ttu-id="9e11f-172">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon1.png)

1. <span data-ttu-id="9e11f-174">Under Add-ons tab section, click **Find new add-ons**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="9e11f-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="9e11f-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon2.png)

1. <span data-ttu-id="9e11f-177">The plugin installation starts.</span><span class="sxs-lookup"><span data-stu-id="9e11f-177">The plugin installation starts.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon3.png)

1. <span data-ttu-id="9e11f-179">Once the installation is complete.</span><span class="sxs-lookup"><span data-stu-id="9e11f-179">Once the installation is complete.</span></span> <span data-ttu-id="9e11f-180">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-180">Click **Close**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon33.png)

1.  <span data-ttu-id="9e11f-182">Click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-182">Click **Manage**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon34.png)
    
1. <span data-ttu-id="9e11f-184">New plugin is listed under **INTEGRATIONS**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="9e11f-185">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="9e11f-185">Click **Configure** to configure the new plugin.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon35.png)

1. <span data-ttu-id="9e11f-187">In the **SAML** section.</span><span class="sxs-lookup"><span data-stu-id="9e11f-187">In the **SAML** section.</span></span> <span data-ttu-id="9e11f-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9e11f-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon4.png)

1. <span data-ttu-id="9e11f-190">Select subscription level as **Basic**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-190">Select subscription level as **Basic**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon5.png)       

1. <span data-ttu-id="9e11f-192">On the **App properties** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-192">On the **App properties** section, perform following steps:</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="9e11f-194">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-194">a.</span></span> <span data-ttu-id="9e11f-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e11f-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="9e11f-196">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-196">b.</span></span> <span data-ttu-id="9e11f-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-197">Click **Next**.</span></span>

1. <span data-ttu-id="9e11f-198">On the **Metadata import** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-198">On the **Metadata import** section, perform following steps:</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="9e11f-200">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-200">a.</span></span> <span data-ttu-id="9e11f-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e11f-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="9e11f-202">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-202">b.</span></span> <span data-ttu-id="9e11f-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-203">Click **Next**.</span></span>

1. <span data-ttu-id="9e11f-204">On the **Name and SSO location** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="9e11f-206">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-206">a.</span></span> <span data-ttu-id="9e11f-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e11f-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="9e11f-208">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-208">b.</span></span> <span data-ttu-id="9e11f-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-209">Click **Next**.</span></span>

1. <span data-ttu-id="9e11f-210">Verify the Signing certificate and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-210">Verify the Signing certificate and click **Next**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon9.png)

1. <span data-ttu-id="9e11f-212">On the **JIRA user accounts** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-212">On the **JIRA user accounts** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="9e11f-214">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-214">a.</span></span> <span data-ttu-id="9e11f-215">Select **Create users in JIRA's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span><span class="sxs-lookup"><span data-stu-id="9e11f-215">Select **Create users in JIRA's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="9e11f-216">of groups separated by comma).</span><span class="sxs-lookup"><span data-stu-id="9e11f-216">of groups separated by comma).</span></span>

    <span data-ttu-id="9e11f-217">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-217">b.</span></span> <span data-ttu-id="9e11f-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-218">Click **Next**.</span></span>

1. <span data-ttu-id="9e11f-219">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-219">Click **Finish**.</span></span>    

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon11.png)

1. <span data-ttu-id="9e11f-221">On the **Known domains for Azure AD** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="9e11f-223">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-223">a.</span></span> <span data-ttu-id="9e11f-224">Select **Known domains** from the left panel of the page.</span><span class="sxs-lookup"><span data-stu-id="9e11f-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="9e11f-225">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-225">b.</span></span> <span data-ttu-id="9e11f-226">Enter domain name in the **Known domains** textbox.</span><span class="sxs-lookup"><span data-stu-id="9e11f-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="9e11f-227">c.</span><span class="sxs-lookup"><span data-stu-id="9e11f-227">c.</span></span> <span data-ttu-id="9e11f-228">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="9e11f-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9e11f-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e11f-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9e11f-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e11f-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e11f-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e11f-232">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9e11f-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e11f-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e11f-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="9e11f-235">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e11f-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e11f-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9e11f-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforjira-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="9e11f-238">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kantegassoforjira-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="9e11f-240">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9e11f-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforjira-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="9e11f-242">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e11f-244">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-244">a.</span></span> <span data-ttu-id="9e11f-245">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e11f-246">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-246">b.</span></span> <span data-ttu-id="9e11f-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e11f-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e11f-248">c.</span><span class="sxs-lookup"><span data-stu-id="9e11f-248">c.</span></span> <span data-ttu-id="9e11f-249">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e11f-250">d.</span><span class="sxs-lookup"><span data-stu-id="9e11f-250">d.</span></span> <span data-ttu-id="9e11f-251">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="9e11f-252">Creating a Kantega SSO for JIRA test user</span><span class="sxs-lookup"><span data-stu-id="9e11f-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="9e11f-253">To enable Azure AD users to log in to JIRA, they must be provisioned into JIRA.</span><span class="sxs-lookup"><span data-stu-id="9e11f-253">To enable Azure AD users to log in to JIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="9e11f-254">In Kantega SSO for JIRA, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="9e11f-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="9e11f-255">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e11f-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9e11f-256">Log in to your JIRA on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9e11f-256">Log in to your JIRA on-premises server as an administrator.</span></span>

1. <span data-ttu-id="9e11f-257">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-257">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/kantegassoforjira-tutorial/user1.png) 

1. <span data-ttu-id="9e11f-259">Under **User management** tab section, click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Add Employee](./media/kantegassoforjira-tutorial/user2.png) 

1. <span data-ttu-id="9e11f-261">On the **“Create new user”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9e11f-261">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="9e11f-263">a.</span><span class="sxs-lookup"><span data-stu-id="9e11f-263">a.</span></span> <span data-ttu-id="9e11f-264">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9e11f-264">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="9e11f-265">b.</span><span class="sxs-lookup"><span data-stu-id="9e11f-265">b.</span></span> <span data-ttu-id="9e11f-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e11f-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="9e11f-267">c.</span><span class="sxs-lookup"><span data-stu-id="9e11f-267">c.</span></span> <span data-ttu-id="9e11f-268">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9e11f-268">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="9e11f-269">d.</span><span class="sxs-lookup"><span data-stu-id="9e11f-269">d.</span></span> <span data-ttu-id="9e11f-270">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="9e11f-270">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="9e11f-271">e.</span><span class="sxs-lookup"><span data-stu-id="9e11f-271">e.</span></span> <span data-ttu-id="9e11f-272">Click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-272">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e11f-273">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9e11f-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e11f-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for JIRA.</span><span class="sxs-lookup"><span data-stu-id="9e11f-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for JIRA.</span></span>

![Assign User][200] 

<span data-ttu-id="9e11f-276">**To assign Britta Simon to Kantega SSO for JIRA, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e11f-276">**To assign Britta Simon to Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="9e11f-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9e11f-279">In the applications list, select **Kantega SSO for JIRA**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-279">In the applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

1. <span data-ttu-id="9e11f-281">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9e11f-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="9e11f-283">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9e11f-283">Click **Add** button.</span></span> <span data-ttu-id="9e11f-284">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e11f-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="9e11f-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9e11f-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9e11f-287">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e11f-287">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9e11f-288">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e11f-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e11f-289">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e11f-289">Testing single sign-on</span></span>

<span data-ttu-id="9e11f-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9e11f-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e11f-291">When you click the Kantega SSO for JIRA tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for JIRA application.</span><span class="sxs-lookup"><span data-stu-id="9e11f-291">When you click the Kantega SSO for JIRA tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="9e11f-292">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e11f-292">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e11f-293">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9e11f-293">Additional resources</span></span>

* [<span data-ttu-id="9e11f-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e11f-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9e11f-295">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e11f-295">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/kantegassoforjira-tutorial/tutorial_general_203.png

