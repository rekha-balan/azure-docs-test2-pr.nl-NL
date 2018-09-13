---
title: 'Tutorial: Azure Active Directory integration with TimeOffManager | Microsoft Docs'
description: Learn how to use TimeOffManager with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/16/2017
ms.author: jeedes
ms.openlocfilehash: ecea5821ea360c291b18f9fbcfafb8b38d585d2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556612"
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="a42c3-103">Tutorial: Azure Active Directory integration with TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="a42c3-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>
<span data-ttu-id="a42c3-104">The objective of this tutorial is to show the integration of Azure and TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="a42c3-104">The objective of this tutorial is to show the integration of Azure and TimeOffManager.</span></span>  

<span data-ttu-id="a42c3-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a42c3-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a42c3-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a42c3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a42c3-107">A TimeOffManager single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a42c3-107">A TimeOffManager single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a42c3-108">After completing this tutorial, the Azure AD users you have assigned to TimeOffManager will be able to sign into the application with SSO at your TimeOffManager company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a42c3-108">After completing this tutorial, the Azure AD users you have assigned to TimeOffManager will be able to sign into the application with SSO at your TimeOffManager company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a42c3-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a42c3-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="a42c3-110">Enabling the application integration for TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="a42c3-110">Enabling the application integration for TimeOffManager</span></span>
* <span data-ttu-id="a42c3-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="a42c3-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="a42c3-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a42c3-112">Configuring user provisioning</span></span>
* <span data-ttu-id="a42c3-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a42c3-113">Assigning users</span></span>

<span data-ttu-id="a42c3-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795909.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a42c3-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795909.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-timeoffmanager"></a><span data-ttu-id="a42c3-115">Enable the application integration for TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="a42c3-115">Enable the application integration for TimeOffManager</span></span>
<span data-ttu-id="a42c3-116">The objective of this section is to outline how to enable the application integration for TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="a42c3-116">The objective of this section is to outline how to enable the application integration for TimeOffManager.</span></span>

<span data-ttu-id="a42c3-117">**To enable the application integration for TimeOffManager, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a42c3-117">**To enable the application integration for TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="a42c3-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a42c3-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a42c3-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a42c3-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a42c3-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a42c3-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a42c3-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a42c3-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a42c3-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a42c3-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a42c3-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a42c3-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a42c3-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a42c3-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a42c3-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a42c3-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a42c3-127">In the **search box**, type **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-127">In the **search box**, type **TimeOffManager**.</span></span>
   
   <span data-ttu-id="a42c3-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795910.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a42c3-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795910.png "Application Gallery")</span></span>
7. <span data-ttu-id="a42c3-129">In the results pane, select **TimeOffManager**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a42c3-129">In the results pane, select **TimeOffManager**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a42c3-130">![TimeOffManager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795911.png "TimeOffManager")</span><span class="sxs-lookup"><span data-stu-id="a42c3-130">![TimeOffManager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795911.png "TimeOffManager")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="a42c3-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a42c3-131">Configure single sign-on</span></span>
<span data-ttu-id="a42c3-132">The objective of this section is to outline how to enable users to authenticate to TimeOffManager with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a42c3-132">The objective of this section is to outline how to enable users to authenticate to TimeOffManager with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="a42c3-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your TimeOffManager tenant.</span><span class="sxs-lookup"><span data-stu-id="a42c3-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your TimeOffManager tenant.</span></span> <span data-ttu-id="a42c3-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a42c3-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="a42c3-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a42c3-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="a42c3-136">In the Azure classic portal, on the **TimeOffManager** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a42c3-136">In the Azure classic portal, on the **TimeOffManager** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a42c3-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795912.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a42c3-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795912.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a42c3-138">On the **How would you like users to sign on to TimeOffManager** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-138">On the **How would you like users to sign on to TimeOffManager** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a42c3-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795913.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a42c3-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795913.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="a42c3-140">On the **Configure App URL** page, in the **TimeOffManager Reply URL** textbox, type your TimeOffManager AssertionConsumerService URL (e.g.: "*Example: https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company\_id=IC34216*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-140">On the **Configure App URL** page, in the **TimeOffManager Reply URL** textbox, type your TimeOffManager AssertionConsumerService URL (e.g.: "*Example: https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company\_id=IC34216*", and then click **Next**.</span></span>
   
   <span data-ttu-id="a42c3-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795914.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a42c3-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795914.png "Configure App URL")</span></span>
   
   <span data-ttu-id="a42c3-142">You can get the reply URL from the TimeOffManager Single Sign on setting page.</span><span class="sxs-lookup"><span data-stu-id="a42c3-142">You can get the reply URL from the TimeOffManager Single Sign on setting page.</span></span>
   
   <span data-ttu-id="a42c3-143">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795915.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="a42c3-143">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795915.png "Single Sign-On Settings")</span></span>
4. <span data-ttu-id="a42c3-144">On the **Configure single sign-on at TimeOffManager** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a42c3-144">On the **Configure single sign-on at TimeOffManager** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="a42c3-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795916.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a42c3-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795916.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="a42c3-146">In a different web browser window, log into your TimeOffManager company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a42c3-146">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>
6. <span data-ttu-id="a42c3-147">Go to **Account \> Account Options \> Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-147">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="a42c3-148">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795917.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="a42c3-148">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="a42c3-149">In the **Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a42c3-149">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a42c3-150">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795918.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="a42c3-150">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795918.png "Single Sign-On Settings")</span></span>
  1.  <span data-ttu-id="a42c3-151">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="a42c3-151">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
   
       >[!TIP] 
       ><span data-ttu-id="a42c3-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a42c3-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
       > 
  2.  <span data-ttu-id="a42c3-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="a42c3-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  3.  <span data-ttu-id="a42c3-154">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, copy the **Issuer URL** value, and then paste it into the **Idp Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="a42c3-154">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, copy the **Issuer URL** value, and then paste it into the **Idp Issuer** textbox.</span></span>
  4.  <span data-ttu-id="a42c3-155">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP Endpoint URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a42c3-155">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP Endpoint URL** textbox.</span></span>
  5.  <span data-ttu-id="a42c3-156">As **Enforce SAML**, select **No**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-156">As **Enforce SAML**, select **No**.</span></span>
  6.  <span data-ttu-id="a42c3-157">As **Auto-Create Users**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-157">As **Auto-Create Users**, select **Yes**.</span></span>
  7.  <span data-ttu-id="a42c3-158">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox, and click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-158">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox, and click **Save Changes**.</span></span>

1. <span data-ttu-id="a42c3-159">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-159">In the Azure classic portal, on the **Configure single sign-on at TimeOffManager** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="a42c3-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795919.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a42c3-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795919.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a42c3-161">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="a42c3-161">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="a42c3-162">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795920.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="a42c3-162">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795920.png "Attributes")</span></span>
3. <span data-ttu-id="a42c3-163">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a42c3-163">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="a42c3-164">![saml token attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/123.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="a42c3-164">![saml token attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/123.png "saml token attributes")</span></span>
   
   | <span data-ttu-id="a42c3-165">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="a42c3-165">Attribute Name</span></span> | <span data-ttu-id="a42c3-166">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="a42c3-166">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="a42c3-167">Email</span><span class="sxs-lookup"><span data-stu-id="a42c3-167">Email</span></span> |<span data-ttu-id="a42c3-168">User.mail</span><span class="sxs-lookup"><span data-stu-id="a42c3-168">User.mail</span></span> |
   | <span data-ttu-id="a42c3-169">Firstname</span><span class="sxs-lookup"><span data-stu-id="a42c3-169">Firstname</span></span> |<span data-ttu-id="a42c3-170">User.givenname</span><span class="sxs-lookup"><span data-stu-id="a42c3-170">User.givenname</span></span> |
   | <span data-ttu-id="a42c3-171">Lastname</span><span class="sxs-lookup"><span data-stu-id="a42c3-171">Lastname</span></span> |<span data-ttu-id="a42c3-172">User.surname</span><span class="sxs-lookup"><span data-stu-id="a42c3-172">User.surname</span></span> |
  1.  <span data-ttu-id="a42c3-173">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-173">For each data row in the table above, click **add user attribute**.</span></span>
  2.  <span data-ttu-id="a42c3-174">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a42c3-174">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  3.  <span data-ttu-id="a42c3-175">In the **Attribute Value** textbox, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a42c3-175">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
  4.  <span data-ttu-id="a42c3-176">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-176">Click **Complete**.</span></span>
4. <span data-ttu-id="a42c3-177">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-177">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="a42c3-178">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a42c3-178">Configure user provisioning</span></span>
<span data-ttu-id="a42c3-179">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="a42c3-179">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="a42c3-180">TimeOffManager supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="a42c3-180">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="a42c3-181">There is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="a42c3-181">There is no action item for you.</span></span>  

<span data-ttu-id="a42c3-182">The users are added automatically during the first login using single sign on.</span><span class="sxs-lookup"><span data-stu-id="a42c3-182">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="a42c3-183">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a42c3-183">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision AAD user accounts.</span></span>
> 

## <a name="assign-users"></a><span data-ttu-id="a42c3-184">Assign users</span><span class="sxs-lookup"><span data-stu-id="a42c3-184">Assign users</span></span>
<span data-ttu-id="a42c3-185">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a42c3-185">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a42c3-186">**To assign users to TimeOffManager, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a42c3-186">**To assign users to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="a42c3-187">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a42c3-187">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a42c3-188">On the **TimeOffManager** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a42c3-188">On the **TimeOffManager** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a42c3-189">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795922.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="a42c3-189">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC795922.png "Assign Users")</span></span>
3. <span data-ttu-id="a42c3-190">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a42c3-190">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a42c3-191">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a42c3-191">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-timeoffmanager-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a42c3-192">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a42c3-192">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a42c3-193">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a42c3-193">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















