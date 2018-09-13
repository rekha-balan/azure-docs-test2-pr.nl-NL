---
title: 'Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAML SSO for Jira by resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 6ae8256f3485d49d42efeb2927a6838252a1aeee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866729"
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="8811b-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="8811b-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="8811b-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8811b-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8811b-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8811b-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8811b-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="8811b-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="8811b-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8811b-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8811b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8811b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8811b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8811b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8811b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8811b-110">Prerequisites</span></span>

<span data-ttu-id="8811b-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8811b-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="8811b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8811b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8811b-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8811b-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8811b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8811b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8811b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8811b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8811b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8811b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8811b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8811b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8811b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8811b-118">Scenario description</span></span>
<span data-ttu-id="8811b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8811b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8811b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8811b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8811b-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span><span class="sxs-lookup"><span data-stu-id="8811b-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
1. <span data-ttu-id="8811b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8811b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="8811b-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span><span class="sxs-lookup"><span data-stu-id="8811b-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="8811b-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8811b-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8811b-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8811b-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8811b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8811b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8811b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8811b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8811b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8811b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8811b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8811b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8811b-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="8811b-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Creating an Azure AD test user](./media/samlssojira-tutorial/tutorial_samlssojira_search.png)

1. <span data-ttu-id="8811b-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8811b-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8811b-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8811b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8811b-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8811b-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8811b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8811b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="8811b-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8811b-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="8811b-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8811b-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8811b-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8811b-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8811b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8811b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8811b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8811b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8811b-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8811b-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8811b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8811b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8811b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8811b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8811b-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8811b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8811b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="8811b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="8811b-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8811b-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="8811b-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8811b-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8811b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8811b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

1. <span data-ttu-id="8811b-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="8811b-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="8811b-157">a.</span><span class="sxs-lookup"><span data-stu-id="8811b-157">a.</span></span> <span data-ttu-id="8811b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="8811b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="8811b-159">b.</span><span class="sxs-lookup"><span data-stu-id="8811b-159">b.</span></span> <span data-ttu-id="8811b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="8811b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

1. <span data-ttu-id="8811b-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="8811b-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="8811b-162">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="8811b-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="8811b-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="8811b-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8811b-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8811b-165">These values are not real.</span></span> <span data-ttu-id="8811b-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="8811b-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8811b-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8811b-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

1. <span data-ttu-id="8811b-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8811b-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

1. <span data-ttu-id="8811b-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="8811b-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8811b-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

1. <span data-ttu-id="8811b-173">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="8811b-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon1.png)

1. <span data-ttu-id="8811b-175">You are redirected to Administrator Access page.</span><span class="sxs-lookup"><span data-stu-id="8811b-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="8811b-176">Enter the **Password** and click **Confirm** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon2.png)

1. <span data-ttu-id="8811b-178">Under Add-ons tab section, click **Find new add-ons**.</span><span class="sxs-lookup"><span data-stu-id="8811b-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="8811b-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="8811b-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon7.png)

1. <span data-ttu-id="8811b-181">The plugin installation will start.</span><span class="sxs-lookup"><span data-stu-id="8811b-181">The plugin installation will start.</span></span> <span data-ttu-id="8811b-182">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="8811b-182">Click **Close**.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon8.png)

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon9.png)

1.  <span data-ttu-id="8811b-185">Click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="8811b-185">Click **Manage**.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon10.png)
    
1. <span data-ttu-id="8811b-187">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="8811b-187">Click **Configure** to configure the new plugin.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon11.png)

1. <span data-ttu-id="8811b-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add new IdP** button to configure the settings of Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="8811b-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add new IdP** button to configure the settings of Identity Provider.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon4.png)

1. <span data-ttu-id="8811b-191">On **Choose your SAML Identity Provider** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8811b-191">On **Choose your SAML Identity Provider** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon5a.png)
 
    <span data-ttu-id="8811b-193">a.</span><span class="sxs-lookup"><span data-stu-id="8811b-193">a.</span></span> <span data-ttu-id="8811b-194">Set **Azure AD** as the IdP type.</span><span class="sxs-lookup"><span data-stu-id="8811b-194">Set **Azure AD** as the IdP type.</span></span>
    
    <span data-ttu-id="8811b-195">b.</span><span class="sxs-lookup"><span data-stu-id="8811b-195">b.</span></span> <span data-ttu-id="8811b-196">Add **Name** of the Identity Provider (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8811b-196">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="8811b-197">c.</span><span class="sxs-lookup"><span data-stu-id="8811b-197">c.</span></span> <span data-ttu-id="8811b-198">Add **Description** of the Identity Provider (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8811b-198">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="8811b-199">d.</span><span class="sxs-lookup"><span data-stu-id="8811b-199">d.</span></span> <span data-ttu-id="8811b-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8811b-200">Click **Next**.</span></span>
    
1. <span data-ttu-id="8811b-201">On **Identity provider configuration** page, click **Next** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-201">On **Identity provider configuration** page, click **Next** button.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon5b.png)

1. <span data-ttu-id="8811b-203">On **Import SAML IdP Metadata** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8811b-203">On **Import SAML IdP Metadata** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon5c.png)

    <span data-ttu-id="8811b-205">a.</span><span class="sxs-lookup"><span data-stu-id="8811b-205">a.</span></span> <span data-ttu-id="8811b-206">Click **Load File** button and pick Metadata XML file you downloaded in Step 5.</span><span class="sxs-lookup"><span data-stu-id="8811b-206">Click **Load File** button and pick Metadata XML file you downloaded in Step 5.</span></span>

    <span data-ttu-id="8811b-207">b.</span><span class="sxs-lookup"><span data-stu-id="8811b-207">b.</span></span> <span data-ttu-id="8811b-208">Click **Import** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-208">Click **Import** button.</span></span>
    
    <span data-ttu-id="8811b-209">c.</span><span class="sxs-lookup"><span data-stu-id="8811b-209">c.</span></span> <span data-ttu-id="8811b-210">Wait briefly until import succeeds.</span><span class="sxs-lookup"><span data-stu-id="8811b-210">Wait briefly until import succeeds.</span></span>
    
    <span data-ttu-id="8811b-211">d.</span><span class="sxs-lookup"><span data-stu-id="8811b-211">d.</span></span> <span data-ttu-id="8811b-212">Click **Next** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-212">Click **Next** button.</span></span>
    
1. <span data-ttu-id="8811b-213">On **User ID attribute and transformation** page, click **Next** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-213">On **User ID attribute and transformation** page, click **Next** button.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon5d.png)
    
1. <span data-ttu-id="8811b-215">On **User creation and update** page, click **Save & Next** to save settings.</span><span class="sxs-lookup"><span data-stu-id="8811b-215">On **User creation and update** page, click **Save & Next** to save settings.</span></span>    
    
    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon6a.png)
    
1. <span data-ttu-id="8811b-217">On **Test your settings** page, click **Skip test & configure manually** to skip the user test for now.</span><span class="sxs-lookup"><span data-stu-id="8811b-217">On **Test your settings** page, click **Skip test & configure manually** to skip the user test for now.</span></span> <span data-ttu-id="8811b-218">This will be performed in the next section and requires some settings in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8811b-218">This will be performed in the next section and requires some settings in Azure portal.</span></span> 
    
    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon6b.png)
    
1. <span data-ttu-id="8811b-220">In the apprearing dialog reading **Skipping the test means...**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8811b-220">In the apprearing dialog reading **Skipping the test means...**, click **OK**.</span></span>
    
    ![Configure Single Sign-On](./media/samlssojira-tutorial/addon6c.png)

> [!TIP]
> <span data-ttu-id="8811b-222">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8811b-222">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8811b-223">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8811b-223">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8811b-224">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8811b-224">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8811b-225">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8811b-225">Creating an Azure AD test user</span></span>
<span data-ttu-id="8811b-226">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8811b-226">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8811b-228">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8811b-228">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8811b-229">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8811b-229">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/samlssojira-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8811b-231">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8811b-231">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/samlssojira-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8811b-233">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8811b-233">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/samlssojira-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8811b-235">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8811b-235">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8811b-237">a.</span><span class="sxs-lookup"><span data-stu-id="8811b-237">a.</span></span> <span data-ttu-id="8811b-238">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8811b-238">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8811b-239">b.</span><span class="sxs-lookup"><span data-stu-id="8811b-239">b.</span></span> <span data-ttu-id="8811b-240">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8811b-240">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8811b-241">c.</span><span class="sxs-lookup"><span data-stu-id="8811b-241">c.</span></span> <span data-ttu-id="8811b-242">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8811b-242">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8811b-243">d.</span><span class="sxs-lookup"><span data-stu-id="8811b-243">d.</span></span> <span data-ttu-id="8811b-244">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8811b-244">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="8811b-245">Creating a SAML SSO for Jira by resolution GmbH test user</span><span class="sxs-lookup"><span data-stu-id="8811b-245">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="8811b-246">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="8811b-246">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="8811b-247">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="8811b-247">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="8811b-248">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8811b-248">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="8811b-249">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8811b-249">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

1. <span data-ttu-id="8811b-250">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="8811b-250">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/samlssojira-tutorial/user1.png) 

1. <span data-ttu-id="8811b-252">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-252">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Add Employee](./media/samlssojira-tutorial/user2.png) 

1. <span data-ttu-id="8811b-254">Under **User management** tab section, click **create user**.</span><span class="sxs-lookup"><span data-stu-id="8811b-254">Under **User management** tab section, click **create user**.</span></span>

    ![Add Employee](./media/samlssojira-tutorial/user3.png) 

1. <span data-ttu-id="8811b-256">On the **“Create new user”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8811b-256">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/samlssojira-tutorial/user4.png) 

    <span data-ttu-id="8811b-258">a.</span><span class="sxs-lookup"><span data-stu-id="8811b-258">a.</span></span> <span data-ttu-id="8811b-259">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8811b-259">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="8811b-260">b.</span><span class="sxs-lookup"><span data-stu-id="8811b-260">b.</span></span> <span data-ttu-id="8811b-261">In the **Full Name** textbox, type full name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8811b-261">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="8811b-262">c.</span><span class="sxs-lookup"><span data-stu-id="8811b-262">c.</span></span> <span data-ttu-id="8811b-263">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8811b-263">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="8811b-264">d.</span><span class="sxs-lookup"><span data-stu-id="8811b-264">d.</span></span> <span data-ttu-id="8811b-265">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="8811b-265">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="8811b-266">e.</span><span class="sxs-lookup"><span data-stu-id="8811b-266">e.</span></span> <span data-ttu-id="8811b-267">Click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="8811b-267">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8811b-268">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8811b-268">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8811b-269">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="8811b-269">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Assign User][200] 

<span data-ttu-id="8811b-271">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8811b-271">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="8811b-272">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8811b-272">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8811b-274">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="8811b-274">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configure Single Sign-On](./media/samlssojira-tutorial/tutorial_samlssojira_app.png) 

1. <span data-ttu-id="8811b-276">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8811b-276">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8811b-278">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8811b-278">Click **Add** button.</span></span> <span data-ttu-id="8811b-279">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8811b-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8811b-281">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8811b-281">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8811b-282">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8811b-282">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8811b-283">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8811b-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8811b-284">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8811b-284">Testing single sign-on</span></span>

<span data-ttu-id="8811b-285">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8811b-285">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8811b-286">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="8811b-286">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="8811b-287">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8811b-287">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8811b-288">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8811b-288">Additional resources</span></span>

* [<span data-ttu-id="8811b-289">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8811b-289">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8811b-290">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8811b-290">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/samlssojira-tutorial/tutorial_general_203.png

