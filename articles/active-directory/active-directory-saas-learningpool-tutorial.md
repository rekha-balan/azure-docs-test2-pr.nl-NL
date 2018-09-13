---
title: 'Tutorial: Azure Active Directory integration with Learningpool | Microsoft Docs'
description: Learn how to use Learningpool with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: dc61cf351ed962a5ab0ef14c652ddf13baf93dc0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549411"
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool"></a><span data-ttu-id="6d343-103">Tutorial: Azure Active Directory integration with Learningpool</span><span class="sxs-lookup"><span data-stu-id="6d343-103">Tutorial: Azure Active Directory integration with Learningpool</span></span>
<span data-ttu-id="6d343-104">The objective of this tutorial is to show the integration of Azure and Learningpool.</span><span class="sxs-lookup"><span data-stu-id="6d343-104">The objective of this tutorial is to show the integration of Azure and Learningpool.</span></span>  

<span data-ttu-id="6d343-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6d343-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6d343-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="6d343-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6d343-107">A Learningpool single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6d343-107">A Learningpool single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="6d343-108">After completing this tutorial, the Azure AD users you have assigned to Learningpool will be able to single sign into the application at your Learningpool company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d343-108">After completing this tutorial, the Azure AD users you have assigned to Learningpool will be able to single sign into the application at your Learningpool company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6d343-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6d343-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="6d343-110">Enabling the application integration for Learningpool</span><span class="sxs-lookup"><span data-stu-id="6d343-110">Enabling the application integration for Learningpool</span></span>
2. <span data-ttu-id="6d343-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="6d343-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="6d343-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6d343-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="6d343-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6d343-113">Assigning users</span></span>

<span data-ttu-id="6d343-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC791166.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="6d343-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC791166.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-learningpool"></a><span data-ttu-id="6d343-115">Enabling the application integration for Learningpool</span><span class="sxs-lookup"><span data-stu-id="6d343-115">Enabling the application integration for Learningpool</span></span>
<span data-ttu-id="6d343-116">The objective of this section is to outline how to enable the application integration for Learningpool.</span><span class="sxs-lookup"><span data-stu-id="6d343-116">The objective of this section is to outline how to enable the application integration for Learningpool.</span></span>

<span data-ttu-id="6d343-117">**To enable the application integration for Learningpool, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6d343-117">**To enable the application integration for Learningpool, perform the following steps:**</span></span>

1. <span data-ttu-id="6d343-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d343-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6d343-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6d343-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6d343-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6d343-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6d343-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6d343-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="6d343-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6d343-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6d343-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6d343-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="6d343-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="6d343-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6d343-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6d343-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="6d343-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="6d343-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6d343-127">In the **search box**, type **Learningpool**.</span><span class="sxs-lookup"><span data-stu-id="6d343-127">In the **search box**, type **Learningpool**.</span></span>
   
   <span data-ttu-id="6d343-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795073.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="6d343-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795073.png "Application Gallery")</span></span>
7. <span data-ttu-id="6d343-129">In the results pane, select **Learningpool**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6d343-129">In the results pane, select **Learningpool**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="6d343-130">![Learningpool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC809577.png "Learningpool")</span><span class="sxs-lookup"><span data-stu-id="6d343-130">![Learningpool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC809577.png "Learningpool")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="6d343-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="6d343-131">Configuring single sign-on</span></span>

<span data-ttu-id="6d343-132">The objective of this section is to outline how to enable users to authenticate to Learningpool with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="6d343-132">The objective of this section is to outline how to enable users to authenticate to Learningpool with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="6d343-133">Your Learningpool application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="6d343-133">Your Learningpool application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>  
<span data-ttu-id="6d343-134">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="6d343-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="6d343-135">![SAML Token Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795074.png "SAML Token Attributes")</span><span class="sxs-lookup"><span data-stu-id="6d343-135">![SAML Token Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795074.png "SAML Token Attributes")</span></span>

<span data-ttu-id="6d343-136">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6d343-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="6d343-137">In the Azure classic portal, on the **Learningpool** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="6d343-137">In the Azure classic portal, on the **Learningpool** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="6d343-138">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795075.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="6d343-138">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795075.png "Attributes")</span></span>
2. <span data-ttu-id="6d343-139">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6d343-139">To add the required attribute mappings, perform the following steps:</span></span>
   
   ### 
   | <span data-ttu-id="6d343-140">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="6d343-140">Attribute Name</span></span> | <span data-ttu-id="6d343-141">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="6d343-141">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="6d343-142">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="6d343-142">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="6d343-143">User.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="6d343-143">User.userprincipalname</span></span> |
   |  <span data-ttu-id="6d343-144">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="6d343-144">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="6d343-145">User.givenname</span><span class="sxs-lookup"><span data-stu-id="6d343-145">User.givenname</span></span> |
   | <span data-ttu-id="6d343-146">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="6d343-146">urn:oid:0.9.2342.19200300.100.1.3</span></span> |<span data-ttu-id="6d343-147">User.mail</span><span class="sxs-lookup"><span data-stu-id="6d343-147">User.mail</span></span> |
   | <span data-ttu-id="6d343-148">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="6d343-148">urn:oid:2.5.4.4</span></span> |<span data-ttu-id="6d343-149">User.surname</span><span class="sxs-lookup"><span data-stu-id="6d343-149">User.surname</span></span> |
   
   1. <span data-ttu-id="6d343-150">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="6d343-150">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="6d343-151">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="6d343-151">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="6d343-152">From the **Attribute Value** list, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="6d343-152">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="6d343-153">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6d343-153">Click **Complete**.</span></span>
3. <span data-ttu-id="6d343-154">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="6d343-154">Click **Apply Changes**.</span></span>
4. <span data-ttu-id="6d343-155">In your browser, click **Back** to open the **Quick Start** dialog again.</span><span class="sxs-lookup"><span data-stu-id="6d343-155">In your browser, click **Back** to open the **Quick Start** dialog again.</span></span>
5. <span data-ttu-id="6d343-156">Click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="6d343-156">Click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="6d343-157">![Configure Singel Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795076.png "Configure Singel Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6d343-157">![Configure Singel Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795076.png "Configure Singel Sign-On")</span></span>
6. <span data-ttu-id="6d343-158">On the **How would you like users to sign on to Learningpool** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d343-158">On the **How would you like users to sign on to Learningpool** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6d343-159">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795077.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6d343-159">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795077.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="6d343-160">On the **Configure App URL** page, in the **Learningpool Sign On URL** textbox, type the URL used by your users to sign on to your Learningpool application ( e.g.: https://parliament.preview.learningpool.com/auth/shibboleth/index.php), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d343-160">On the **Configure App URL** page, in the **Learningpool Sign On URL** textbox, type the URL used by your users to sign on to your Learningpool application ( e.g.: https://parliament.preview.learningpool.com/auth/shibboleth/index.php), and then click **Next**.</span></span>
   
   <span data-ttu-id="6d343-161">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795078.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="6d343-161">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795078.png "Configure App URL")</span></span>
8. <span data-ttu-id="6d343-162">On the **Configure single sign-on at Learningpool** page, to download your metadata, click **Download metadata**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="6d343-162">On the **Configure single sign-on at Learningpool** page, to download your metadata, click **Download metadata**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="6d343-163">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795079.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6d343-163">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795079.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="6d343-164">Forward that Metadata file to your Learningpool Support team.</span><span class="sxs-lookup"><span data-stu-id="6d343-164">Forward that Metadata file to your Learningpool Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="6d343-165">SSO has to be enabled by the Learningpool support team.</span><span class="sxs-lookup"><span data-stu-id="6d343-165">SSO has to be enabled by the Learningpool support team.</span></span>
   > 
   
10. <span data-ttu-id="6d343-166">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6d343-166">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="6d343-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795080.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6d343-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795080.png "Configure Single Sign-On")</span></span>
    
## <a name="configuring-user-provisioning"></a><span data-ttu-id="6d343-168">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6d343-168">Configuring user provisioning</span></span>

<span data-ttu-id="6d343-169">In order to enable Azure AD users to log into Learningpool, they must be provisioned into Learningpool.</span><span class="sxs-lookup"><span data-stu-id="6d343-169">In order to enable Azure AD users to log into Learningpool, they must be provisioned into Learningpool.</span></span>

<span data-ttu-id="6d343-170">There is no action item for you to configure user provisioning to Learningpool.</span><span class="sxs-lookup"><span data-stu-id="6d343-170">There is no action item for you to configure user provisioning to Learningpool.</span></span>  
<span data-ttu-id="6d343-171">Users need to be created by your Learningpool support team.</span><span class="sxs-lookup"><span data-stu-id="6d343-171">Users need to be created by your Learningpool support team.</span></span>

>[!NOTE]
><span data-ttu-id="6d343-172">You can use any other Learningpool user account creation tools or APIs provided by Learningpool to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="6d343-172">You can use any other Learningpool user account creation tools or APIs provided by Learningpool to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="6d343-173">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6d343-173">Assigning users</span></span>
<span data-ttu-id="6d343-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="6d343-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="6d343-175">**To assign users to Learningpool, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6d343-175">**To assign users to Learningpool, perform the following steps:**</span></span>

1. <span data-ttu-id="6d343-176">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="6d343-176">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6d343-177">On the **Learningpool** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="6d343-177">On the **Learningpool** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6d343-178">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795081.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="6d343-178">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC795081.png "Assign Users")</span></span>
3. <span data-ttu-id="6d343-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="6d343-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="6d343-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="6d343-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learningpool-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6d343-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6d343-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="6d343-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d343-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















