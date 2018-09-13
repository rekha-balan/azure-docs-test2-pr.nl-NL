---
title: 'Tutorial: Azure Active Directory integration with Jobscience | Microsoft Docs'
description: Learn how to use Jobscience with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 5bb639354bbb7e8b48544a20dd7d640912a75c11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553879"
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="1787a-103">Tutorial: Azure Active Directory integration with Jobscience</span><span class="sxs-lookup"><span data-stu-id="1787a-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>
<span data-ttu-id="1787a-104">The objective of this tutorial is to show the integration of Azure and Jobscience.</span><span class="sxs-lookup"><span data-stu-id="1787a-104">The objective of this tutorial is to show the integration of Azure and Jobscience.</span></span>  
<span data-ttu-id="1787a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="1787a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1787a-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="1787a-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1787a-107">A Jobscience single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1787a-107">A Jobscience single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="1787a-108">After completing this tutorial, the Azure AD users you have assigned to Jobscience will be able to single sign into the application at your Jobscience company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1787a-108">After completing this tutorial, the Azure AD users you have assigned to Jobscience will be able to single sign into the application at your Jobscience company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="1787a-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1787a-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="1787a-110">Enabling the application integration for Jobscience</span><span class="sxs-lookup"><span data-stu-id="1787a-110">Enabling the application integration for Jobscience</span></span>
2. <span data-ttu-id="1787a-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="1787a-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="1787a-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="1787a-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="1787a-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="1787a-113">Assigning users</span></span>

<span data-ttu-id="1787a-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784341.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="1787a-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784341.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-jobscience"></a><span data-ttu-id="1787a-115">Enable the application integration for Jobscience</span><span class="sxs-lookup"><span data-stu-id="1787a-115">Enable the application integration for Jobscience</span></span>
<span data-ttu-id="1787a-116">The objective of this section is to outline how to enable the application integration for Jobscience.</span><span class="sxs-lookup"><span data-stu-id="1787a-116">The objective of this section is to outline how to enable the application integration for Jobscience.</span></span>

<span data-ttu-id="1787a-117">**To enable the application integration for Jobscience, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1787a-117">**To enable the application integration for Jobscience, perform the following steps:**</span></span>
1. <span data-ttu-id="1787a-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1787a-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1787a-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1787a-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1787a-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1787a-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1787a-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1787a-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="1787a-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="1787a-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1787a-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1787a-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="1787a-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="1787a-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1787a-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1787a-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="1787a-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="1787a-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1787a-127">In the **search box**, type **jobscience**.</span><span class="sxs-lookup"><span data-stu-id="1787a-127">In the **search box**, type **jobscience**.</span></span>
   
   <span data-ttu-id="1787a-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784342.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="1787a-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784342.png "Application Gallery")</span></span>
7. <span data-ttu-id="1787a-129">In the results pane, select **Jobscience**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1787a-129">In the results pane, select **Jobscience**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="1787a-130">![Jobscience](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784357.png "Jobscience")</span><span class="sxs-lookup"><span data-stu-id="1787a-130">![Jobscience](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784357.png "Jobscience")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1787a-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="1787a-131">Configure single sign-on</span></span>

<span data-ttu-id="1787a-132">The objective of this section is to outline how to enable users to authenticate to Jobscience with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="1787a-132">The objective of this section is to outline how to enable users to authenticate to Jobscience with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="1787a-133">Configuring single sign-on for Jobscience requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="1787a-133">Configuring single sign-on for Jobscience requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="1787a-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="1787a-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="1787a-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1787a-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="1787a-136">Log in to your Jobscience company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1787a-136">Log in to your Jobscience company site as an administrator.</span></span>
2. <span data-ttu-id="1787a-137">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="1787a-137">Go to **Setup**.</span></span>
   
   <span data-ttu-id="1787a-138">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="1787a-138">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>
3. <span data-ttu-id="1787a-139">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="1787a-139">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="1787a-140">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="1787a-140">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767825.png "My Domain")</span></span>
4. <span data-ttu-id="1787a-141">To verify that your domain has been setup correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span><span class="sxs-lookup"><span data-stu-id="1787a-141">To verify that your domain has been setup correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
   <span data-ttu-id="1787a-142">![Doman Deployed to User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784377.png "Doman Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="1787a-142">![Doman Deployed to User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784377.png "Doman Deployed to User")</span></span>
5. <span data-ttu-id="1787a-143">In a different web browser window, log in to your Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="1787a-143">In a different web browser window, log in to your Azure classic portal.</span></span>
6. <span data-ttu-id="1787a-144">On the **Jobscience** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="1787a-144">On the **Jobscience** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="1787a-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784360.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1787a-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784360.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="1787a-146">On the **How would you like users to sign on to Jobscience** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1787a-146">On the **How would you like users to sign on to Jobscience** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1787a-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784361.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1787a-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784361.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="1787a-148">On the **Configure App URL** page, in the **Jobscience Sign In URL** textbox, type your URL using the following pattern "*http://company.my.salesforce.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1787a-148">On the **Configure App URL** page, in the **Jobscience Sign In URL** textbox, type your URL using the following pattern "*http://company.my.salesforce.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="1787a-149">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784362.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="1787a-149">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784362.png "Configure App URL")</span></span>
9. <span data-ttu-id="1787a-150">On the **Configure single sign-on at Jobscience** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="1787a-150">On the **Configure single sign-on at Jobscience** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="1787a-151">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784363.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1787a-151">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784363.png "Configure Single Sign-On")</span></span>
10. <span data-ttu-id="1787a-152">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="1787a-152">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="1787a-153">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784364.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="1787a-153">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784364.png "Security Controls")</span></span>
11. <span data-ttu-id="1787a-154">In the **Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1787a-154">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="1787a-155">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC781026.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="1787a-155">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC781026.png "Single Sign-On Settings")</span></span>
    
    1. <span data-ttu-id="1787a-156">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="1787a-156">Select **SAML Enabled**.</span></span>
    2. <span data-ttu-id="1787a-157">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="1787a-157">Click **New**.</span></span>
12. <span data-ttu-id="1787a-158">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1787a-158">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="1787a-159">![SAML Single Sign-On Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784365.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="1787a-159">![SAML Single Sign-On Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784365.png "SAML Single Sign-On Setting")</span></span>
    
    1. <span data-ttu-id="1787a-160">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="1787a-160">In the **Name** textbox, type a name for your configuration.</span></span>
    2. <span data-ttu-id="1787a-161">In the Azure classic portal, on the **Configure single sign-on at Jobscience** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="1787a-161">In the Azure classic portal, on the **Configure single sign-on at Jobscience** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
    3. <span data-ttu-id="1787a-162">In the **Entity Id** textbox, type **https://salesforce-jobscience.com**</span><span class="sxs-lookup"><span data-stu-id="1787a-162">In the **Entity Id** textbox, type **https://salesforce-jobscience.com**</span></span>
    4. <span data-ttu-id="1787a-163">Click **Browse** to upload your Azure AD certificate.</span><span class="sxs-lookup"><span data-stu-id="1787a-163">Click **Browse** to upload your Azure AD certificate.</span></span>
    5. <span data-ttu-id="1787a-164">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span><span class="sxs-lookup"><span data-stu-id="1787a-164">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    6. <span data-ttu-id="1787a-165">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="1787a-165">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    7. <span data-ttu-id="1787a-166">In the Azure classic portal, on the **Configure single sign-on at Jobscience** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1787a-166">In the Azure classic portal, on the **Configure single sign-on at Jobscience** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span>
    8. <span data-ttu-id="1787a-167">In the Azure classic portal, on the **Configure single sign-on at Jobscience** dialogue page, copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1787a-167">In the Azure classic portal, on the **Configure single sign-on at Jobscience** dialogue page, copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span></span>
    9. <span data-ttu-id="1787a-168">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1787a-168">Click **Save**.</span></span>
13. <span data-ttu-id="1787a-169">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="1787a-169">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="1787a-170">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="1787a-170">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767825.png "My Domain")</span></span>
14. <span data-ttu-id="1787a-171">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="1787a-171">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="1787a-172">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="1787a-172">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767826.png "Login Page Branding")</span></span>
15. <span data-ttu-id="1787a-173">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span><span class="sxs-lookup"><span data-stu-id="1787a-173">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="1787a-174">Select it, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1787a-174">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="1787a-175">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="1787a-175">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784366.png "Login Page Branding")</span></span>
16. <span data-ttu-id="1787a-176">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="1787a-176">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="1787a-177">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784367.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1787a-177">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784367.png "Configure Single Sign-On")</span></span>

<span data-ttu-id="1787a-178">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span><span class="sxs-lookup"><span data-stu-id="1787a-178">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

<span data-ttu-id="1787a-179">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784368.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="1787a-179">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784368.png "Security Controls")</span></span>

<span data-ttu-id="1787a-180">Click the SSO profile you have created in the step above.</span><span class="sxs-lookup"><span data-stu-id="1787a-180">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="1787a-181">This page shows the Single Sign on URL for your company (e.g. *https://companyname.my.salesforce.com?so=companyid*).</span><span class="sxs-lookup"><span data-stu-id="1787a-181">This page shows the Single Sign on URL for your company (e.g. *https://companyname.my.salesforce.com?so=companyid*).</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="1787a-182">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="1787a-182">Configure user provisioning</span></span>
<span data-ttu-id="1787a-183">In order to enable Azure AD users to log into Jobscience, they must be provisioned into Jobscience.</span><span class="sxs-lookup"><span data-stu-id="1787a-183">In order to enable Azure AD users to log into Jobscience, they must be provisioned into Jobscience.</span></span>  
<span data-ttu-id="1787a-184">In the case of Jobscience, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="1787a-184">In the case of Jobscience, provisioning is a manual task.</span></span>

<span data-ttu-id="1787a-185">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1787a-185">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="1787a-186">Log in to your **Jobscience** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="1787a-186">Log in to your **Jobscience** company site as administrator.</span></span>
2. <span data-ttu-id="1787a-187">Go to Setup.</span><span class="sxs-lookup"><span data-stu-id="1787a-187">Go to Setup.</span></span>
   
   <span data-ttu-id="1787a-188">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="1787a-188">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>
3. <span data-ttu-id="1787a-189">Go to **Manage Users \> Users**.</span><span class="sxs-lookup"><span data-stu-id="1787a-189">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="1787a-190">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784369.png "Users")</span><span class="sxs-lookup"><span data-stu-id="1787a-190">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784369.png "Users")</span></span>
4. <span data-ttu-id="1787a-191">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="1787a-191">Click **New User**.</span></span>
   
   <span data-ttu-id="1787a-192">![All Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784370.png "All Users")</span><span class="sxs-lookup"><span data-stu-id="1787a-192">![All Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784370.png "All Users")</span></span>
5. <span data-ttu-id="1787a-193">On the **Edit User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1787a-193">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="1787a-194">![User Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784371.png "User Edit")</span><span class="sxs-lookup"><span data-stu-id="1787a-194">![User Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784371.png "User Edit")</span></span>
   
   1. <span data-ttu-id="1787a-195">Type the first name, last name, alias, email, user name and nickname properties of the Azure AD user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="1787a-195">Type the first name, last name, alias, email, user name and nickname properties of the Azure AD user you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="1787a-196">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1787a-196">Click **Save**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1787a-197">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span><span class="sxs-lookup"><span data-stu-id="1787a-197">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="1787a-198">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="1787a-198">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="1787a-199">Assign users</span><span class="sxs-lookup"><span data-stu-id="1787a-199">Assign users</span></span>
<span data-ttu-id="1787a-200">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="1787a-200">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="1787a-201">**To assign users to Jobscience, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1787a-201">**To assign users to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="1787a-202">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="1787a-202">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1787a-203">On the **Jobscience** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="1787a-203">On the **Jobscience** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1787a-204">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784372.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="1787a-204">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC784372.png "Assign Users")</span></span>
3. <span data-ttu-id="1787a-205">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="1787a-205">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="1787a-206">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="1787a-206">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscience-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1787a-207">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1787a-207">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1787a-208">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1787a-208">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





























