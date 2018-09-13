---
title: 'Tutorial: Azure Active Directory integration with Work.com | Microsoft Docs'
description: Learn how to use Work.com with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 6a1be66c7dd3b6f807c0219e0bb0b5cdbc5a7b95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554981"
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="19fe4-103">Tutorial: Azure Active Directory integration with Work.com</span><span class="sxs-lookup"><span data-stu-id="19fe4-103">Tutorial: Azure Active Directory integration with Work.com</span></span>
<span data-ttu-id="19fe4-104">The objective of this tutorial is to show the integration of Azure and Work.com.</span><span class="sxs-lookup"><span data-stu-id="19fe4-104">The objective of this tutorial is to show the integration of Azure and Work.com.</span></span>  
<span data-ttu-id="19fe4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="19fe4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="19fe4-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="19fe4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="19fe4-107">A Work.com single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="19fe4-107">A Work.com single sign-on enabled subscription</span></span>

<span data-ttu-id="19fe4-108">After completing this tutorial, the AAD users to whom you have assign Work.com access will be able to single sign into the application at your Work.com company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19fe4-108">After completing this tutorial, the AAD users to whom you have assign Work.com access will be able to single sign into the application at your Work.com company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="19fe4-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19fe4-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="19fe4-110">Enabling the application integration for Work.com</span><span class="sxs-lookup"><span data-stu-id="19fe4-110">Enabling the application integration for Work.com</span></span>
2. <span data-ttu-id="19fe4-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="19fe4-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="19fe4-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="19fe4-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="19fe4-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="19fe4-113">Assigning users</span></span>

<span data-ttu-id="19fe4-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794105.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="19fe4-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794105.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-workcom"></a><span data-ttu-id="19fe4-115">Enabling the application integration for Work.com</span><span class="sxs-lookup"><span data-stu-id="19fe4-115">Enabling the application integration for Work.com</span></span>
<span data-ttu-id="19fe4-116">The objective of this section is to outline how to enable the application integration for Work.com.</span><span class="sxs-lookup"><span data-stu-id="19fe4-116">The objective of this section is to outline how to enable the application integration for Work.com.</span></span>

### <a name="to-enable-the-application-integration-for-workcom-perform-the-following-steps"></a><span data-ttu-id="19fe4-117">To enable the application integration for Work.com, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-117">To enable the application integration for Work.com, perform the following steps:</span></span>
1. <span data-ttu-id="19fe4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="19fe4-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="19fe4-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="19fe4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19fe4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="19fe4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19fe4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="19fe4-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="19fe4-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="19fe4-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19fe4-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="19fe4-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="19fe4-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="19fe4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="19fe4-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="19fe4-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="19fe4-127">In the **search box**, type **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-127">In the **search box**, type **Work.com**.</span></span>
   
    <span data-ttu-id="19fe4-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794106.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="19fe4-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794106.png "Application Gallery")</span></span>

7. <span data-ttu-id="19fe4-129">In the results pane, select **Work.com**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="19fe4-129">In the results pane, select **Work.com**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="19fe4-130">![Work.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794107.png "Work.com")</span><span class="sxs-lookup"><span data-stu-id="19fe4-130">![Work.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794107.png "Work.com")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="19fe4-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="19fe4-131">Configuring single sign-on</span></span>
<span data-ttu-id="19fe4-132">The objective of this section is to outline how to enable users to authenticate to Work.com with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="19fe4-132">The objective of this section is to outline how to enable users to authenticate to Work.com with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="19fe4-133">As part of this procedure, you are required to upload a certificate to Work.com.com.</span><span class="sxs-lookup"><span data-stu-id="19fe4-133">As part of this procedure, you are required to upload a certificate to Work.com.com.</span></span>

> [!NOTE]
> <span data-ttu-id="19fe4-134">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span><span class="sxs-lookup"><span data-stu-id="19fe4-134">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="19fe4-135">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span><span class="sxs-lookup"><span data-stu-id="19fe4-135">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>
> 
> 

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="19fe4-136">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-136">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="19fe4-137">Log in to your Work.com tenant as administrator.</span><span class="sxs-lookup"><span data-stu-id="19fe4-137">Log in to your Work.com tenant as administrator.</span></span>
2. <span data-ttu-id="19fe4-138">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-138">Go to **Setup**.</span></span>
   
    <span data-ttu-id="19fe4-139">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="19fe4-139">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>

3. <span data-ttu-id="19fe4-140">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="19fe4-140">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="19fe4-141">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="19fe4-141">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767825.png "My Domain")</span></span>

4. <span data-ttu-id="19fe4-142">To verify that your domain has been setup correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span><span class="sxs-lookup"><span data-stu-id="19fe4-142">To verify that your domain has been setup correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="19fe4-143">![Doman Deployed to User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784377.png "Doman Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="19fe4-143">![Doman Deployed to User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784377.png "Doman Deployed to User")</span></span>

5. <span data-ttu-id="19fe4-144">In a different web browser window, log in to your Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="19fe4-144">In a different web browser window, log in to your Azure classic portal.</span></span>

6. <span data-ttu-id="19fe4-145">On the \*\*Work.com \*\*application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="19fe4-145">On the \*\*Work.com \*\*application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="19fe4-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794109.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19fe4-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794109.png "Configure Single Sign-On")</span></span>

7. <span data-ttu-id="19fe4-147">On the **How would you like users to sign on to Work.com** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-147">On the **How would you like users to sign on to Work.com** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="19fe4-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794110.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19fe4-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794110.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="19fe4-149">On the **Configure App URL** page, in the **Work.com Sign On URL** textbox, type the URL used by your users to sign on to your Work.com application (e.g.:” *http://company.my.salesforce.com*”), and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="19fe4-149">On the **Configure App URL** page, in the **Work.com Sign On URL** textbox, type the URL used by your users to sign on to your Work.com application (e.g.:” *http://company.my.salesforce.com*”), and then click **Next**:</span></span> 
   
    <span data-ttu-id="19fe4-150">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794111.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="19fe4-150">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794111.png "Configure App URL")</span></span>

9. <span data-ttu-id="19fe4-151">On the **Configure single sign-on at Work.com** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="19fe4-151">On the **Configure single sign-on at Work.com** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="19fe4-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794112.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19fe4-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794112.png "Configure Single Sign-On")</span></span>

10. <span data-ttu-id="19fe4-153">Log in to your Work.com tenant.</span><span class="sxs-lookup"><span data-stu-id="19fe4-153">Log in to your Work.com tenant.</span></span>

11. <span data-ttu-id="19fe4-154">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-154">Go to **Setup**.</span></span>
    
    <span data-ttu-id="19fe4-155">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="19fe4-155">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>

12. <span data-ttu-id="19fe4-156">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-156">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="19fe4-157">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794113.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="19fe4-157">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794113.png "Single Sign-On Settings")</span></span>

13. <span data-ttu-id="19fe4-158">On the **Single Sign-On Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-158">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="19fe4-159">![SAML Enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC781026.png "SAML Enabled")</span><span class="sxs-lookup"><span data-stu-id="19fe4-159">![SAML Enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="19fe4-160">a.</span><span class="sxs-lookup"><span data-stu-id="19fe4-160">a.</span></span> <span data-ttu-id="19fe4-161">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-161">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="19fe4-162">b.</span><span class="sxs-lookup"><span data-stu-id="19fe4-162">b.</span></span> <span data-ttu-id="19fe4-163">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-163">Click **New**.</span></span>

14. <span data-ttu-id="19fe4-164">In the **SAML Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-164">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="19fe4-165">![SAML Single Sign-On Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794114.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="19fe4-165">![SAML Single Sign-On Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="19fe4-166">a.</span><span class="sxs-lookup"><span data-stu-id="19fe4-166">a.</span></span> <span data-ttu-id="19fe4-167">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="19fe4-167">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="19fe4-168">Providing a value for **Name** does automatically populate the **API Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="19fe4-168">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    > 
    > 
    
    <span data-ttu-id="19fe4-169">b.</span><span class="sxs-lookup"><span data-stu-id="19fe4-169">b.</span></span> <span data-ttu-id="19fe4-170">In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="19fe4-170">In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="19fe4-171">c.</span><span class="sxs-lookup"><span data-stu-id="19fe4-171">c.</span></span> <span data-ttu-id="19fe4-172">To upload the downloaded certificate, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-172">To upload the downloaded certificate, click **Browse**.</span></span>
    
    <span data-ttu-id="19fe4-173">d.</span><span class="sxs-lookup"><span data-stu-id="19fe4-173">d.</span></span> <span data-ttu-id="19fe4-174">In the **Entity Id** textbox, type **https://salesforce-work.com**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-174">In the **Entity Id** textbox, type **https://salesforce-work.com**.</span></span>
    
    <span data-ttu-id="19fe4-175">e.</span><span class="sxs-lookup"><span data-stu-id="19fe4-175">e.</span></span> <span data-ttu-id="19fe4-176">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-176">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="19fe4-177">f.</span><span class="sxs-lookup"><span data-stu-id="19fe4-177">f.</span></span> <span data-ttu-id="19fe4-178">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-178">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="19fe4-179">g.</span><span class="sxs-lookup"><span data-stu-id="19fe4-179">g.</span></span> <span data-ttu-id="19fe4-180">In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="19fe4-180">In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="19fe4-181">h.</span><span class="sxs-lookup"><span data-stu-id="19fe4-181">h.</span></span> <span data-ttu-id="19fe4-182">In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="19fe4-182">In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span></span>
    
    <span data-ttu-id="19fe4-183">i.</span><span class="sxs-lookup"><span data-stu-id="19fe4-183">i.</span></span> <span data-ttu-id="19fe4-184">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-184">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="19fe4-185">j.</span><span class="sxs-lookup"><span data-stu-id="19fe4-185">j.</span></span> <span data-ttu-id="19fe4-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-186">Click **Save**.</span></span>

15. <span data-ttu-id="19fe4-187">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="19fe4-187">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="19fe4-188">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794115.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="19fe4-188">![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794115.png "My Domain")</span></span>

16. <span data-ttu-id="19fe4-189">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-189">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="19fe4-190">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="19fe4-190">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767826.png "Login Page Branding")</span></span>

17. <span data-ttu-id="19fe4-191">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span><span class="sxs-lookup"><span data-stu-id="19fe4-191">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="19fe4-192">Select it, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-192">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="19fe4-193">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="19fe4-193">![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784366.png "Login Page Branding")</span></span>

18. <span data-ttu-id="19fe4-194">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="19fe4-194">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="19fe4-195">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794116.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19fe4-195">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794116.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="19fe4-196">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="19fe4-196">Configuring user provisioning</span></span>
<span data-ttu-id="19fe4-197">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span><span class="sxs-lookup"><span data-stu-id="19fe4-197">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span>  
<span data-ttu-id="19fe4-198">In the case of Work.com, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="19fe4-198">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="19fe4-199">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-199">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="19fe4-200">Sign on to your Work.com company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="19fe4-200">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="19fe4-201">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-201">Go to **Setup**.</span></span>
   
    <span data-ttu-id="19fe4-202">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="19fe4-202">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="19fe4-203">Go to **Manage Users \> Users**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-203">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="19fe4-204">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="19fe4-204">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="19fe4-205">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-205">Click **New User**.</span></span>
   
    <span data-ttu-id="19fe4-206">![All Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span><span class="sxs-lookup"><span data-stu-id="19fe4-206">![All Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="19fe4-207">In the User Edit section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-207">In the User Edit section, perform the following steps:</span></span>
   
    <span data-ttu-id="19fe4-208">![User Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794118.png "User Edit")</span><span class="sxs-lookup"><span data-stu-id="19fe4-208">![User Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794118.png "User Edit")</span></span>
   
    <span data-ttu-id="19fe4-209">a.</span><span class="sxs-lookup"><span data-stu-id="19fe4-209">a.</span></span> <span data-ttu-id="19fe4-210">Type the **Last Name**, **Alias**, **Email**, **Username** and **Nickname** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="19fe4-210">Type the **Last Name**, **Alias**, **Email**, **Username** and **Nickname** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="19fe4-211">b.</span><span class="sxs-lookup"><span data-stu-id="19fe4-211">b.</span></span> <span data-ttu-id="19fe4-212">Select **Role**, **User License** and **Profile**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-212">Select **Role**, **User License** and **Profile**.</span></span>
   
    <span data-ttu-id="19fe4-213">c.</span><span class="sxs-lookup"><span data-stu-id="19fe4-213">c.</span></span> <span data-ttu-id="19fe4-214">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-214">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="19fe4-215">The Azure Active Directory account holder will get an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="19fe4-215">The Azure Active Directory account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

## <a name="assigning-users"></a><span data-ttu-id="19fe4-216">Assigning users</span><span class="sxs-lookup"><span data-stu-id="19fe4-216">Assigning users</span></span>
<span data-ttu-id="19fe4-217">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="19fe4-217">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-workcom-perform-the-following-steps"></a><span data-ttu-id="19fe4-218">To assign users to Work.com, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19fe4-218">To assign users to Work.com, perform the following steps:</span></span>
1. <span data-ttu-id="19fe4-219">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="19fe4-219">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="19fe4-220">On the Work.com application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="19fe4-220">On the Work.com application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="19fe4-221">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794119.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="19fe4-221">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794119.png "Assign Users")</span></span>

3. <span data-ttu-id="19fe4-222">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="19fe4-222">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="19fe4-223">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="19fe4-223">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="19fe4-224">You should now wait for 10 minutes and verify that the account has been synchronized to Work.com.com.</span><span class="sxs-lookup"><span data-stu-id="19fe4-224">You should now wait for 10 minutes and verify that the account has been synchronized to Work.com.com.</span></span>

<span data-ttu-id="19fe4-225">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="19fe4-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="19fe4-226">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19fe4-226">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





























