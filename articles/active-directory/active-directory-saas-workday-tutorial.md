---
title: 'Tutorial: Azure Active Directory integration with Workday | Microsoft Docs'
description: Learn how to use Workday with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: d0527222286880123562327096ad24dff357c8cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556602"
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="1d954-103">Tutorial: Azure Active Directory integration with Workday</span><span class="sxs-lookup"><span data-stu-id="1d954-103">Tutorial: Azure Active Directory integration with Workday</span></span>
<span data-ttu-id="1d954-104">The objective of this tutorial is to show the integration of Azure and Workday.</span><span class="sxs-lookup"><span data-stu-id="1d954-104">The objective of this tutorial is to show the integration of Azure and Workday.</span></span> <span data-ttu-id="1d954-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="1d954-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1d954-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="1d954-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1d954-107">A tenant in Workday</span><span class="sxs-lookup"><span data-stu-id="1d954-107">A tenant in Workday</span></span>

<span data-ttu-id="1d954-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1d954-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="1d954-109">Enabling the application integration for Workday</span><span class="sxs-lookup"><span data-stu-id="1d954-109">Enabling the application integration for Workday</span></span>
2. <span data-ttu-id="1d954-110">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="1d954-110">Configuring single sign-on</span></span>
3. <span data-ttu-id="1d954-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="1d954-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="1d954-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="1d954-112">Configuring user provisioning</span></span>

<span data-ttu-id="1d954-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782919.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="1d954-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782919.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-workday"></a><span data-ttu-id="1d954-114">Enabling the application integration for Workday</span><span class="sxs-lookup"><span data-stu-id="1d954-114">Enabling the application integration for Workday</span></span>
<span data-ttu-id="1d954-115">The objective of this section is to outline how to enable the application integration for Salesforce.</span><span class="sxs-lookup"><span data-stu-id="1d954-115">The objective of this section is to outline how to enable the application integration for Salesforce.</span></span>

### <a name="to-enable-the-application-integration-for-workday-perform-the-following-steps"></a><span data-ttu-id="1d954-116">To enable the application integration for Workday, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-116">To enable the application integration for Workday, perform the following steps:</span></span>
1. <span data-ttu-id="1d954-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d954-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="1d954-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1d954-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="1d954-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1d954-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1d954-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1d954-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="1d954-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="1d954-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="1d954-122">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span><span class="sxs-lookup"><span data-stu-id="1d954-122">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
    <span data-ttu-id="1d954-123">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC700995.png "What do you want to do?")</span><span class="sxs-lookup"><span data-stu-id="1d954-123">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC700995.png "What do you want to do?")</span></span>

5. <span data-ttu-id="1d954-124">In the **search box**, type **Workday**.</span><span class="sxs-lookup"><span data-stu-id="1d954-124">In the **search box**, type **Workday**.</span></span>
   
    <span data-ttu-id="1d954-125">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC701021.png "Workday")</span><span class="sxs-lookup"><span data-stu-id="1d954-125">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC701021.png "Workday")</span></span>

6. <span data-ttu-id="1d954-126">In the results pane, select **Workday**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1d954-126">In the results pane, select **Workday**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="1d954-127">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC701022.png "Workday")</span><span class="sxs-lookup"><span data-stu-id="1d954-127">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC701022.png "Workday")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="1d954-128">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="1d954-128">Configuring single sign-on</span></span>
<span data-ttu-id="1d954-129">The objective of this section is to outline how to enable users to authenticate to Workday with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="1d954-129">The objective of this section is to outline how to enable users to authenticate to Workday with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="1d954-130">As part of this procedure, you are required to create a base-64 encoded certificate.</span><span class="sxs-lookup"><span data-stu-id="1d954-130">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span>  
<span data-ttu-id="1d954-131">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="1d954-131">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="1d954-132">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-132">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="1d954-133">On the **Workday** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="1d954-133">On the **Workday** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="1d954-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782920.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1d954-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782920.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="1d954-135">On the **How would you like users to sign on to Workday** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1d954-135">On the **How would you like users to sign on to Workday** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="1d954-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782921.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1d954-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782921.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="1d954-137">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1d954-137">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="1d954-138">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782957.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="1d954-138">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782957.png "Configure App URL")</span></span>
   
    <span data-ttu-id="1d954-139">a.</span><span class="sxs-lookup"><span data-stu-id="1d954-139">a.</span></span> <span data-ttu-id="1d954-140">In the **Sign On URL** textbox, type the URL used by your users to sign in to Workday using the following pattern: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="1d954-140">In the **Sign On URL** textbox, type the URL used by your users to sign in to Workday using the following pattern: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>
   
    <span data-ttu-id="1d954-141">b.</span><span class="sxs-lookup"><span data-stu-id="1d954-141">b.</span></span>  <span data-ttu-id="1d954-142">In the **Workday Reply URL** textbox, type the Workday reply URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="1d954-142">In the **Workday Reply URL** textbox, type the Workday reply URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="1d954-143">Your reply URL must have a sub-domain (e.g.: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span><span class="sxs-lookup"><span data-stu-id="1d954-143">Your reply URL must have a sub-domain (e.g.: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="1d954-144">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span><span class="sxs-lookup"><span data-stu-id="1d954-144">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> 
    > 
    > 

4. <span data-ttu-id="1d954-145">On the **Configure single sign-on at Workday** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1d954-145">On the **Configure single sign-on at Workday** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
 
    <span data-ttu-id="1d954-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782922.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1d954-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782922.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="1d954-147">In a different web browser window, log into your Workday company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1d954-147">In a different web browser window, log into your Workday company site as an administrator.</span></span>

6. <span data-ttu-id="1d954-148">Go to **Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="1d954-148">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="1d954-149">![Workbench](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="1d954-149">![Workbench](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

7. <span data-ttu-id="1d954-150">Go to **Account Administration**.</span><span class="sxs-lookup"><span data-stu-id="1d954-150">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="1d954-151">![Account Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span><span class="sxs-lookup"><span data-stu-id="1d954-151">![Account Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

8. <span data-ttu-id="1d954-152">Go to **Edit Tenant Setup – Security**.</span><span class="sxs-lookup"><span data-stu-id="1d954-152">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="1d954-153">![Edit Tenant Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span><span class="sxs-lookup"><span data-stu-id="1d954-153">![Edit Tenant Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

9. <span data-ttu-id="1d954-154">In the **Redirection URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-154">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1d954-155">![Redirection URLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span><span class="sxs-lookup"><span data-stu-id="1d954-155">![Redirection URLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="1d954-156">a.</span><span class="sxs-lookup"><span data-stu-id="1d954-156">a.</span></span> <span data-ttu-id="1d954-157">Click **Add Row**.</span><span class="sxs-lookup"><span data-stu-id="1d954-157">Click **Add Row**.</span></span>
   
    <span data-ttu-id="1d954-158">b.</span><span class="sxs-lookup"><span data-stu-id="1d954-158">b.</span></span> <span data-ttu-id="1d954-159">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Workday Tenant URL** you have entered on the **Configure App URL** page of the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="1d954-159">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Workday Tenant URL** you have entered on the **Configure App URL** page of the Azure classic portal.</span></span>
   
    <span data-ttu-id="1d954-160">c.</span><span class="sxs-lookup"><span data-stu-id="1d954-160">c.</span></span> <span data-ttu-id="1d954-161">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Single Sign-Out Service URL**, and then paste it into the **Logout Redirect URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1d954-161">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Single Sign-Out Service URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="1d954-162">d.</span><span class="sxs-lookup"><span data-stu-id="1d954-162">d.</span></span>  <span data-ttu-id="1d954-163">In **Environment** textbox, type the environment name.</span><span class="sxs-lookup"><span data-stu-id="1d954-163">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="1d954-164">The value of the Environment attribute is tied to the value of the tenant URL:</span><span class="sxs-lookup"><span data-stu-id="1d954-164">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    >-   <span data-ttu-id="1d954-165">If the domain name of the Workday tenant URL starts with impl (e.g.: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span><span class="sxs-lookup"><span data-stu-id="1d954-165">If the domain name of the Workday tenant URL starts with impl (e.g.: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    >-   <span data-ttu-id="1d954-166">If the domain name starts with something else, you need to contact Workday to get the matching **Environment** value.</span><span class="sxs-lookup"><span data-stu-id="1d954-166">If the domain name starts with something else, you need to contact Workday to get the matching **Environment** value.</span></span>

1. <span data-ttu-id="1d954-167">In the **SAML Setup** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-167">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1d954-168">![SAML Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="1d954-168">![SAML Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="1d954-169">a.</span><span class="sxs-lookup"><span data-stu-id="1d954-169">a.</span></span>  <span data-ttu-id="1d954-170">Select **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="1d954-170">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="1d954-171">b.</span><span class="sxs-lookup"><span data-stu-id="1d954-171">b.</span></span>  <span data-ttu-id="1d954-172">Click **Add Row**.</span><span class="sxs-lookup"><span data-stu-id="1d954-172">Click **Add Row**.</span></span>

2. <span data-ttu-id="1d954-173">In the SAML Identity Providers section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-173">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="1d954-174">![SAML Identity Providers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="1d954-174">![SAML Identity Providers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="1d954-175">a.</span><span class="sxs-lookup"><span data-stu-id="1d954-175">a.</span></span> <span data-ttu-id="1d954-176">In the Identity Provider Name textbox, type a provider name (e.g.: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="1d954-176">In the Identity Provider Name textbox, type a provider name (e.g.: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="1d954-177">b.</span><span class="sxs-lookup"><span data-stu-id="1d954-177">b.</span></span> <span data-ttu-id="1d954-178">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="1d954-178">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="1d954-179">c.</span><span class="sxs-lookup"><span data-stu-id="1d954-179">c.</span></span> <span data-ttu-id="1d954-180">Select **Enable Workday Initialted Logout**.</span><span class="sxs-lookup"><span data-stu-id="1d954-180">Select **Enable Workday Initialted Logout**.</span></span>
   
    <span data-ttu-id="1d954-181">d.</span><span class="sxs-lookup"><span data-stu-id="1d954-181">d.</span></span> <span data-ttu-id="1d954-182">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Logout Request URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1d954-182">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="1d954-183">e.</span><span class="sxs-lookup"><span data-stu-id="1d954-183">e.</span></span> <span data-ttu-id="1d954-184">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1d954-184">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="1d954-185">![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span><span class="sxs-lookup"><span data-stu-id="1d954-185">![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="1d954-186">f.</span><span class="sxs-lookup"><span data-stu-id="1d954-186">f.</span></span> <span data-ttu-id="1d954-187">Click **Create x509 Public Key**.</span><span class="sxs-lookup"><span data-stu-id="1d954-187">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="1d954-188">![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span><span class="sxs-lookup"><span data-stu-id="1d954-188">![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


1. <span data-ttu-id="1d954-189">In the **View x509 Public Key** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-189">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="1d954-190">![View x509 Public Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span><span class="sxs-lookup"><span data-stu-id="1d954-190">![View x509 Public Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="1d954-191">a.</span><span class="sxs-lookup"><span data-stu-id="1d954-191">a.</span></span> <span data-ttu-id="1d954-192">In the **Name** textbox, type a name for your certificate (e.g.: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="1d954-192">In the **Name** textbox, type a name for your certificate (e.g.: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="1d954-193">b.</span><span class="sxs-lookup"><span data-stu-id="1d954-193">b.</span></span> <span data-ttu-id="1d954-194">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span><span class="sxs-lookup"><span data-stu-id="1d954-194">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="1d954-195">c.</span><span class="sxs-lookup"><span data-stu-id="1d954-195">c.</span></span>  <span data-ttu-id="1d954-196">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span><span class="sxs-lookup"><span data-stu-id="1d954-196">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="1d954-197">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="1d954-197">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="1d954-198">The dates are listed under the **Details** tab.</span><span class="sxs-lookup"><span data-stu-id="1d954-198">The dates are listed under the **Details** tab.</span></span>
    > 
    > 
   
    <span data-ttu-id="1d954-199">d.</span><span class="sxs-lookup"><span data-stu-id="1d954-199">d.</span></span> <span data-ttu-id="1d954-200">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="1d954-200">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
   
    > [!TIP]
    > <span data-ttu-id="1d954-201">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1d954-201">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    > 
    > 
   
    <span data-ttu-id="1d954-202">e.</span><span class="sxs-lookup"><span data-stu-id="1d954-202">e.</span></span>  <span data-ttu-id="1d954-203">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span><span class="sxs-lookup"><span data-stu-id="1d954-203">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="1d954-204">f.</span><span class="sxs-lookup"><span data-stu-id="1d954-204">f.</span></span>  <span data-ttu-id="1d954-205">In the **Certificate** textbox, paste the content of your clipboard.</span><span class="sxs-lookup"><span data-stu-id="1d954-205">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="1d954-206">g.</span><span class="sxs-lookup"><span data-stu-id="1d954-206">g.</span></span>  <span data-ttu-id="1d954-207">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d954-207">Click **OK**.</span></span>

2. <span data-ttu-id="1d954-208">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-208">Perform the following steps:</span></span> 
   
    <span data-ttu-id="1d954-209">![SSO configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC7829351111.png "SSO configuration")</span><span class="sxs-lookup"><span data-stu-id="1d954-209">![SSO configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC7829351111.png "SSO configuration")</span></span>
   
    <span data-ttu-id="1d954-210">a.</span><span class="sxs-lookup"><span data-stu-id="1d954-210">a.</span></span>  <span data-ttu-id="1d954-211">Enable the **x509 Private Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="1d954-211">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="1d954-212">b.</span><span class="sxs-lookup"><span data-stu-id="1d954-212">b.</span></span>  <span data-ttu-id="1d954-213">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="1d954-213">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="1d954-214">c.</span><span class="sxs-lookup"><span data-stu-id="1d954-214">c.</span></span>  <span data-ttu-id="1d954-215">Select **Enable SP Initiated SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="1d954-215">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="1d954-216">d.</span><span class="sxs-lookup"><span data-stu-id="1d954-216">d.</span></span>  <span data-ttu-id="1d954-217">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1d954-217">In the Azure classic portal, on the **Configure single sign-on at Workday** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="1d954-218">e.</span><span class="sxs-lookup"><span data-stu-id="1d954-218">e.</span></span> <span data-ttu-id="1d954-219">Select **Do Not Deflate SP-initiated Authentication Request**.</span><span class="sxs-lookup"><span data-stu-id="1d954-219">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="1d954-220">f.</span><span class="sxs-lookup"><span data-stu-id="1d954-220">f.</span></span> <span data-ttu-id="1d954-221">As **Authentication Request Signature Method**, select **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="1d954-221">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="1d954-222">![Authentication Request Signature Method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782932.png "Authentication Request Signature Method")</span><span class="sxs-lookup"><span data-stu-id="1d954-222">![Authentication Request Signature Method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782932.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="1d954-223">g.</span><span class="sxs-lookup"><span data-stu-id="1d954-223">g.</span></span> <span data-ttu-id="1d954-224">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d954-224">Click **OK**.</span></span> 
   
    <span data-ttu-id="1d954-225">![OK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782933.png "OK")</span><span class="sxs-lookup"><span data-stu-id="1d954-225">![OK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782933.png "OK")</span></span>

3. <span data-ttu-id="1d954-226">In the Azure classic portal, on the **Configure single sign-on at Workday** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1d954-226">In the Azure classic portal, on the **Configure single sign-on at Workday** page, click **Next**.</span></span> 
   
    <span data-ttu-id="1d954-227">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782934.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1d954-227">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782934.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="1d954-228">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1d954-228">On the **Single sign-on confirmation** page, click **Complete**.</span></span> 
   
    <span data-ttu-id="1d954-229">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782935111.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1d954-229">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782935111.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="1d954-230">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="1d954-230">Configuring user provisioning</span></span>
<span data-ttu-id="1d954-231">To get a test user provisioned into Workday, you need to contact the Workday support team.</span><span class="sxs-lookup"><span data-stu-id="1d954-231">To get a test user provisioned into Workday, you need to contact the Workday support team.</span></span>  
<span data-ttu-id="1d954-232">The Workday support team will create the user for you.</span><span class="sxs-lookup"><span data-stu-id="1d954-232">The Workday support team will create the user for you.</span></span>

## <a name="assigning-users"></a><span data-ttu-id="1d954-233">Assigning users</span><span class="sxs-lookup"><span data-stu-id="1d954-233">Assigning users</span></span>
<span data-ttu-id="1d954-234">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="1d954-234">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-workday-perform-the-following-steps"></a><span data-ttu-id="1d954-235">To assign users to Workday, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1d954-235">To assign users to Workday, perform the following steps:</span></span>
1. <span data-ttu-id="1d954-236">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="1d954-236">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="1d954-237">On the \*\*Workday \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="1d954-237">On the \*\*Workday \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="1d954-238">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782935.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="1d954-238">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC782935.png "Assign Users")</span></span>

3. <span data-ttu-id="1d954-239">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="1d954-239">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="1d954-240">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="1d954-240">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1d954-241">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1d954-241">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1d954-242">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1d954-242">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



























