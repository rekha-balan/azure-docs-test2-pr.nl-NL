---
title: 'Tutorial: Azure Active Directory integration with Jobscience | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 92ff93f9836b1ab8157602569c8171f81b976d6f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869046"
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="3a1f7-103">Tutorial: Azure Active Directory integration with Jobscience</span><span class="sxs-lookup"><span data-stu-id="3a1f7-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="3a1f7-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a1f7-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a1f7-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a1f7-106">You can control in Azure AD who has access to Jobscience</span><span class="sxs-lookup"><span data-stu-id="3a1f7-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="3a1f7-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3a1f7-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a1f7-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3a1f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3a1f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3a1f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a1f7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3a1f7-110">Prerequisites</span></span>

<span data-ttu-id="3a1f7-111">To configure Azure AD integration with Jobscience, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="3a1f7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3a1f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a1f7-113">A Jobscience single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3a1f7-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a1f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a1f7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a1f7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a1f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a1f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a1f7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3a1f7-118">Scenario description</span></span>
<span data-ttu-id="3a1f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a1f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a1f7-121">Adding Jobscience from the gallery</span><span class="sxs-lookup"><span data-stu-id="3a1f7-121">Adding Jobscience from the gallery</span></span>
1. <span data-ttu-id="3a1f7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3a1f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="3a1f7-123">Adding Jobscience from the gallery</span><span class="sxs-lookup"><span data-stu-id="3a1f7-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="3a1f7-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a1f7-125">**To add Jobscience from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a1f7-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a1f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="3a1f7-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a1f7-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="3a1f7-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="3a1f7-133">In the search box, type **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-133">In the search box, type **Jobscience**.</span></span>

    ![Creating an Azure AD test user](./media/jobscience-tutorial/tutorial_jobscience_search.png)

1. <span data-ttu-id="3a1f7-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a1f7-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3a1f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a1f7-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3a1f7-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a1f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="3a1f7-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="3a1f7-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a1f7-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a1f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3a1f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3a1f7-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3a1f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3a1f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a1f7-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3a1f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a1f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="3a1f7-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a1f7-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="3a1f7-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="3a1f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/jobscience-tutorial/tutorial_jobscience_samlbase.png)

1. <span data-ttu-id="3a1f7-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="3a1f7-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="3a1f7-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3a1f7-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-158">This value is not real.</span></span> <span data-ttu-id="3a1f7-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3a1f7-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
1. <span data-ttu-id="3a1f7-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/jobscience-tutorial/tutorial_jobscience_certificate.png) 

1. <span data-ttu-id="3a1f7-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/jobscience-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="3a1f7-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a1f7-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3a1f7-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/jobscience-tutorial/tutorial_jobscience_configure.png) 

1. <span data-ttu-id="3a1f7-168">Log in to your Jobscience company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-168">Log in to your Jobscience company site as an administrator.</span></span>

1. <span data-ttu-id="3a1f7-169">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="3a1f7-170">![Setup](./media/jobscience-tutorial/IC784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-170">![Setup](./media/jobscience-tutorial/IC784358.png "Setup")</span></span>

1. <span data-ttu-id="3a1f7-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="3a1f7-172">![My Domain](./media/jobscience-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-172">![My Domain](./media/jobscience-tutorial/ic767825.png "My Domain")</span></span>

1. <span data-ttu-id="3a1f7-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="3a1f7-174">![Domain Deployed to User](./media/jobscience-tutorial/ic784377.png "Domain Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-174">![Domain Deployed to User](./media/jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

1. <span data-ttu-id="3a1f7-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="3a1f7-176">![Security Controls](./media/jobscience-tutorial/ic784364.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-176">![Security Controls](./media/jobscience-tutorial/ic784364.png "Security Controls")</span></span>

1. <span data-ttu-id="3a1f7-177">In the **Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="3a1f7-178">![Single Sign-On Settings](./media/jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-178">![Single Sign-On Settings](./media/jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="3a1f7-179">a.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-179">a.</span></span> <span data-ttu-id="3a1f7-180">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="3a1f7-181">b.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-181">b.</span></span> <span data-ttu-id="3a1f7-182">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-182">Click **New**.</span></span>

1. <span data-ttu-id="3a1f7-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="3a1f7-184">![SAML Single Sign-On Setting](./media/jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-184">![SAML Single Sign-On Setting](./media/jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="3a1f7-185">a.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-185">a.</span></span> <span data-ttu-id="3a1f7-186">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="3a1f7-187">b.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-187">b.</span></span> <span data-ttu-id="3a1f7-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a1f7-189">c.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-189">c.</span></span> <span data-ttu-id="3a1f7-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="3a1f7-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="3a1f7-191">d.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-191">d.</span></span> <span data-ttu-id="3a1f7-192">Click **Browse** to upload your Azure AD certificate.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="3a1f7-193">e.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-193">e.</span></span> <span data-ttu-id="3a1f7-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="3a1f7-195">f.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-195">f.</span></span> <span data-ttu-id="3a1f7-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="3a1f7-197">g.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-197">g.</span></span> <span data-ttu-id="3a1f7-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a1f7-199">h.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-199">h.</span></span> <span data-ttu-id="3a1f7-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a1f7-201">i.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-201">i.</span></span> <span data-ttu-id="3a1f7-202">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-202">Click **Save**.</span></span>

1. <span data-ttu-id="3a1f7-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="3a1f7-204">![My Domain](./media/jobscience-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-204">![My Domain](./media/jobscience-tutorial/ic767825.png "My Domain")</span></span>

1. <span data-ttu-id="3a1f7-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="3a1f7-206">![Login Page Branding](./media/jobscience-tutorial/ic767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-206">![Login Page Branding](./media/jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

1. <span data-ttu-id="3a1f7-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="3a1f7-208">Select it, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="3a1f7-209">![Login Page Branding](./media/jobscience-tutorial/ic784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-209">![Login Page Branding](./media/jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

1. <span data-ttu-id="3a1f7-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="3a1f7-211">![Security Controls](./media/jobscience-tutorial/ic784368.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-211">![Security Controls](./media/jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="3a1f7-212">Click the SSO profile you have created in the step above.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="3a1f7-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="3a1f7-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="3a1f7-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3a1f7-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a1f7-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a1f7-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a1f7-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a1f7-217">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3a1f7-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a1f7-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="3a1f7-220">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a1f7-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a1f7-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/jobscience-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="3a1f7-223">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/jobscience-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="3a1f7-225">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/jobscience-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="3a1f7-227">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a1f7-229">a.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-229">a.</span></span> <span data-ttu-id="3a1f7-230">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a1f7-231">b.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-231">b.</span></span> <span data-ttu-id="3a1f7-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a1f7-233">c.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-233">c.</span></span> <span data-ttu-id="3a1f7-234">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a1f7-235">d.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-235">d.</span></span> <span data-ttu-id="3a1f7-236">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="3a1f7-237">Creating a Jobscience test user</span><span class="sxs-lookup"><span data-stu-id="3a1f7-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="3a1f7-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="3a1f7-239">In the case of Jobscience, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="3a1f7-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="3a1f7-241">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a1f7-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3a1f7-242">Log in to your **Jobscience** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-242">Log in to your **Jobscience** company site as administrator.</span></span>

1. <span data-ttu-id="3a1f7-243">Go to Setup.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-243">Go to Setup.</span></span>
   
   <span data-ttu-id="3a1f7-244">![Setup](./media/jobscience-tutorial/ic784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-244">![Setup](./media/jobscience-tutorial/ic784358.png "Setup")</span></span>
1. <span data-ttu-id="3a1f7-245">Go to **Manage Users \> Users**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="3a1f7-246">![Users](./media/jobscience-tutorial/ic784369.png "Users")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-246">![Users](./media/jobscience-tutorial/ic784369.png "Users")</span></span>
1. <span data-ttu-id="3a1f7-247">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-247">Click **New User**.</span></span>
   
   <span data-ttu-id="3a1f7-248">![All Users](./media/jobscience-tutorial/ic784370.png "All Users")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-248">![All Users](./media/jobscience-tutorial/ic784370.png "All Users")</span></span>
1. <span data-ttu-id="3a1f7-249">On the **Edit User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a1f7-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="3a1f7-250">![User Edit](./media/jobscience-tutorial/ic784371.png "User Edit")</span><span class="sxs-lookup"><span data-stu-id="3a1f7-250">![User Edit](./media/jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="3a1f7-251">a.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-251">a.</span></span> <span data-ttu-id="3a1f7-252">In the **First Name** textbox, type a first name of the user like Britta.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="3a1f7-253">b.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-253">b.</span></span> <span data-ttu-id="3a1f7-254">In the **Last Name** textbox, type a last name of the user like Simon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="3a1f7-255">c.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-255">c.</span></span> <span data-ttu-id="3a1f7-256">In the **Alias** textbox, type an alias name of the user like brittas.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="3a1f7-257">d.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-257">d.</span></span> <span data-ttu-id="3a1f7-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="3a1f7-259">e.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-259">e.</span></span> <span data-ttu-id="3a1f7-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="3a1f7-261">f.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-261">f.</span></span> <span data-ttu-id="3a1f7-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="3a1f7-263">g.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-263">g.</span></span> <span data-ttu-id="3a1f7-264">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="3a1f7-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3a1f7-266">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3a1f7-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3a1f7-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Assign User][200] 

<span data-ttu-id="3a1f7-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a1f7-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="3a1f7-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="3a1f7-272">In the applications list, select **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-272">In the applications list, select **Jobscience**.</span></span>

    ![Configure Single Sign-On](./media/jobscience-tutorial/tutorial_jobscience_app.png) 

1. <span data-ttu-id="3a1f7-274">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="3a1f7-276">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-276">Click **Add** button.</span></span> <span data-ttu-id="3a1f7-277">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="3a1f7-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3a1f7-280">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-280">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3a1f7-281">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a1f7-282">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="3a1f7-282">Testing single sign-on</span></span>

<span data-ttu-id="3a1f7-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a1f7-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span><span class="sxs-lookup"><span data-stu-id="3a1f7-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="3a1f7-285">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a1f7-285">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a1f7-286">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3a1f7-286">Additional resources</span></span>

* [<span data-ttu-id="3a1f7-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a1f7-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3a1f7-288">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a1f7-288">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/jobscience-tutorial/tutorial_general_01.png
[2]: ./media/jobscience-tutorial/tutorial_general_02.png
[3]: ./media/jobscience-tutorial/tutorial_general_03.png
[4]: ./media/jobscience-tutorial/tutorial_general_04.png

[100]: ./media/jobscience-tutorial/tutorial_general_100.png

[200]: ./media/jobscience-tutorial/tutorial_general_200.png
[201]: ./media/jobscience-tutorial/tutorial_general_201.png
[202]: ./media/jobscience-tutorial/tutorial_general_202.png
[203]: ./media/jobscience-tutorial/tutorial_general_203.png

