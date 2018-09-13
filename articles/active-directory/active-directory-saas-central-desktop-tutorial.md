---
title: 'Tutorial: Azure Active Directory integration with Central Desktop | Microsoft Docs'
description: Learn how to use Central Desktop with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9627d2337594eb7c7a67bee08b5860c2dbcee45e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549407"
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="11a12-103">Tutorial: Azure Active Directory integration with Central Desktop</span><span class="sxs-lookup"><span data-stu-id="11a12-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="11a12-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="11a12-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="11a12-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="11a12-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="11a12-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="11a12-106">A valid Azure subscription</span></span>
* <span data-ttu-id="11a12-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span><span class="sxs-lookup"><span data-stu-id="11a12-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="11a12-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="11a12-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="11a12-109">Enabling the application integration for Central Desktop</span><span class="sxs-lookup"><span data-stu-id="11a12-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="11a12-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="11a12-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="11a12-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="11a12-111">Configuring user provisioning</span></span>
* <span data-ttu-id="11a12-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="11a12-112">Assigning users</span></span>

<span data-ttu-id="11a12-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="11a12-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="11a12-114">Enable the application integration for Central Desktop</span><span class="sxs-lookup"><span data-stu-id="11a12-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="11a12-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="11a12-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="11a12-116">**To enable the application integration for Central Desktop, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11a12-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="11a12-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11a12-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="11a12-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="11a12-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="11a12-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="11a12-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="11a12-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="11a12-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="11a12-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="11a12-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="11a12-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="11a12-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="11a12-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="11a12-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="11a12-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="11a12-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="11a12-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="11a12-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="11a12-126">In the **search box**, type **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="11a12-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="11a12-127">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="11a12-127">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="11a12-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="11a12-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="11a12-129">![Central Desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="11a12-129">![Central Desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="11a12-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="11a12-130">Configure single sign-on</span></span>

<span data-ttu-id="11a12-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="11a12-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="11a12-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span><span class="sxs-lookup"><span data-stu-id="11a12-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="11a12-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="11a12-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="11a12-134">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11a12-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="11a12-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="11a12-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="11a12-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="11a12-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="11a12-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11a12-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="11a12-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="11a12-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="11a12-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="11a12-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="11a12-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="11a12-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="11a12-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="11a12-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="11a12-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="11a12-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="11a12-143">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="11a12-143">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="11a12-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="11a12-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="11a12-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="11a12-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="11a12-146">Log in to your **Central Desktop** tenant.</span><span class="sxs-lookup"><span data-stu-id="11a12-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="11a12-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="11a12-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="11a12-148">![Setup - Advanced](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span><span class="sxs-lookup"><span data-stu-id="11a12-148">![Setup - Advanced](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="11a12-149">On the **Single Sign On Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11a12-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="11a12-150">![Single Sign On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="11a12-150">![Single Sign On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="11a12-151">Select **Enable SAML v2 Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="11a12-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="11a12-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="11a12-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="11a12-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="11a12-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="11a12-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="11a12-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="11a12-155">In the **Message Signature Verification Method** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11a12-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="11a12-156">![Message Signature Verification Method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span><span class="sxs-lookup"><span data-stu-id="11a12-156">![Message Signature Verification Method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="11a12-157">Select **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="11a12-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="11a12-158">From the **SSO Certificate** list, select **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="11a12-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="11a12-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span><span class="sxs-lookup"><span data-stu-id="11a12-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="11a12-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="11a12-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="11a12-161">Select **Display a link to your SAMLv2 login page**.</span><span class="sxs-lookup"><span data-stu-id="11a12-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="11a12-162">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="11a12-162">Click **Update**.</span></span>
10. <span data-ttu-id="11a12-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="11a12-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="11a12-164">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="11a12-164">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="11a12-165">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="11a12-165">Configure user provisioning</span></span>

<span data-ttu-id="11a12-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span><span class="sxs-lookup"><span data-stu-id="11a12-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="11a12-167">This section describes how to create AAD user accounts in Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="11a12-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="11a12-168">**To provision user accounts to Central Desktop:**</span><span class="sxs-lookup"><span data-stu-id="11a12-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="11a12-169">Log in to your Central Desktop tenant.</span><span class="sxs-lookup"><span data-stu-id="11a12-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="11a12-170">Go to **People \> Internal Members**.</span><span class="sxs-lookup"><span data-stu-id="11a12-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="11a12-171">Click **Add Internal Members**.</span><span class="sxs-lookup"><span data-stu-id="11a12-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="11a12-172">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span><span class="sxs-lookup"><span data-stu-id="11a12-172">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="11a12-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11a12-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="11a12-174">![Email Addresses of New Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span><span class="sxs-lookup"><span data-stu-id="11a12-174">![Email Addresses of New Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="11a12-175">Click **Add Internal member(s)**.</span><span class="sxs-lookup"><span data-stu-id="11a12-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="11a12-176">![Add Internal Member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span><span class="sxs-lookup"><span data-stu-id="11a12-176">![Add Internal Member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="11a12-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span><span class="sxs-lookup"><span data-stu-id="11a12-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="11a12-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span><span class="sxs-lookup"><span data-stu-id="11a12-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="11a12-179">Assign users</span><span class="sxs-lookup"><span data-stu-id="11a12-179">Assign users</span></span>
<span data-ttu-id="11a12-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="11a12-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="11a12-181">**To assign users to Central Desktop, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11a12-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="11a12-182">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="11a12-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="11a12-183">On the **Central Desktop** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="11a12-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="11a12-184">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="11a12-184">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="11a12-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="11a12-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="11a12-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="11a12-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="11a12-187">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="11a12-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="11a12-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11a12-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















