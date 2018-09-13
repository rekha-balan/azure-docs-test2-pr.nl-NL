---
title: 'Tutorial: Azure Active Directory integration with TOPdesk - Public | Microsoft Docs'
description: Learn how to use TOPdesk - Public with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 60999b40e88a8aef2283cd1c632ef2207271cd29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540952"
---
# <a name="tutorial-azure-directory-integration-with-topdesk---public"></a><span data-ttu-id="7e7f0-103">Tutorial: Azure Directory integration with TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="7e7f0-103">Tutorial: Azure Directory integration with TOPdesk - Public</span></span>
<span data-ttu-id="7e7f0-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Public.</span></span>  
<span data-ttu-id="7e7f0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="7e7f0-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7e7f0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="7e7f0-107">A TOPdesk - Public single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7e7f0-107">A TOPdesk - Public single sign-on enabled subscription</span></span>

<span data-ttu-id="7e7f0-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Public will be able to single sign into the application at your TOPdesk - Public company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e7f0-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Public will be able to single sign into the application at your TOPdesk - Public company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="7e7f0-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="7e7f0-110">Enabling the application integration for TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="7e7f0-110">Enabling the application integration for TOPdesk - Public</span></span>
2. <span data-ttu-id="7e7f0-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e7f0-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="7e7f0-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="7e7f0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="7e7f0-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="7e7f0-113">Assigning users</span></span>

<span data-ttu-id="7e7f0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790613.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790613.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---public"></a><span data-ttu-id="7e7f0-115">Enabling the application integration for TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="7e7f0-115">Enabling the application integration for TOPdesk - Public</span></span>
<span data-ttu-id="7e7f0-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Public.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---public-perform-the-following-steps"></a><span data-ttu-id="7e7f0-117">To enable the application integration for TOPdesk - Public, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-117">To enable the application integration for TOPdesk - Public, perform the following steps:</span></span>
1. <span data-ttu-id="7e7f0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="7e7f0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="7e7f0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7e7f0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="7e7f0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="7e7f0-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="7e7f0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="7e7f0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="7e7f0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="7e7f0-127">In the **search box**, type **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-127">In the **search box**, type **TOPdesk - Public**.</span></span>
   
    <span data-ttu-id="7e7f0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790614.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790614.png "Application Gallery")</span></span>

7. <span data-ttu-id="7e7f0-129">In the results pane, select **TOPdesk - Public**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-129">In the results pane, select **TOPdesk - Public**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="7e7f0-130">![TOPdesk Public](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC791317.png "TOPdesk Public")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-130">![TOPdesk Public](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC791317.png "TOPdesk Public")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="7e7f0-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e7f0-131">Configuring single sign-on</span></span>
<span data-ttu-id="7e7f0-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Public with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Public with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="7e7f0-133">Configuring single sign-on for TOPdesk - Public requires you to upload a logo icon file.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-133">Configuring single sign-on for TOPdesk - Public requires you to upload a logo icon file.</span></span> <span data-ttu-id="7e7f0-134">To get the icon file, contact the TOPdesk support team.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="7e7f0-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="7e7f0-136">Sign on to your **TOPdesk - Public** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-136">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

2. <span data-ttu-id="7e7f0-137">In the **TOPdesk** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="7e7f0-138">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790598.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-138">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="7e7f0-139">Click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="7e7f0-140">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-140">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="7e7f0-141">Expand the **Login Settings** menu, and then click **General**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="7e7f0-142">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-142">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="7e7f0-143">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-143">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="7e7f0-144">![Technical Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790601.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-144">![Technical Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="7e7f0-145">a.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-145">a.</span></span> <span data-ttu-id="7e7f0-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="7e7f0-147">b.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-147">b.</span></span> <span data-ttu-id="7e7f0-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    <span data-ttu-id="7e7f0-149">![AssertionConsumerService](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-149">![AssertionConsumerService](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="7e7f0-150">c.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-150">c.</span></span> <span data-ttu-id="7e7f0-151">Copy the **AssertionConsumerService** value.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="7e7f0-152">You will need the value in the **Configure App URL** section later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="7e7f0-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="7e7f0-154">On the **TOPdesk - Public** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-154">On the **TOPdesk - Public** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="7e7f0-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790620.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790620.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="7e7f0-156">On the **How would you like users to sign on to TOPdesk - Public** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-156">On the **How would you like users to sign on to TOPdesk - Public** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="7e7f0-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790621.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790621.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="7e7f0-158">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="7e7f0-159">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790622.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-159">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790622.png "Configure App URL")</span></span>
   
    <span data-ttu-id="7e7f0-160">a.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-160">a.</span></span> <span data-ttu-id="7e7f0-161">In the **TOPdesk - Public Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Public application (e.g.: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="7e7f0-161">In the **TOPdesk - Public Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Public application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="7e7f0-162">b.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-162">b.</span></span> <span data-ttu-id="7e7f0-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Public AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Public AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="7e7f0-164">c.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-164">c.</span></span> <span data-ttu-id="7e7f0-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-165">Click **Next**.</span></span>

10. <span data-ttu-id="7e7f0-166">On the **Configure single sign-on at TOPdesk - Public** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-166">On the **Configure single sign-on at TOPdesk - Public** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="7e7f0-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790623.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790623.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="7e7f0-168">To create a certificate file, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="7e7f0-169">![Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-169">![Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790606.png "Certificate")</span></span>
    
    1. <span data-ttu-id="7e7f0-170">Open the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-170">Open the downloaded metadata file.</span></span>
    2. <span data-ttu-id="7e7f0-171">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-171">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    3. <span data-ttu-id="7e7f0-172">Copy the value of the **X509Certificate** node.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-172">Copy the value of the **X509Certificate** node.</span></span>
    4. <span data-ttu-id="7e7f0-173">Save the copied **X509Certificate** value locally on your computer in a file.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-173">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>
12. <span data-ttu-id="7e7f0-174">On your TOPdesk - Public company site, in the **TOPdesk** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-174">On your TOPdesk - Public company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="7e7f0-175">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790598.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-175">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790598.png "Settings")</span></span>
13. <span data-ttu-id="7e7f0-176">Click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-176">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="7e7f0-177">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-177">![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790599.png "Login Settings")</span></span>
14. <span data-ttu-id="7e7f0-178">Expand the **Login Settings** menu, and then click **General**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-178">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="7e7f0-179">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-179">![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790600.png "General")</span></span>
15. <span data-ttu-id="7e7f0-180">In the **Public** section, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-180">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="7e7f0-181">![SAML Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790625.png "SAML Login")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-181">![SAML Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790625.png "SAML Login")</span></span>
16. <span data-ttu-id="7e7f0-182">On the **SAML configuration assistant** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-182">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="7e7f0-183">![SAML Configuration Assistant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-183">![SAML Configuration Assistant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="7e7f0-184">a.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-184">a.</span></span> <span data-ttu-id="7e7f0-185">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-185">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="7e7f0-186">b.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-186">b.</span></span> <span data-ttu-id="7e7f0-187">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-187">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="7e7f0-188">c.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-188">c.</span></span> <span data-ttu-id="7e7f0-189">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-189">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="7e7f0-190">d.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-190">d.</span></span> <span data-ttu-id="7e7f0-191">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-191">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="7e7f0-192">e.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-192">e.</span></span> <span data-ttu-id="7e7f0-193">In the **Display name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-193">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="7e7f0-194">f.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-194">f.</span></span> <span data-ttu-id="7e7f0-195">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-195">Click **Save**.</span></span>

17. <span data-ttu-id="7e7f0-196">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-196">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="7e7f0-197">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790627.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-197">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790627.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="7e7f0-198">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="7e7f0-198">Configuring user provisioning</span></span>
<span data-ttu-id="7e7f0-199">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-199">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="7e7f0-200">In the case of TOPdesk - Public, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-200">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="7e7f0-201">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-201">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="7e7f0-202">Sign on to your **TOPdesk - Public** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-202">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="7e7f0-203">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-203">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="7e7f0-204">![Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790628.png "Person")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-204">![Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790628.png "Person")</span></span>

3. <span data-ttu-id="7e7f0-205">On the New Person dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-205">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="7e7f0-206">![New Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790629.png "New Person")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-206">![New Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790629.png "New Person")</span></span>
   
    <span data-ttu-id="7e7f0-207">a.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-207">a.</span></span> <span data-ttu-id="7e7f0-208">Click the General tab.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-208">Click the General tab.</span></span>

    <span data-ttu-id="7e7f0-209">b.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-209">b.</span></span> <span data-ttu-id="7e7f0-210">In the Surname textbox, type the last name of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-210">In the Surname textbox, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
 
    <span data-ttu-id="7e7f0-211">c.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-211">c.</span></span> <span data-ttu-id="7e7f0-212">Select a **Site** for the account.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-212">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="7e7f0-213">d.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-213">d.</span></span> <span data-ttu-id="7e7f0-214">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-214">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="7e7f0-215">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-215">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="7e7f0-216">Assigning users</span><span class="sxs-lookup"><span data-stu-id="7e7f0-216">Assigning users</span></span>
<span data-ttu-id="7e7f0-217">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-217">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---public-perform-the-following-steps"></a><span data-ttu-id="7e7f0-218">To assign users to TOPdesk - Public, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e7f0-218">To assign users to TOPdesk - Public, perform the following steps:</span></span>
1. <span data-ttu-id="7e7f0-219">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-219">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="7e7f0-220">On the \*\*TOPdesk - Public \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-220">On the \*\*TOPdesk - Public \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="7e7f0-221">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790630.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-221">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC790630.png "Assign Users")</span></span>

3. <span data-ttu-id="7e7f0-222">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-222">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="7e7f0-223">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="7e7f0-223">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-public-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="7e7f0-224">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7e7f0-224">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7e7f0-225">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e7f0-225">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




























