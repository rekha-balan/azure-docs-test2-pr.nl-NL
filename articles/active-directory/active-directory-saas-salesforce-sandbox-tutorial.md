---
title: 'Tutorial: Azure Active Directory integration with Salesforce Sandbox | Microsoft Docs'
description: Learn how to use Salesforce Sandbox with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: 98c442c2cddec3312f0500ae99dd8d6cd1bd75b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556677"
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="4114a-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4114a-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="4114a-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="4114a-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="4114a-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="4114a-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span><span class="sxs-lookup"><span data-stu-id="4114a-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="4114a-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="4114a-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="4114a-108">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="4114a-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="4114a-109">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4114a-109">A valid Azure subscription</span></span>
* <span data-ttu-id="4114a-110">A sandbox in Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="4114a-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="4114a-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4114a-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="4114a-112">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4114a-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="4114a-113">Enabling the application integration for Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4114a-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="4114a-114">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="4114a-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="4114a-115">Enabling your domain</span><span class="sxs-lookup"><span data-stu-id="4114a-115">Enabling your domain</span></span>
4. <span data-ttu-id="4114a-116">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="4114a-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="4114a-117">Assigning users</span><span class="sxs-lookup"><span data-stu-id="4114a-117">Assigning users</span></span>

<span data-ttu-id="4114a-118">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="4114a-118">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="4114a-119">Enable the application integration for Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4114a-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="4114a-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="4114a-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4114a-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="4114a-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4114a-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4114a-123">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4114a-123">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4114a-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4114a-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4114a-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4114a-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="4114a-126">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4114a-126">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4114a-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span><span class="sxs-lookup"><span data-stu-id="4114a-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="4114a-128">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span><span class="sxs-lookup"><span data-stu-id="4114a-128">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="4114a-129">In the **search box**, type **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="4114a-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="4114a-130">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="4114a-130">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="4114a-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4114a-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="4114a-132">![Salesforce Sandbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="4114a-132">![Salesforce Sandbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="4114a-133">Configur single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="4114a-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="4114a-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="4114a-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="4114a-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4114a-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="4114a-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="4114a-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4114a-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4114a-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="4114a-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4114a-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4114a-139">![Salesforce Sandbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="4114a-139">![Salesforce Sandbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="4114a-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4114a-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="4114a-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="4114a-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="4114a-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span><span class="sxs-lookup"><span data-stu-id="4114a-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="4114a-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4114a-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="4114a-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4114a-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="4114a-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4114a-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="4114a-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4114a-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="4114a-147">In the menu on the top, click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="4114a-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="4114a-148">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="4114a-148">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="4114a-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="4114a-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="4114a-150">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="4114a-150">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="4114a-151">On the Single Sign-On Settings section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4114a-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="4114a-152">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="4114a-152">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="4114a-153">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="4114a-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="4114a-154">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="4114a-154">Click **New**.</span></span>
10. <span data-ttu-id="4114a-155">On the SAML Single Sign-On Settings section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4114a-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="4114a-156">![SAML Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="4114a-156">![SAML Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="4114a-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="4114a-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="4114a-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="4114a-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span><span class="sxs-lookup"><span data-stu-id="4114a-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="4114a-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4114a-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="4114a-161">Click **Browse** to upload the downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="4114a-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="4114a-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span><span class="sxs-lookup"><span data-stu-id="4114a-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="4114a-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="4114a-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="4114a-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="4114a-165">SFDC does not support SAML logout.</span><span class="sxs-lookup"><span data-stu-id="4114a-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="4114a-166">As a workaround, paste 'https://login.windows.net/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-166">As a workaround, paste 'https://login.windows.net/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="4114a-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="4114a-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="4114a-168">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4114a-168">Click **Save**.</span></span>
11. <span data-ttu-id="4114a-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="4114a-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="4114a-170">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4114a-170">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="4114a-171">Enable your domain</span><span class="sxs-lookup"><span data-stu-id="4114a-171">Enable your domain</span></span>
<span data-ttu-id="4114a-172">This section assumes that you already have created a domain.</span><span class="sxs-lookup"><span data-stu-id="4114a-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="4114a-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="4114a-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="4114a-174">**To enable your domain, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4114a-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="4114a-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span><span class="sxs-lookup"><span data-stu-id="4114a-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="4114a-176">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="4114a-176">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4114a-177">Please make sure that your domain has been configured correctly.</span><span class="sxs-lookup"><span data-stu-id="4114a-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="4114a-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4114a-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="4114a-179">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="4114a-179">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="4114a-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="4114a-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="4114a-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="4114a-182">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="4114a-182">Configure user provisioning</span></span>
<span data-ttu-id="4114a-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="4114a-184">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4114a-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="4114a-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span><span class="sxs-lookup"><span data-stu-id="4114a-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="4114a-186">![My Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span><span class="sxs-lookup"><span data-stu-id="4114a-186">![My Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="4114a-187">From your user menu, select **My Settings** to open your **My Settings** page.</span><span class="sxs-lookup"><span data-stu-id="4114a-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="4114a-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span><span class="sxs-lookup"><span data-stu-id="4114a-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="4114a-189">![My Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span><span class="sxs-lookup"><span data-stu-id="4114a-189">![My Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="4114a-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span><span class="sxs-lookup"><span data-stu-id="4114a-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="4114a-191">![New Token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span><span class="sxs-lookup"><span data-stu-id="4114a-191">![New Token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="4114a-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span><span class="sxs-lookup"><span data-stu-id="4114a-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="4114a-193">Review this email and copy the security token value.</span><span class="sxs-lookup"><span data-stu-id="4114a-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="4114a-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="4114a-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="4114a-195">![Configure user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span><span class="sxs-lookup"><span data-stu-id="4114a-195">![Configure user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="4114a-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="4114a-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="4114a-197">![Salesforce Sandbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="4114a-197">![Salesforce Sandbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="4114a-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span><span class="sxs-lookup"><span data-stu-id="4114a-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="4114a-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="4114a-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="4114a-200">In the **User Security Token** textbox, paste the security token value.</span><span class="sxs-lookup"><span data-stu-id="4114a-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="4114a-201">Click **Validate** to verify your configuration.</span><span class="sxs-lookup"><span data-stu-id="4114a-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="4114a-202">Click the **Next** button to open the **Confirmation** page.</span><span class="sxs-lookup"><span data-stu-id="4114a-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="4114a-203">On the **Confirmation** page, click **Complete** to save your configuration.</span><span class="sxs-lookup"><span data-stu-id="4114a-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="4114a-204">Assigning users</span><span class="sxs-lookup"><span data-stu-id="4114a-204">Assigning users</span></span>

<span data-ttu-id="4114a-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="4114a-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="4114a-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4114a-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="4114a-207">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="4114a-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4114a-208">On the \*\*Salesforce Sandbox \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="4114a-208">On the \*\*Salesforce Sandbox \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4114a-209">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="4114a-209">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="4114a-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="4114a-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="4114a-211">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="4114a-211">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4114a-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4114a-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="4114a-213">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4114a-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="4114a-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4114a-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

























