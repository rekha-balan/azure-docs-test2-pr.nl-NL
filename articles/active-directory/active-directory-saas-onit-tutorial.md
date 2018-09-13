---
title: 'Tutorial: Azure Active Directory integration with Onit | Microsoft Docs'
description: Learn how to use Onit with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 87df9cf2c83e904e58946e348aa791ed2b4724e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555459"
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="e18a0-103">Tutorial: Azure Active Directory integration with Onit</span><span class="sxs-lookup"><span data-stu-id="e18a0-103">Tutorial: Azure Active Directory integration with Onit</span></span>
<span data-ttu-id="e18a0-104">The objective of this tutorial is to show the integration of Azure and Onit.</span><span class="sxs-lookup"><span data-stu-id="e18a0-104">The objective of this tutorial is to show the integration of Azure and Onit.</span></span>  

<span data-ttu-id="e18a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="e18a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="e18a0-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e18a0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e18a0-107">An Onit single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e18a0-107">An Onit single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="e18a0-108">After completing this tutorial, the Azure AD users you have assigned to Onit will be able to single sign-on (SSO) to the application at your Onit company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e18a0-108">After completing this tutorial, the Azure AD users you have assigned to Onit will be able to single sign-on (SSO) to the application at your Onit company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e18a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e18a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="e18a0-110">Enabling the application integration for Onit</span><span class="sxs-lookup"><span data-stu-id="e18a0-110">Enabling the application integration for Onit</span></span>
2. <span data-ttu-id="e18a0-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="e18a0-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="e18a0-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="e18a0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="e18a0-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="e18a0-113">Assigning users</span></span>

<span data-ttu-id="e18a0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791166.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="e18a0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791166.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-onit"></a><span data-ttu-id="e18a0-115">Enable the application integration for Onit</span><span class="sxs-lookup"><span data-stu-id="e18a0-115">Enable the application integration for Onit</span></span>
<span data-ttu-id="e18a0-116">The objective of this section is to outline how to enable the application integration for Onit.</span><span class="sxs-lookup"><span data-stu-id="e18a0-116">The objective of this section is to outline how to enable the application integration for Onit.</span></span>

<span data-ttu-id="e18a0-117">**To enable the application integration for Onit, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18a0-117">**To enable the application integration for Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="e18a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="e18a0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e18a0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e18a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e18a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e18a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e18a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="e18a0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="e18a0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e18a0-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e18a0-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="e18a0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="e18a0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e18a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="e18a0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="e18a0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e18a0-127">In the **search box**, type **Onit**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-127">In the **search box**, type **Onit**.</span></span>
   
   <span data-ttu-id="e18a0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791167.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="e18a0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791167.png "Application Gallery")</span></span>
7. <span data-ttu-id="e18a0-129">In the results pane, select **Onit**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e18a0-129">In the results pane, select **Onit**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="e18a0-130">![Onit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC795325.png "Onit")</span><span class="sxs-lookup"><span data-stu-id="e18a0-130">![Onit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC795325.png "Onit")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e18a0-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="e18a0-131">Configure single sign-on</span></span>

<span data-ttu-id="e18a0-132">The objective of this section is to outline how to enable users to authenticate to Onit with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="e18a0-132">The objective of this section is to outline how to enable users to authenticate to Onit with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="e18a0-133">Configuring SSO for Onit requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="e18a0-133">Configuring SSO for Onit requires you to retrieve a thumbprint value from a certificate.</span></span>

<span data-ttu-id="e18a0-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="e18a0-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="e18a0-135">Your Onit application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="e18a0-135">Your Onit application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>  

<span data-ttu-id="e18a0-136">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="e18a0-136">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="e18a0-137">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791168.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e18a0-137">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791168.png "Single Sign-On")</span></span>

<span data-ttu-id="e18a0-138">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18a0-138">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="e18a0-139">In the Azure classic portal, on the **Onit** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="e18a0-139">In the Azure classic portal, on the **Onit** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="e18a0-140">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791169.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="e18a0-140">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791169.png "Attributes")</span></span>
2. <span data-ttu-id="e18a0-141">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18a0-141">To add the required attribute mappings, perform the following steps:</span></span>

   |<span data-ttu-id="e18a0-142">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="e18a0-142">Attribute Name</span></span>|<span data-ttu-id="e18a0-143">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="e18a0-143">Attribute Value</span></span>|
   |---|---|
   |<span data-ttu-id="e18a0-144">name</span><span class="sxs-lookup"><span data-stu-id="e18a0-144">name</span></span>|<span data-ttu-id="e18a0-145">User.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="e18a0-145">User.userprincipalname</span></span>|
   |<span data-ttu-id="e18a0-146">email</span><span class="sxs-lookup"><span data-stu-id="e18a0-146">email</span></span>|<span data-ttu-id="e18a0-147">User.mail</span><span class="sxs-lookup"><span data-stu-id="e18a0-147">User.mail</span></span>|

   1. <span data-ttu-id="e18a0-148">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-148">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="e18a0-149">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="e18a0-149">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="e18a0-150">From the **Attribute Value** list, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="e18a0-150">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="e18a0-151">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-151">Click **Complete**.</span></span>

3. <span data-ttu-id="e18a0-152">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-152">Click **Apply Changes**.</span></span>
4. <span data-ttu-id="e18a0-153">In your browser, click **Back** to open the **Quick Start** dialog again.</span><span class="sxs-lookup"><span data-stu-id="e18a0-153">In your browser, click **Back** to open the **Quick Start** dialog again.</span></span>
5. <span data-ttu-id="e18a0-154">Click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="e18a0-154">Click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="e18a0-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791170.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e18a0-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791170.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="e18a0-156">On the **How would you like users to sign on to Onit** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-156">On the **How would you like users to sign on to Onit** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="e18a0-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791171.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e18a0-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791171.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="e18a0-158">On the **Configure App URL** page, in the **Onit Sign On URL** textbox, type the URL used by your users to sign on to your Onit application (e.g.: "*https://ms-sso-test.onit.com*”), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-158">On the **Configure App URL** page, in the **Onit Sign On URL** textbox, type the URL used by your users to sign on to your Onit application (e.g.: "*https://ms-sso-test.onit.com*”), and then click **Next**.</span></span>
   
   <span data-ttu-id="e18a0-159">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791172.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="e18a0-159">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791172.png "Configure App URL")</span></span>
8. <span data-ttu-id="e18a0-160">On the **Configure single sign-on at Onit** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="e18a0-160">On the **Configure single sign-on at Onit** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="e18a0-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791173.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e18a0-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791173.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="e18a0-162">In a different web browser window, log into your Onit company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e18a0-162">In a different web browser window, log into your Onit company site as an administrator.</span></span>
10. <span data-ttu-id="e18a0-163">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-163">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="e18a0-164">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="e18a0-164">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="e18a0-165">Click **Edit Corporation**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-165">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="e18a0-166">![Edit Corporation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span><span class="sxs-lookup"><span data-stu-id="e18a0-166">![Edit Corporation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
12. <span data-ttu-id="e18a0-167">Click the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="e18a0-167">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="e18a0-168">![Edit Company Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span><span class="sxs-lookup"><span data-stu-id="e18a0-168">![Edit Company Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>
13. <span data-ttu-id="e18a0-169">On the **Security** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18a0-169">On the **Security** tab, perform the following steps:</span></span>
    
   <span data-ttu-id="e18a0-170">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e18a0-170">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>
    
   1. <span data-ttu-id="e18a0-171">As **Authentication Strategy**, select **Single Sign On and Password**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-171">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
   2. <span data-ttu-id="e18a0-172">In the Azure classic portal, on the **Configure single sign-on at Onit** dialog page, copy the **Remote Login URL** value, and then paste it into the **Idp Target URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e18a0-172">In the Azure classic portal, on the **Configure single sign-on at Onit** dialog page, copy the **Remote Login URL** value, and then paste it into the **Idp Target URL** textbox.</span></span>
   3. <span data-ttu-id="e18a0-173">In the Azure classic portal, on the **Configure single sign-on at Onit** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Idp logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e18a0-173">In the Azure classic portal, on the **Configure single sign-on at Onit** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Idp logout URL** textbox.</span></span>
   4. <span data-ttu-id="e18a0-174">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Idp Cert Fingerprint (SHA1)** textbox.</span><span class="sxs-lookup"><span data-stu-id="e18a0-174">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Idp Cert Fingerprint (SHA1)** textbox.</span></span>    
      >[!TIP]
      ><span data-ttu-id="e18a0-175">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="e18a0-175">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>
      >
      
   5. <span data-ttu-id="e18a0-176">As **SSO Type**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-176">As **SSO Type**, select **SAML**.</span></span>
   6. <span data-ttu-id="e18a0-177">In the **SSO login button text** textbox, type a button text you like.</span><span class="sxs-lookup"><span data-stu-id="e18a0-177">In the **SSO login button text** textbox, type a button text you like.</span></span>
   7. <span data-ttu-id="e18a0-178">Select **Login with SSO: Required for the following domains/users**, type the email address of a test user into the related textbox, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-178">Select **Login with SSO: Required for the following domains/users**, type the email address of a test user into the related textbox, and then click **Update**.</span></span>
   
       <span data-ttu-id="e18a0-179">![Edit Corporation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791178.png "Edit Corporation")</span><span class="sxs-lookup"><span data-stu-id="e18a0-179">![Edit Corporation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791178.png "Edit Corporation")</span></span>  
14. <span data-ttu-id="e18a0-180">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="e18a0-180">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="e18a0-181">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791179.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e18a0-181">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791179.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="e18a0-182">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="e18a0-182">Configure user provisioning</span></span>

<span data-ttu-id="e18a0-183">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span><span class="sxs-lookup"><span data-stu-id="e18a0-183">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="e18a0-184">In the case of Onit, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e18a0-184">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="e18a0-185">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18a0-185">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e18a0-186">Sign on to your **Onit** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e18a0-186">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="e18a0-187">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-187">Click **Add User**.</span></span>
   
   <span data-ttu-id="e18a0-188">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="e18a0-188">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="e18a0-189">On the **Add User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18a0-189">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="e18a0-190">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="e18a0-190">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="e18a0-191">Type the **Name** and the **Email Address** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="e18a0-191">Type the **Name** and the **Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="e18a0-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-192">Click **Create**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="e18a0-193">The account owner will get an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="e18a0-193">The account owner will get an email including a link to confirm the account before it becomes active.</span></span>
      >
      >
     

> [!NOTE]
> <span data-ttu-id="e18a0-194">You can use any other Onit user account creation tools or APIs provided by Onit to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="e18a0-194">You can use any other Onit user account creation tools or APIs provided by Onit to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="e18a0-195">Assign users</span><span class="sxs-lookup"><span data-stu-id="e18a0-195">Assign users</span></span>

<span data-ttu-id="e18a0-196">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="e18a0-196">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="e18a0-197">**To assign users to Onit, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18a0-197">**To assign users to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="e18a0-198">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="e18a0-198">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e18a0-199">On the **Onit** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="e18a0-199">On the **Onit** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e18a0-200">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791182.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="e18a0-200">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC791182.png "Assign Users")</span></span>
3. <span data-ttu-id="e18a0-201">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="e18a0-201">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="e18a0-202">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="e18a0-202">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-onit-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e18a0-203">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e18a0-203">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="e18a0-204">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e18a0-204">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e18a0-205">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e18a0-205">Additional resources</span></span>

* [<span data-ttu-id="e18a0-206">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e18a0-206">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e18a0-207">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e18a0-207">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)























