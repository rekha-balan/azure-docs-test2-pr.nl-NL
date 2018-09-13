---
title: 'Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAML SSO for Confluence by resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: c1a1126026f3d2618a0669e4bd69a84cc1c6c54c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968331"
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="56862-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="56862-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="56862-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56862-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56862-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="56862-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56862-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="56862-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="56862-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="56862-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56862-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="56862-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56862-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="56862-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56862-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="56862-110">Prerequisites</span></span>

<span data-ttu-id="56862-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="56862-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="56862-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="56862-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56862-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="56862-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56862-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="56862-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56862-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="56862-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56862-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="56862-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56862-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56862-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56862-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="56862-118">Scenario description</span></span>
<span data-ttu-id="56862-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="56862-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56862-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="56862-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56862-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span><span class="sxs-lookup"><span data-stu-id="56862-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>
1. <span data-ttu-id="56862-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56862-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="56862-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span><span class="sxs-lookup"><span data-stu-id="56862-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>

<span data-ttu-id="56862-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="56862-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56862-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56862-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56862-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="56862-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="56862-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="56862-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56862-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="56862-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="56862-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="56862-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="56862-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="56862-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Creating an Azure AD test user](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

1. <span data-ttu-id="56862-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="56862-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56862-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56862-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="56862-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="56862-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="56862-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56862-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="56862-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span><span class="sxs-lookup"><span data-stu-id="56862-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="56862-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="56862-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56862-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="56862-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56862-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="56862-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="56862-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56862-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="56862-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="56862-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="56862-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="56862-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="56862-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="56862-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56862-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56862-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56862-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="56862-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="56862-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56862-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="56862-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="56862-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="56862-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="56862-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

1. <span data-ttu-id="56862-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="56862-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="56862-157">a.</span><span class="sxs-lookup"><span data-stu-id="56862-157">a.</span></span> <span data-ttu-id="56862-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="56862-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="56862-159">b.</span><span class="sxs-lookup"><span data-stu-id="56862-159">b.</span></span> <span data-ttu-id="56862-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="56862-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

1. <span data-ttu-id="56862-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="56862-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="56862-162">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="56862-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="56862-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="56862-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="56862-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="56862-165">These values are not real.</span></span> <span data-ttu-id="56862-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="56862-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="56862-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="56862-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

1. <span data-ttu-id="56862-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="56862-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

1. <span data-ttu-id="56862-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="56862-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/tutorial_general_400.png)    
    
1. <span data-ttu-id="56862-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="56862-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

1. <span data-ttu-id="56862-173">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="56862-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon1.png)

1. <span data-ttu-id="56862-175">You are redirected to Administrator Access page.</span><span class="sxs-lookup"><span data-stu-id="56862-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="56862-176">Enter the password and click **Confirm** button.</span><span class="sxs-lookup"><span data-stu-id="56862-176">Enter the password and click **Confirm** button.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon2.png)

1. <span data-ttu-id="56862-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span><span class="sxs-lookup"><span data-stu-id="56862-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon.png)

1. <span data-ttu-id="56862-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="56862-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon7.png)

1. <span data-ttu-id="56862-182">The plugin installation will start.</span><span class="sxs-lookup"><span data-stu-id="56862-182">The plugin installation will start.</span></span> <span data-ttu-id="56862-183">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="56862-183">Click **Close**.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon8.png)

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon9.png)

1.  <span data-ttu-id="56862-186">Click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="56862-186">Click **Manage**.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon10.png)
    
1. <span data-ttu-id="56862-188">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="56862-188">Click **Configure** to configure the new plugin.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon11.png)

1. <span data-ttu-id="56862-190">This new plugin can also be found under **USERS & SECURITY** tab.</span><span class="sxs-lookup"><span data-stu-id="56862-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon3.png)
    
1. <span data-ttu-id="56862-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add new IdP** button to configure the settings of Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="56862-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add new IdP** button to configure the settings of Identity Provider.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon4.png)

1. <span data-ttu-id="56862-194">On **Choose your SAML Identity Provider** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56862-194">On **Choose your SAML Identity Provider** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon5a.png)
 
    <span data-ttu-id="56862-196">a.</span><span class="sxs-lookup"><span data-stu-id="56862-196">a.</span></span> <span data-ttu-id="56862-197">Set **Azure AD** as the IdP type.</span><span class="sxs-lookup"><span data-stu-id="56862-197">Set **Azure AD** as the IdP type.</span></span>
    
    <span data-ttu-id="56862-198">b.</span><span class="sxs-lookup"><span data-stu-id="56862-198">b.</span></span> <span data-ttu-id="56862-199">Add **Name** of the Identity Provider (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56862-199">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="56862-200">c.</span><span class="sxs-lookup"><span data-stu-id="56862-200">c.</span></span> <span data-ttu-id="56862-201">Add **Description** of the Identity Provider (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56862-201">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="56862-202">d.</span><span class="sxs-lookup"><span data-stu-id="56862-202">d.</span></span> <span data-ttu-id="56862-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56862-203">Click **Next**.</span></span>
    
1. <span data-ttu-id="56862-204">On **Identity provider configuration** page, click **Next** button.</span><span class="sxs-lookup"><span data-stu-id="56862-204">On **Identity provider configuration** page, click **Next** button.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon5b.png)

1. <span data-ttu-id="56862-206">On **Import SAML IdP Metadata** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56862-206">On **Import SAML IdP Metadata** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon5c.png)

    <span data-ttu-id="56862-208">a.</span><span class="sxs-lookup"><span data-stu-id="56862-208">a.</span></span> <span data-ttu-id="56862-209">Click **Load File** button and pick Metadata XML file you downloaded in Step 5.</span><span class="sxs-lookup"><span data-stu-id="56862-209">Click **Load File** button and pick Metadata XML file you downloaded in Step 5.</span></span>

    <span data-ttu-id="56862-210">b.</span><span class="sxs-lookup"><span data-stu-id="56862-210">b.</span></span> <span data-ttu-id="56862-211">Click **Import** button.</span><span class="sxs-lookup"><span data-stu-id="56862-211">Click **Import** button.</span></span>
    
    <span data-ttu-id="56862-212">c.</span><span class="sxs-lookup"><span data-stu-id="56862-212">c.</span></span> <span data-ttu-id="56862-213">Wait briefly until import succeeds.</span><span class="sxs-lookup"><span data-stu-id="56862-213">Wait briefly until import succeeds.</span></span>
    
    <span data-ttu-id="56862-214">d.</span><span class="sxs-lookup"><span data-stu-id="56862-214">d.</span></span> <span data-ttu-id="56862-215">Click **Next** button.</span><span class="sxs-lookup"><span data-stu-id="56862-215">Click **Next** button.</span></span>
    
1. <span data-ttu-id="56862-216">On **User ID attribute and transformation** page, click **Next** button.</span><span class="sxs-lookup"><span data-stu-id="56862-216">On **User ID attribute and transformation** page, click **Next** button.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon5d.png)
    
1. <span data-ttu-id="56862-218">On **User creation and update** page, click **Save & Next** to save settings.</span><span class="sxs-lookup"><span data-stu-id="56862-218">On **User creation and update** page, click **Save & Next** to save settings.</span></span>    
    
    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon6a.png)
    
1. <span data-ttu-id="56862-220">On **Test your settings** page, click **Skip test & configure manually** to skip the user test for now.</span><span class="sxs-lookup"><span data-stu-id="56862-220">On **Test your settings** page, click **Skip test & configure manually** to skip the user test for now.</span></span> <span data-ttu-id="56862-221">This will be performed in the next section and requires some settings in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56862-221">This will be performed in the next section and requires some settings in Azure portal.</span></span> 
    
    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon6b.png)
    
1. <span data-ttu-id="56862-223">In the apprearing dialog reading **Skipping the test means...**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="56862-223">In the apprearing dialog reading **Skipping the test means...**, click **OK**.</span></span>
    
    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/addon6c.png)

> [!TIP]
> <span data-ttu-id="56862-225">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="56862-225">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56862-226">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="56862-226">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56862-227">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56862-227">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56862-228">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="56862-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="56862-229">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56862-229">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="56862-231">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56862-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56862-232">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="56862-232">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/samlssoconfluence-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="56862-234">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="56862-234">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/samlssoconfluence-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="56862-236">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="56862-236">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/samlssoconfluence-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="56862-238">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56862-238">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56862-240">a.</span><span class="sxs-lookup"><span data-stu-id="56862-240">a.</span></span> <span data-ttu-id="56862-241">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56862-241">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56862-242">b.</span><span class="sxs-lookup"><span data-stu-id="56862-242">b.</span></span> <span data-ttu-id="56862-243">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56862-243">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56862-244">c.</span><span class="sxs-lookup"><span data-stu-id="56862-244">c.</span></span> <span data-ttu-id="56862-245">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="56862-245">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56862-246">d.</span><span class="sxs-lookup"><span data-stu-id="56862-246">d.</span></span> <span data-ttu-id="56862-247">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="56862-247">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="56862-248">Creating a SAML SSO for Confluence by resolution GmbH test user</span><span class="sxs-lookup"><span data-stu-id="56862-248">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="56862-249">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="56862-249">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="56862-250">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="56862-250">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="56862-251">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56862-251">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="56862-252">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="56862-252">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

1. <span data-ttu-id="56862-253">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="56862-253">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/samlssoconfluence-tutorial/user1.png) 

1. <span data-ttu-id="56862-255">Under Users section, click **Add users** tab. On the **“Add a User”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56862-255">Under Users section, click **Add users** tab. On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="56862-257">a.</span><span class="sxs-lookup"><span data-stu-id="56862-257">a.</span></span> <span data-ttu-id="56862-258">In the **Username** textbox, type the email of user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56862-258">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="56862-259">b.</span><span class="sxs-lookup"><span data-stu-id="56862-259">b.</span></span> <span data-ttu-id="56862-260">In the **Full Name** textbox, type the full name of user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56862-260">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="56862-261">c.</span><span class="sxs-lookup"><span data-stu-id="56862-261">c.</span></span> <span data-ttu-id="56862-262">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="56862-262">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="56862-263">d.</span><span class="sxs-lookup"><span data-stu-id="56862-263">d.</span></span> <span data-ttu-id="56862-264">In the **Password** textbox, type the password for Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56862-264">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="56862-265">e.</span><span class="sxs-lookup"><span data-stu-id="56862-265">e.</span></span> <span data-ttu-id="56862-266">Click **Confirm Password** reenter the password.</span><span class="sxs-lookup"><span data-stu-id="56862-266">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="56862-267">f.</span><span class="sxs-lookup"><span data-stu-id="56862-267">f.</span></span> <span data-ttu-id="56862-268">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="56862-268">Click **Add** button.</span></span>    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56862-269">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="56862-269">Assigning the Azure AD test user</span></span>

<span data-ttu-id="56862-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="56862-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span></span>

![Assign User][200] 

<span data-ttu-id="56862-272">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56862-272">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="56862-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="56862-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="56862-275">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="56862-275">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Configure Single Sign-On](./media/samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

1. <span data-ttu-id="56862-277">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="56862-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="56862-279">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="56862-279">Click **Add** button.</span></span> <span data-ttu-id="56862-280">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="56862-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="56862-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="56862-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="56862-283">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="56862-283">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="56862-284">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="56862-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56862-285">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="56862-285">Testing single sign-on</span></span>

<span data-ttu-id="56862-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="56862-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="56862-287">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="56862-287">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="56862-288">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="56862-288">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56862-289">Additional resources</span><span class="sxs-lookup"><span data-stu-id="56862-289">Additional resources</span></span>

* [<span data-ttu-id="56862-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56862-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="56862-291">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56862-291">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/samlssoconfluence-tutorial/tutorial_general_203.png

