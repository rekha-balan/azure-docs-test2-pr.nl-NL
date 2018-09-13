---
title: 'Tutorial: Azure Active Directory Integration with PolicyStat | Microsoft Docs'
description: Learn how to use PolicyStat with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: a38c92f167127ae66af13908f83adce68ae698ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555963"
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="27f12-103">Tutorial: Azure Active Directory Integration with PolicyStat</span><span class="sxs-lookup"><span data-stu-id="27f12-103">Tutorial: Azure Active Directory Integration with PolicyStat</span></span>
<span data-ttu-id="27f12-104">The objective of this tutorial is to show the integration of Azure and PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="27f12-104">The objective of this tutorial is to show the integration of Azure and PolicyStat.</span></span>  

<span data-ttu-id="27f12-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="27f12-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="27f12-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="27f12-106">A valid Azure subscription</span></span>
* <span data-ttu-id="27f12-107">A PolicyStat tenant</span><span class="sxs-lookup"><span data-stu-id="27f12-107">A PolicyStat tenant</span></span>

<span data-ttu-id="27f12-108">After completing this tutorial, the Azure AD users you have assigned to PolicyStat will be able to single sign into the application at your PolicyStat company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="27f12-108">After completing this tutorial, the Azure AD users you have assigned to PolicyStat will be able to single sign into the application at your PolicyStat company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="27f12-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="27f12-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="27f12-110">Enabling the application integration for PolicyStat</span><span class="sxs-lookup"><span data-stu-id="27f12-110">Enabling the application integration for PolicyStat</span></span>
2. <span data-ttu-id="27f12-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="27f12-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="27f12-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="27f12-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="27f12-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="27f12-113">Assigning users</span></span>

<span data-ttu-id="27f12-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808662.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="27f12-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808662.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-policystat"></a><span data-ttu-id="27f12-115">Enable the application integration for PolicyStat</span><span class="sxs-lookup"><span data-stu-id="27f12-115">Enable the application integration for PolicyStat</span></span>
<span data-ttu-id="27f12-116">The objective of this section is to outline how to enable the application integration for PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="27f12-116">The objective of this section is to outline how to enable the application integration for PolicyStat.</span></span>

<span data-ttu-id="27f12-117">**To enable the application integration for PolicyStat, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27f12-117">**To enable the application integration for PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="27f12-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="27f12-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="27f12-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="27f12-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="27f12-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="27f12-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="27f12-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="27f12-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="27f12-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="27f12-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="27f12-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="27f12-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="27f12-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="27f12-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="27f12-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="27f12-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="27f12-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="27f12-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="27f12-127">In the **search box**, type **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="27f12-127">In the **search box**, type **PolicyStat**.</span></span>
   
   <span data-ttu-id="27f12-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808627.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="27f12-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808627.png "Application Gallery")</span></span>
7. <span data-ttu-id="27f12-129">In the results pane, select **PolicyStat**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="27f12-129">In the results pane, select **PolicyStat**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="27f12-130">![PolicyStat](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC810430.png "PolicyStat")</span><span class="sxs-lookup"><span data-stu-id="27f12-130">![PolicyStat](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC810430.png "PolicyStat")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="27f12-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="27f12-131">Configure single sign-on</span></span>

<span data-ttu-id="27f12-132">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="27f12-132">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="27f12-133">Your PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="27f12-133">Your PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>  

<span data-ttu-id="27f12-134">The following screenshot shows an example of this.</span><span class="sxs-lookup"><span data-stu-id="27f12-134">The following screenshot shows an example of this.</span></span>

<span data-ttu-id="27f12-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808628.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="27f12-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808628.png "Attributes")</span></span>

<span data-ttu-id="27f12-136">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27f12-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="27f12-137">In the Azure classic portal, on the **PolicyStat** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="27f12-137">In the Azure classic portal, on the **PolicyStat** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="27f12-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808629.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="27f12-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808629.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="27f12-139">On the **How would you like users to sign on to PolicyStat** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="27f12-139">On the **How would you like users to sign on to PolicyStat** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="27f12-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808630.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="27f12-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808630.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="27f12-141">On the **Configure App Settings** page, in the **Sign On URL** textbox, type the URL used by your users to sign-on to your URL PolicyStat application (e.g.: *“https://demo-azure.policystat.com”*), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="27f12-141">On the **Configure App Settings** page, in the **Sign On URL** textbox, type the URL used by your users to sign-on to your URL PolicyStat application (e.g.: *“https://demo-azure.policystat.com”*), and then click **Next**.</span></span>
   
   <span data-ttu-id="27f12-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808631.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="27f12-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808631.png "Configure App Settings")</span></span>
4. <span data-ttu-id="27f12-143">On the **Configure single sign-on at PolicyStat** page, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="27f12-143">On the **Configure single sign-on at PolicyStat** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="27f12-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808632.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="27f12-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808632.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="27f12-145">In a different web browser window, log into your PolicyStat company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="27f12-145">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>
6. <span data-ttu-id="27f12-146">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="27f12-146">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
   <span data-ttu-id="27f12-147">![Administrator Menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808633.png "Administrator Menu")</span><span class="sxs-lookup"><span data-stu-id="27f12-147">![Administrator Menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808633.png "Administrator Menu")</span></span>
7. <span data-ttu-id="27f12-148">In the **Setup** section, select **Enable Single Sign-on Integration**.</span><span class="sxs-lookup"><span data-stu-id="27f12-148">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
   <span data-ttu-id="27f12-149">![Single Sign-On Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808634.png "Single Sign-On Configuration")</span><span class="sxs-lookup"><span data-stu-id="27f12-149">![Single Sign-On Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808634.png "Single Sign-On Configuration")</span></span>
8. <span data-ttu-id="27f12-150">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="27f12-150">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
   <span data-ttu-id="27f12-151">![Single Sign-On Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808635.png "Single Sign-On Configuration")</span><span class="sxs-lookup"><span data-stu-id="27f12-151">![Single Sign-On Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808635.png "Single Sign-On Configuration")</span></span>
   
   1. <span data-ttu-id="27f12-152">In the **Username Attribute** textbox, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="27f12-152">In the **Username Attribute** textbox, type **uid**.</span></span>
   2. <span data-ttu-id="27f12-153">In the **First Name Attribute** textbox, type **firstname**.</span><span class="sxs-lookup"><span data-stu-id="27f12-153">In the **First Name Attribute** textbox, type **firstname**.</span></span>
   3. <span data-ttu-id="27f12-154">In the **Last Name Attribute** textbox, type **lastname**.</span><span class="sxs-lookup"><span data-stu-id="27f12-154">In the **Last Name Attribute** textbox, type **lastname**.</span></span>
   4. <span data-ttu-id="27f12-155">In the **Email Attribute** textbox, type **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="27f12-155">In the **Email Attribute** textbox, type **emailaddress**.</span></span>
   5. <span data-ttu-id="27f12-156">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="27f12-156">Click **Save Changes**.</span></span>
9. <span data-ttu-id="27f12-157">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="27f12-157">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
   <span data-ttu-id="27f12-158">![Single Sign-On Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808635.png "Single Sign-On Configuration")</span><span class="sxs-lookup"><span data-stu-id="27f12-158">![Single Sign-On Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808635.png "Single Sign-On Configuration")</span></span>
   
   1. <span data-ttu-id="27f12-159">Open your downloaded metadata file, copy the content, and then paste it into the **Your Identity Provider Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="27f12-159">Open your downloaded metadata file, copy the content, and then paste it into the **Your Identity Provider Metadata** textbox.</span></span>
   2. <span data-ttu-id="27f12-160">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="27f12-160">Click **Save Changes**.</span></span>
10. <span data-ttu-id="27f12-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="27f12-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="27f12-162">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC771723.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="27f12-162">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC771723.png "Configure Single Sign-On")</span></span>
  
11. <span data-ttu-id="27f12-163">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="27f12-163">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
    
    <span data-ttu-id="27f12-164">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC795920.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="27f12-164">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC795920.png "Attributes")</span></span>
12. <span data-ttu-id="27f12-165">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="27f12-165">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="27f12-166">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC804823.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="27f12-166">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC804823.png "Attributes")</span></span>
    
   1. <span data-ttu-id="27f12-167">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="27f12-167">Click **add user attribute**.</span></span>
   2. <span data-ttu-id="27f12-168">In the **Attribute Name** textbox, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="27f12-168">In the **Attribute Name** textbox, type **uid**.</span></span>
   3. <span data-ttu-id="27f12-169">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="27f12-169">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   4. <span data-ttu-id="27f12-170">From the **Mail** list, select **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="27f12-170">From the **Mail** list, select **User.mail**.</span></span>
   5. <span data-ttu-id="27f12-171">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="27f12-171">Click **Complete**.</span></span>

##<a name="configure-user-provisioning"></a><span data-ttu-id="27f12-172">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="27f12-172">Configure user provisioning</span></span>

<span data-ttu-id="27f12-173">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="27f12-173">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="27f12-174">PolicyStat supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="27f12-174">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="27f12-175">This means, you do not need to add the users manually to PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="27f12-175">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="27f12-176">The users will get added automatically on their first login through SSO.</span><span class="sxs-lookup"><span data-stu-id="27f12-176">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="27f12-177">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="27f12-177">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="27f12-178">Assign users</span><span class="sxs-lookup"><span data-stu-id="27f12-178">Assign users</span></span>
<span data-ttu-id="27f12-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="27f12-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="27f12-180">**To assign users to PolicyStat, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27f12-180">**To assign users to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="27f12-181">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="27f12-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="27f12-182">On the **PolicyStat** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="27f12-182">On the **PolicyStat** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="27f12-183">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808636.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="27f12-183">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC808636.png "Assign Users")</span></span>
3. <span data-ttu-id="27f12-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="27f12-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="27f12-185">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="27f12-185">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-policystat-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="27f12-186">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="27f12-186">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="27f12-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="27f12-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















