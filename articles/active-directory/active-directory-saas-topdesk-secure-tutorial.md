---
title: 'Tutorial: Azure Active Directory integration with TOPdesk - Secure | Microsoft Docs'
description: Learn how to use TOPdesk - Secure with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 51ba2d2e7c2e4d31b27628477c501745be8a50f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548730"
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="afc78-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="afc78-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="afc78-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="afc78-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="afc78-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="afc78-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="afc78-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="afc78-106">A valid Azure subscription</span></span>
* <span data-ttu-id="afc78-107">A TOPdesk - Secure single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="afc78-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="afc78-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="afc78-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="afc78-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="afc78-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="afc78-110">Enabling the application integration for TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="afc78-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="afc78-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="afc78-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="afc78-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="afc78-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="afc78-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="afc78-113">Assigning users</span></span>

<span data-ttu-id="afc78-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="afc78-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="afc78-115">Enabling the application integration for TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="afc78-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="afc78-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="afc78-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="afc78-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="afc78-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afc78-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="afc78-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="afc78-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="afc78-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="afc78-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="afc78-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="afc78-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="afc78-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="afc78-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="afc78-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="afc78-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="afc78-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="afc78-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="afc78-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="afc78-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="afc78-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="afc78-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="afc78-127">In the **search box**, type **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="afc78-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="afc78-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="afc78-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="afc78-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="afc78-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="afc78-130">![TOPdesk - Secure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="afc78-130">![TOPdesk - Secure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="afc78-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="afc78-131">Configuring single sign-on</span></span>
<span data-ttu-id="afc78-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="afc78-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="afc78-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span><span class="sxs-lookup"><span data-stu-id="afc78-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="afc78-134">To get the icon file, contact the TOPdesk support team.</span><span class="sxs-lookup"><span data-stu-id="afc78-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="afc78-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="afc78-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="afc78-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="afc78-137">In the **TOPdesk** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="afc78-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="afc78-138">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="afc78-138">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="afc78-139">Click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="afc78-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="afc78-140">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="afc78-140">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="afc78-141">Expand the **Login Settings** menu, and then click **General**.</span><span class="sxs-lookup"><span data-stu-id="afc78-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="afc78-142">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="afc78-142">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="afc78-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="afc78-144">![Technical Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="afc78-144">![Technical Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="afc78-145">a.</span><span class="sxs-lookup"><span data-stu-id="afc78-145">a.</span></span> <span data-ttu-id="afc78-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="afc78-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="afc78-147">b.</span><span class="sxs-lookup"><span data-stu-id="afc78-147">b.</span></span> <span data-ttu-id="afc78-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span><span class="sxs-lookup"><span data-stu-id="afc78-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="afc78-149">![Assertion Consumer Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="afc78-149">![Assertion Consumer Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="afc78-150">c.</span><span class="sxs-lookup"><span data-stu-id="afc78-150">c.</span></span> <span data-ttu-id="afc78-151">Copy the **AssertionConsumerService** value.</span><span class="sxs-lookup"><span data-stu-id="afc78-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="afc78-152">You will need the value in the **Configure App URL** section later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc78-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="afc78-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="afc78-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="afc78-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="afc78-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="afc78-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="afc78-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="afc78-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="afc78-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="afc78-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="afc78-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="afc78-158">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="afc78-159">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="afc78-159">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="afc78-160">a.</span><span class="sxs-lookup"><span data-stu-id="afc78-160">a.</span></span> <span data-ttu-id="afc78-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="afc78-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="afc78-162">b.</span><span class="sxs-lookup"><span data-stu-id="afc78-162">b.</span></span> <span data-ttu-id="afc78-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="afc78-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="afc78-164">c.</span><span class="sxs-lookup"><span data-stu-id="afc78-164">c.</span></span> <span data-ttu-id="afc78-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="afc78-165">Click **Next**.</span></span>

10. <span data-ttu-id="afc78-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="afc78-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="afc78-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="afc78-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="afc78-168">To create a certificate file, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="afc78-169">![Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="afc78-169">![Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="afc78-170">a.</span><span class="sxs-lookup"><span data-stu-id="afc78-170">a.</span></span> <span data-ttu-id="afc78-171">Open the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="afc78-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="afc78-172">b.</span><span class="sxs-lookup"><span data-stu-id="afc78-172">b.</span></span> <span data-ttu-id="afc78-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="afc78-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="afc78-174">c.</span><span class="sxs-lookup"><span data-stu-id="afc78-174">c.</span></span> <span data-ttu-id="afc78-175">Copy the value of the **X509Certificate** node.</span><span class="sxs-lookup"><span data-stu-id="afc78-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="afc78-176">d.</span><span class="sxs-lookup"><span data-stu-id="afc78-176">d.</span></span> <span data-ttu-id="afc78-177">Save the copied **X509Certificate** value locally on your computer in a file.</span><span class="sxs-lookup"><span data-stu-id="afc78-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="afc78-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="afc78-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="afc78-179">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="afc78-179">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="afc78-180">Click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="afc78-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="afc78-181">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="afc78-181">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="afc78-182">Expand the **Login Settings** menu, and then click **General**.</span><span class="sxs-lookup"><span data-stu-id="afc78-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="afc78-183">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="afc78-183">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="afc78-184">In the **Public** section, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="afc78-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="afc78-185">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span><span class="sxs-lookup"><span data-stu-id="afc78-185">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="afc78-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="afc78-187">![SAML Configuration Assistant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="afc78-187">![SAML Configuration Assistant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="afc78-188">a.</span><span class="sxs-lookup"><span data-stu-id="afc78-188">a.</span></span> <span data-ttu-id="afc78-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="afc78-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="afc78-190">b.</span><span class="sxs-lookup"><span data-stu-id="afc78-190">b.</span></span> <span data-ttu-id="afc78-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="afc78-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="afc78-192">c.</span><span class="sxs-lookup"><span data-stu-id="afc78-192">c.</span></span> <span data-ttu-id="afc78-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="afc78-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="afc78-194">d.</span><span class="sxs-lookup"><span data-stu-id="afc78-194">d.</span></span> <span data-ttu-id="afc78-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="afc78-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="afc78-196">e.</span><span class="sxs-lookup"><span data-stu-id="afc78-196">e.</span></span> <span data-ttu-id="afc78-197">In the **Display name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="afc78-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="afc78-198">f.</span><span class="sxs-lookup"><span data-stu-id="afc78-198">f.</span></span> <span data-ttu-id="afc78-199">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="afc78-199">Click **Save**.</span></span>

17. <span data-ttu-id="afc78-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="afc78-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="afc78-201">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="afc78-201">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="afc78-202">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="afc78-202">Configuring user provisioning</span></span>
<span data-ttu-id="afc78-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="afc78-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="afc78-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="afc78-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="afc78-205">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="afc78-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="afc78-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="afc78-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="afc78-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="afc78-208">![Operator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span><span class="sxs-lookup"><span data-stu-id="afc78-208">![Operator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="afc78-209">On the **New Operator** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="afc78-210">![New Operator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span><span class="sxs-lookup"><span data-stu-id="afc78-210">![New Operator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="afc78-211">a.</span><span class="sxs-lookup"><span data-stu-id="afc78-211">a.</span></span> <span data-ttu-id="afc78-212">Click the General tab.</span><span class="sxs-lookup"><span data-stu-id="afc78-212">Click the General tab.</span></span>
   
    <span data-ttu-id="afc78-213">b.</span><span class="sxs-lookup"><span data-stu-id="afc78-213">b.</span></span> <span data-ttu-id="afc78-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="afc78-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="afc78-215">c.</span><span class="sxs-lookup"><span data-stu-id="afc78-215">c.</span></span> <span data-ttu-id="afc78-216">Select a **Site** for the account in the **Location** section.</span><span class="sxs-lookup"><span data-stu-id="afc78-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="afc78-217">d.</span><span class="sxs-lookup"><span data-stu-id="afc78-217">d.</span></span> <span data-ttu-id="afc78-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span><span class="sxs-lookup"><span data-stu-id="afc78-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="afc78-219">e.</span><span class="sxs-lookup"><span data-stu-id="afc78-219">e.</span></span> <span data-ttu-id="afc78-220">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="afc78-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="afc78-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="afc78-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="afc78-222">Assigning users</span><span class="sxs-lookup"><span data-stu-id="afc78-222">Assigning users</span></span>
<span data-ttu-id="afc78-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="afc78-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="afc78-224">To assign users to TOPdesk - Secure, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="afc78-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="afc78-225">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="afc78-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="afc78-226">On the \*\*TOPdesk - Secure \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="afc78-226">On the \*\*TOPdesk - Secure \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="afc78-227">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="afc78-227">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="afc78-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="afc78-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="afc78-229">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="afc78-229">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="afc78-230">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="afc78-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="afc78-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="afc78-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




























