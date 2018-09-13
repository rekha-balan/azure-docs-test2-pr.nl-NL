---
title: 'Tutorial: Azure Active Directory integration with Tinfoil Security | Microsoft Docs'
description: Learn how to use Tinfoil Security with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 74de2d568b011209b31be8b4ca116739e97e4ed3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555601"
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="5d23f-103">Tutorial: Azure Active Directory integration with Tinfoil Security</span><span class="sxs-lookup"><span data-stu-id="5d23f-103">Tutorial: Azure Active Directory integration with Tinfoil Security</span></span>
<span data-ttu-id="5d23f-104">The objective of this tutorial is to show the integration of Azure and Tinfoil Security.</span><span class="sxs-lookup"><span data-stu-id="5d23f-104">The objective of this tutorial is to show the integration of Azure and Tinfoil Security.</span></span>  
<span data-ttu-id="5d23f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="5d23f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5d23f-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5d23f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5d23f-107">A Tinfoil Security single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5d23f-107">A Tinfoil Security single sign-on enabled subscription</span></span>

<span data-ttu-id="5d23f-108">After completing this tutorial, the Azure AD users you have assigned to Tinfoil Security will be able to single sign into the application at your Tinfoil Security company site (identity provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5d23f-108">After completing this tutorial, the Azure AD users you have assigned to Tinfoil Security will be able to single sign into the application at your Tinfoil Security company site (identity provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5d23f-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5d23f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="5d23f-110">Enabling the application integration for Tinfoil Security</span><span class="sxs-lookup"><span data-stu-id="5d23f-110">Enabling the application integration for Tinfoil Security</span></span>
2. <span data-ttu-id="5d23f-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5d23f-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="5d23f-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5d23f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5d23f-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5d23f-113">Assigning users</span></span>

<span data-ttu-id="5d23f-114">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798965.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5d23f-114">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798965.png "Configure Single Sign-On")</span></span>

## <a name="enabling-the-application-integration-for-tinfoil-security"></a><span data-ttu-id="5d23f-115">Enabling the application integration for Tinfoil Security</span><span class="sxs-lookup"><span data-stu-id="5d23f-115">Enabling the application integration for Tinfoil Security</span></span>
<span data-ttu-id="5d23f-116">The objective of this section is to outline how to enable the application integration for Tinfoil Security.</span><span class="sxs-lookup"><span data-stu-id="5d23f-116">The objective of this section is to outline how to enable the application integration for Tinfoil Security.</span></span>

### <a name="to-enable-the-application-integration-for-tinfoil-security-perform-the-following-steps"></a><span data-ttu-id="5d23f-117">To enable the application integration for Tinfoil Security, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d23f-117">To enable the application integration for Tinfoil Security, perform the following steps:</span></span>
1. <span data-ttu-id="5d23f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="5d23f-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5d23f-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="5d23f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5d23f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="5d23f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5d23f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="5d23f-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="5d23f-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="5d23f-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5d23f-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="5d23f-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="5d23f-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="5d23f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="5d23f-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="5d23f-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="5d23f-127">In the **search box**, type **Tinfoil Security**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-127">In the **search box**, type **Tinfoil Security**.</span></span>
   
    <span data-ttu-id="5d23f-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798966.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="5d23f-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798966.png "Application Gallery")</span></span>

7. <span data-ttu-id="5d23f-129">In the results pane, select **Tinfoil Security**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5d23f-129">In the results pane, select **Tinfoil Security**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="5d23f-130">![Tinfoil Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC802771.png "Tinfoil Security")</span><span class="sxs-lookup"><span data-stu-id="5d23f-130">![Tinfoil Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC802771.png "Tinfoil Security")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="5d23f-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5d23f-131">Configuring single sign-on</span></span>
<span data-ttu-id="5d23f-132">The objective of this section is to outline how to enable users to authenticate to Tinfoil Security with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="5d23f-132">The objective of this section is to outline how to enable users to authenticate to Tinfoil Security with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="5d23f-133">Configuring single sign-on for Tinfoil Security requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="5d23f-133">Configuring single sign-on for Tinfoil Security requires you to retrieve a thumbprint value from a certificate.</span></span>  
<span data-ttu-id="5d23f-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="5d23f-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="5d23f-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d23f-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="5d23f-136">In the Azure classic portal, on the **Tinfoil Security** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="5d23f-136">In the Azure classic portal, on the **Tinfoil Security** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="5d23f-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798967.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5d23f-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798967.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="5d23f-138">On the **How would you like users to sign on to Tinfoil Security** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-138">On the **How would you like users to sign on to Tinfoil Security** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5d23f-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798968.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5d23f-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798968.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="5d23f-140">On the **Configure App URL** page, in the **Tinfoil Security Reply URL** textbox, type your Tinfoil Security Assertion Consumer Service (ACS) URL (e.g.: "*https://www.tinfoilsecurity.com/saml/consume*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-140">On the **Configure App URL** page, in the **Tinfoil Security Reply URL** textbox, type your Tinfoil Security Assertion Consumer Service (ACS) URL (e.g.: "*https://www.tinfoilsecurity.com/saml/consume*", and then click **Next**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5d23f-141">You should be able to get the ACS URL from Tinfoil Security Metadata (https://www.tinfoilsecurity.com/saml/metadata).</span><span class="sxs-lookup"><span data-stu-id="5d23f-141">You should be able to get the ACS URL from Tinfoil Security Metadata (https://www.tinfoilsecurity.com/saml/metadata).</span></span>
    > 
    > 
   
    <span data-ttu-id="5d23f-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798969.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="5d23f-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798969.png "Configure App URL")</span></span>

4. <span data-ttu-id="5d23f-143">On the **Configure single sign-on at Tinfoil Security** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Tinfoil Security.cer**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-143">On the **Configure single sign-on at Tinfoil Security** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Tinfoil Security.cer**.</span></span>
   
    <span data-ttu-id="5d23f-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798970.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5d23f-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798970.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="5d23f-145">In a different web browser window, log into your Tinfoil Security company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5d23f-145">In a different web browser window, log into your Tinfoil Security company site as an administrator.</span></span>

6. <span data-ttu-id="5d23f-146">In the toolbar on the top, click **My Account**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-146">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="5d23f-147">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798971.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="5d23f-147">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798971.png "Dashboard")</span></span>

7. <span data-ttu-id="5d23f-148">Click **Security**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-148">Click **Security**.</span></span>
   
    <span data-ttu-id="5d23f-149">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798972.png "Security")</span><span class="sxs-lookup"><span data-stu-id="5d23f-149">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798972.png "Security")</span></span>

8. <span data-ttu-id="5d23f-150">On the **Single Sign-On** configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d23f-150">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="5d23f-151">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798973.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5d23f-151">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="5d23f-152">a.</span><span class="sxs-lookup"><span data-stu-id="5d23f-152">a.</span></span> <span data-ttu-id="5d23f-153">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-153">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="5d23f-154">b.</span><span class="sxs-lookup"><span data-stu-id="5d23f-154">b.</span></span> <span data-ttu-id="5d23f-155">Click **Manual Configuration**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-155">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="5d23f-156">c.</span><span class="sxs-lookup"><span data-stu-id="5d23f-156">c.</span></span> <span data-ttu-id="5d23f-157">In the Azure classic portal, on the **Configure single sign-on at Tinfoil Security** dialog page, copy the **SAML SSO URL** value, and then paste it into the **SAML Post URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="5d23f-157">In the Azure classic portal, on the **Configure single sign-on at Tinfoil Security** dialog page, copy the **SAML SSO URL** value, and then paste it into the **SAML Post URL** textbox.</span></span>
   
    <span data-ttu-id="5d23f-158">d.</span><span class="sxs-lookup"><span data-stu-id="5d23f-158">d.</span></span> <span data-ttu-id="5d23f-159">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **SAML Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="5d23f-159">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **SAML Certificate Fingerprint** textbox.</span></span>  
      
    > [!TIP]
    > <span data-ttu-id="5d23f-160">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="5d23f-160">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span>
    > 
    > 
   
    <span data-ttu-id="5d23f-161">e.</span><span class="sxs-lookup"><span data-stu-id="5d23f-161">e.</span></span> <span data-ttu-id="5d23f-162">Copy **Your Account ID**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-162">Copy **Your Account ID**.</span></span>
   
    <span data-ttu-id="5d23f-163">f.</span><span class="sxs-lookup"><span data-stu-id="5d23f-163">f.</span></span> <span data-ttu-id="5d23f-164">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-164">Click **Save**.</span></span>

9. <span data-ttu-id="5d23f-165">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5d23f-165">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="5d23f-166">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798974.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5d23f-166">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798974.png "Configure Single Sign-On")</span></span>

10. <span data-ttu-id="5d23f-167">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="5d23f-167">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
    
    <span data-ttu-id="5d23f-168">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC795920.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="5d23f-168">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC795920.png "Attributes")</span></span>

11. <span data-ttu-id="5d23f-169">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d23f-169">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="5d23f-170">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798975.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="5d23f-170">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798975.png "Attributes")</span></span>
    
    <span data-ttu-id="5d23f-171">a.</span><span class="sxs-lookup"><span data-stu-id="5d23f-171">a.</span></span> <span data-ttu-id="5d23f-172">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-172">Click **add user attribute**.</span></span>

    <span data-ttu-id="5d23f-173">b.</span><span class="sxs-lookup"><span data-stu-id="5d23f-173">b.</span></span> <span data-ttu-id="5d23f-174">In the **Attribute Name** textbox, type **accountid**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-174">In the **Attribute Name** textbox, type **accountid**.</span></span>

    <span data-ttu-id="5d23f-175">c.</span><span class="sxs-lookup"><span data-stu-id="5d23f-175">c.</span></span> <span data-ttu-id="5d23f-176">In the **Attribute Value** textbox, paste the account ID value you have copied in the previous section.</span><span class="sxs-lookup"><span data-stu-id="5d23f-176">In the **Attribute Value** textbox, paste the account ID value you have copied in the previous section.</span></span>

    <span data-ttu-id="5d23f-177">d.</span><span class="sxs-lookup"><span data-stu-id="5d23f-177">d.</span></span> <span data-ttu-id="5d23f-178">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-178">Click **Complete**.</span></span>

12. <span data-ttu-id="5d23f-179">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-179">Click **Apply Changes**.</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="5d23f-180">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5d23f-180">Configuring user provisioning</span></span>
<span data-ttu-id="5d23f-181">In order to enable Azure AD users to log into Tinfoil Security, they must be provisioned into Tinfoil Security.</span><span class="sxs-lookup"><span data-stu-id="5d23f-181">In order to enable Azure AD users to log into Tinfoil Security, they must be provisioned into Tinfoil Security.</span></span>  
<span data-ttu-id="5d23f-182">In the case of Tinfoil Security, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="5d23f-182">In the case of Tinfoil Security, provisioning is a manual task.</span></span>

### <a name="to-get-a-user-provisioned-perform-the-following-steps"></a><span data-ttu-id="5d23f-183">To get a user provisioned, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d23f-183">To get a user provisioned, perform the following steps:</span></span>
1. <span data-ttu-id="5d23f-184">If the user is a part of an Enterprise account, you need to contact the Tinfoil Security support team to get the user account created.</span><span class="sxs-lookup"><span data-stu-id="5d23f-184">If the user is a part of an Enterprise account, you need to contact the Tinfoil Security support team to get the user account created.</span></span>
2. <span data-ttu-id="5d23f-185">If the user is a regular Tinfoil Security SaaS user, then the user can add a collaborator to any of the user’s sites.</span><span class="sxs-lookup"><span data-stu-id="5d23f-185">If the user is a regular Tinfoil Security SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="5d23f-186">This triggers a process to send an invitation to the specified email to create a new Tinfoil Security user account.</span><span class="sxs-lookup"><span data-stu-id="5d23f-186">This triggers a process to send an invitation to the specified email to create a new Tinfoil Security user account.</span></span>

> [!NOTE]
> <span data-ttu-id="5d23f-187">You can use any other Tinfoil Security user account creation tools or APIs provided by Tinfoil Security to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="5d23f-187">You can use any other Tinfoil Security user account creation tools or APIs provided by Tinfoil Security to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="5d23f-188">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5d23f-188">Assigning users</span></span>
<span data-ttu-id="5d23f-189">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="5d23f-189">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-tinfoil-security-perform-the-following-steps"></a><span data-ttu-id="5d23f-190">To assign users to Tinfoil Security, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d23f-190">To assign users to Tinfoil Security, perform the following steps:</span></span>
1. <span data-ttu-id="5d23f-191">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="5d23f-191">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5d23f-192">On the \*\*Tinfoil Security \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="5d23f-192">On the \*\*Tinfoil Security \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="5d23f-193">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798976.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="5d23f-193">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC798976.png "Assign Users")</span></span>

3. <span data-ttu-id="5d23f-194">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="5d23f-194">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="5d23f-195">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="5d23f-195">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tinfoil-security-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5d23f-196">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5d23f-196">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5d23f-197">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5d23f-197">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















