---
title: 'Tutorial: Azure Active Directory integration with Veracode | Microsoft Docs'
description: Learn how to use Veracode with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: b6e29876b1a0a091b009d557903a998766084e75
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552705"
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="00d91-103">Tutorial: Azure Active Directory integration with Veracode</span><span class="sxs-lookup"><span data-stu-id="00d91-103">Tutorial: Azure Active Directory integration with Veracode</span></span>
<span data-ttu-id="00d91-104">The objective of this tutorial is to show the integration of Azure and Veracode.</span><span class="sxs-lookup"><span data-stu-id="00d91-104">The objective of this tutorial is to show the integration of Azure and Veracode.</span></span> <span data-ttu-id="00d91-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="00d91-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="00d91-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="00d91-106">A valid Azure subscription</span></span>
* <span data-ttu-id="00d91-107">A Veracode single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="00d91-107">A Veracode single sign-on enabled subscription</span></span>

<span data-ttu-id="00d91-108">After completing this tutorial, the Azure AD users you have assigned to Veracode will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00d91-108">After completing this tutorial, the Azure AD users you have assigned to Veracode will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="00d91-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="00d91-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="00d91-110">Enabling the application integration for Veracode</span><span class="sxs-lookup"><span data-stu-id="00d91-110">Enabling the application integration for Veracode</span></span>
2. <span data-ttu-id="00d91-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="00d91-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="00d91-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="00d91-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="00d91-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="00d91-113">Assigning users</span></span>

<span data-ttu-id="00d91-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802903.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="00d91-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802903.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-veracode"></a><span data-ttu-id="00d91-115">Enabling the application integration for Veracode</span><span class="sxs-lookup"><span data-stu-id="00d91-115">Enabling the application integration for Veracode</span></span>
<span data-ttu-id="00d91-116">The objective of this section is to outline how to enable the application integration for Veracode.</span><span class="sxs-lookup"><span data-stu-id="00d91-116">The objective of this section is to outline how to enable the application integration for Veracode.</span></span>

### <a name="to-enable-the-application-integration-for-veracode-perform-the-following-steps"></a><span data-ttu-id="00d91-117">To enable the application integration for Veracode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="00d91-117">To enable the application integration for Veracode, perform the following steps:</span></span>
1. <span data-ttu-id="00d91-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00d91-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="00d91-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="00d91-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="00d91-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="00d91-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="00d91-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="00d91-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="00d91-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="00d91-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="00d91-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="00d91-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="00d91-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="00d91-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="00d91-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="00d91-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="00d91-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="00d91-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="00d91-127">In the **search box**, type **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="00d91-127">In the **search box**, type **Veracode**.</span></span>
   
    <span data-ttu-id="00d91-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802904.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="00d91-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802904.png "Application Gallery")</span></span>

7. <span data-ttu-id="00d91-129">In the results pane, select **Veracode**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="00d91-129">In the results pane, select **Veracode**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="00d91-130">![Veracode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802905.png "Veracode")</span><span class="sxs-lookup"><span data-stu-id="00d91-130">![Veracode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802905.png "Veracode")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="00d91-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="00d91-131">Configuring single sign-on</span></span>
<span data-ttu-id="00d91-132">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="00d91-132">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="00d91-133">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="00d91-133">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>  
<span data-ttu-id="00d91-134">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="00d91-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="00d91-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802906.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="00d91-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802906.png "Attributes")</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="00d91-136">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="00d91-136">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="00d91-137">In the Azure classic portal, on the **Veracode** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="00d91-137">In the Azure classic portal, on the **Veracode** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="00d91-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802907.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="00d91-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802907.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="00d91-139">On the **How would you like users to sign on to Veracode** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="00d91-139">On the **How would you like users to sign on to Veracode** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="00d91-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802908.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="00d91-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802908.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="00d91-141">On the **Configure App Settings** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="00d91-141">On the **Configure App Settings** page, click **Next**.</span></span>
   
    <span data-ttu-id="00d91-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802909.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="00d91-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802909.png "Configure App Settings")</span></span>

4. <span data-ttu-id="00d91-143">On the **Configure single sign-on at Veracode** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="00d91-143">On the **Configure single sign-on at Veracode** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="00d91-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802910.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="00d91-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802910.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="00d91-145">In a different web browser window, log into your Veracode company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="00d91-145">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

6. <span data-ttu-id="00d91-146">In the menu on the top, click **Settings**, and then click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="00d91-146">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="00d91-147">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802911.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="00d91-147">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802911.png "Administration")</span></span>

7. <span data-ttu-id="00d91-148">Click the **SAML** tab.</span><span class="sxs-lookup"><span data-stu-id="00d91-148">Click the **SAML** tab.</span></span>

8. <span data-ttu-id="00d91-149">In the **Organization SAML Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="00d91-149">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="00d91-150">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802912.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="00d91-150">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802912.png "Administration")</span></span>
   
    <span data-ttu-id="00d91-151">a.</span><span class="sxs-lookup"><span data-stu-id="00d91-151">a.</span></span> <span data-ttu-id="00d91-152">In the Azure classic portal, on the **Configure single sign-on at Veracode** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox</span><span class="sxs-lookup"><span data-stu-id="00d91-152">In the Azure classic portal, on the **Configure single sign-on at Veracode** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox</span></span>
   
    <span data-ttu-id="00d91-153">b.</span><span class="sxs-lookup"><span data-stu-id="00d91-153">b.</span></span> <span data-ttu-id="00d91-154">To upload your downloaded certificate, click **Choose File**.</span><span class="sxs-lookup"><span data-stu-id="00d91-154">To upload your downloaded certificate, click **Choose File**.</span></span>
   
    <span data-ttu-id="00d91-155">c.</span><span class="sxs-lookup"><span data-stu-id="00d91-155">c.</span></span> <span data-ttu-id="00d91-156">Select **Enable Self Registration**.</span><span class="sxs-lookup"><span data-stu-id="00d91-156">Select **Enable Self Registration**.</span></span>

9. <span data-ttu-id="00d91-157">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="00d91-157">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="00d91-158">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802913.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="00d91-158">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802913.png "Administration")</span></span>
   
    <span data-ttu-id="00d91-159">a.</span><span class="sxs-lookup"><span data-stu-id="00d91-159">a.</span></span> <span data-ttu-id="00d91-160">As **New User Activation**, select **No Activation Required**.</span><span class="sxs-lookup"><span data-stu-id="00d91-160">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="00d91-161">b.</span><span class="sxs-lookup"><span data-stu-id="00d91-161">b.</span></span> <span data-ttu-id="00d91-162">As **User Data Updates**, select **Preference Veracode User Data**.</span><span class="sxs-lookup"><span data-stu-id="00d91-162">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="00d91-163">c.</span><span class="sxs-lookup"><span data-stu-id="00d91-163">c.</span></span> <span data-ttu-id="00d91-164">For **SAML Attribute Details**, select the following:</span><span class="sxs-lookup"><span data-stu-id="00d91-164">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="00d91-165">**User Roles**</span><span class="sxs-lookup"><span data-stu-id="00d91-165">**User Roles**</span></span>
      * <span data-ttu-id="00d91-166">**Policy Administrator**</span><span class="sxs-lookup"><span data-stu-id="00d91-166">**Policy Administrator**</span></span>
      * <span data-ttu-id="00d91-167">**Reviewer**</span><span class="sxs-lookup"><span data-stu-id="00d91-167">**Reviewer**</span></span>
      * <span data-ttu-id="00d91-168">**Security Lead**</span><span class="sxs-lookup"><span data-stu-id="00d91-168">**Security Lead**</span></span>
      * <span data-ttu-id="00d91-169">**Executive**</span><span class="sxs-lookup"><span data-stu-id="00d91-169">**Executive**</span></span>
      * <span data-ttu-id="00d91-170">**Submitter**</span><span class="sxs-lookup"><span data-stu-id="00d91-170">**Submitter**</span></span>
      * <span data-ttu-id="00d91-171">**Creator**</span><span class="sxs-lookup"><span data-stu-id="00d91-171">**Creator**</span></span>
      * <span data-ttu-id="00d91-172">**All Scan Types**</span><span class="sxs-lookup"><span data-stu-id="00d91-172">**All Scan Types**</span></span>
      * <span data-ttu-id="00d91-173">**Team Memberships**</span><span class="sxs-lookup"><span data-stu-id="00d91-173">**Team Memberships**</span></span>
      * <span data-ttu-id="00d91-174">**Default Team**</span><span class="sxs-lookup"><span data-stu-id="00d91-174">**Default Team**</span></span>

10. <span data-ttu-id="00d91-175">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="00d91-175">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="00d91-176">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802914.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="00d91-176">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802914.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="00d91-177">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="00d91-177">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
    
    <span data-ttu-id="00d91-178">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC795920.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="00d91-178">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC795920.png "Attributes")</span></span>

12. <span data-ttu-id="00d91-179">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="00d91-179">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="00d91-180">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802906.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="00d91-180">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802906.png "Attributes")</span></span>
    
    | <span data-ttu-id="00d91-181">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="00d91-181">Attribute Name</span></span> | <span data-ttu-id="00d91-182">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="00d91-182">Attribute Value</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="00d91-183">firstname</span><span class="sxs-lookup"><span data-stu-id="00d91-183">firstname</span></span> |<span data-ttu-id="00d91-184">User.givenname</span><span class="sxs-lookup"><span data-stu-id="00d91-184">User.givenname</span></span> |
    | <span data-ttu-id="00d91-185">lastname</span><span class="sxs-lookup"><span data-stu-id="00d91-185">lastname</span></span> |<span data-ttu-id="00d91-186">User.surname</span><span class="sxs-lookup"><span data-stu-id="00d91-186">User.surname</span></span> |
    | <span data-ttu-id="00d91-187">email</span><span class="sxs-lookup"><span data-stu-id="00d91-187">email</span></span> |<span data-ttu-id="00d91-188">User.mail</span><span class="sxs-lookup"><span data-stu-id="00d91-188">User.mail</span></span> |
    
    <span data-ttu-id="00d91-189">a.</span><span class="sxs-lookup"><span data-stu-id="00d91-189">a.</span></span> <span data-ttu-id="00d91-190">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="00d91-190">For each data row in the table above, click **add user attribute**.</span></span>

    <span data-ttu-id="00d91-191">b.</span><span class="sxs-lookup"><span data-stu-id="00d91-191">b.</span></span> <span data-ttu-id="00d91-192">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="00d91-192">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="00d91-193">c.</span><span class="sxs-lookup"><span data-stu-id="00d91-193">c.</span></span> <span data-ttu-id="00d91-194">In the **Attribute Value** textbox, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="00d91-194">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>

    <span data-ttu-id="00d91-195">d.</span><span class="sxs-lookup"><span data-stu-id="00d91-195">d.</span></span> <span data-ttu-id="00d91-196">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="00d91-196">Click **Complete**.</span></span>

13. <span data-ttu-id="00d91-197">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="00d91-197">Click **Apply Changes**.</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="00d91-198">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="00d91-198">Configuring user provisioning</span></span>
<span data-ttu-id="00d91-199">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span><span class="sxs-lookup"><span data-stu-id="00d91-199">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span>  
<span data-ttu-id="00d91-200">In the case of Veracode, provisioning is an automated task.</span><span class="sxs-lookup"><span data-stu-id="00d91-200">In the case of Veracode, provisioning is an automated task.</span></span>  
<span data-ttu-id="00d91-201">There is no action item for you..</span><span class="sxs-lookup"><span data-stu-id="00d91-201">There is no action item for you..</span></span>

<span data-ttu-id="00d91-202">Users are automatically created if necessary during the first single sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="00d91-202">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="00d91-203">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="00d91-203">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="00d91-204">Assigning users</span><span class="sxs-lookup"><span data-stu-id="00d91-204">Assigning users</span></span>
<span data-ttu-id="00d91-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="00d91-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-veracode-perform-the-following-steps"></a><span data-ttu-id="00d91-206">To assign users to Veracode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="00d91-206">To assign users to Veracode, perform the following steps:</span></span>
1. <span data-ttu-id="00d91-207">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="00d91-207">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="00d91-208">On the \*\*Veracode \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="00d91-208">On the \*\*Veracode \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="00d91-209">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802915.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="00d91-209">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802915.png "Assign Users")</span></span>

3. <span data-ttu-id="00d91-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="00d91-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="00d91-211">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="00d91-211">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="00d91-212">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="00d91-212">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="00d91-213">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00d91-213">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















