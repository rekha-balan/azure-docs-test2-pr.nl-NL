---
title: 'Tutorial: Azure Active Directory integration with Sprinklr | Microsoft Docs'
description: Learn how to use Sprinklr with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: b797adc1a08daca289cf2037ebaf7aa36aef056b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564327"
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="a63db-103">Tutorial: Azure Active Directory integration with Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a63db-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>
<span data-ttu-id="a63db-104">The objective of this tutorial is to show the integration of Azure and Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a63db-104">The objective of this tutorial is to show the integration of Azure and Sprinklr.</span></span>  
<span data-ttu-id="a63db-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a63db-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a63db-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a63db-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a63db-107">A Sprinklr tenant</span><span class="sxs-lookup"><span data-stu-id="a63db-107">A Sprinklr tenant</span></span>

<span data-ttu-id="a63db-108">After completing this tutorial, the Azure AD users you have assigned to Sprinklr will be able to single sign into the application at your Sprinklr company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a63db-108">After completing this tutorial, the Azure AD users you have assigned to Sprinklr will be able to single sign into the application at your Sprinklr company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a63db-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a63db-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="a63db-110">Enabling the application integration for Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a63db-110">Enabling the application integration for Sprinklr</span></span>
2. <span data-ttu-id="a63db-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="a63db-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="a63db-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a63db-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="a63db-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a63db-113">Assigning users</span></span>

<span data-ttu-id="a63db-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782900.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a63db-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782900.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-sprinklr"></a><span data-ttu-id="a63db-115">Enable the application integration for Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a63db-115">Enable the application integration for Sprinklr</span></span>
<span data-ttu-id="a63db-116">The objective of this section is to outline how to enable the application integration for Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a63db-116">The objective of this section is to outline how to enable the application integration for Sprinklr.</span></span>

<span data-ttu-id="a63db-117">**To enable the application integration for Sprinklr, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a63db-117">**To enable the application integration for Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="a63db-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a63db-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="a63db-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a63db-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="a63db-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a63db-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="a63db-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a63db-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="a63db-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a63db-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="a63db-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a63db-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="a63db-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a63db-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="a63db-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a63db-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="a63db-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a63db-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="a63db-127">In the **search box**, type **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a63db-127">In the **search box**, type **Sprinklr**.</span></span>
   
    <span data-ttu-id="a63db-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782901.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a63db-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782901.png "Application Gallery")</span></span>

7. <span data-ttu-id="a63db-129">In the results pane, select **Sprinklr**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a63db-129">In the results pane, select **Sprinklr**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="a63db-130">![Sprinklr](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782902.png "Sprinklr")</span><span class="sxs-lookup"><span data-stu-id="a63db-130">![Sprinklr](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782902.png "Sprinklr")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="a63db-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a63db-131">Configure single sign-on</span></span>
<span data-ttu-id="a63db-132">The objective of this section is to outline how to enable users to authenticate to Sprinklr with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a63db-132">The objective of this section is to outline how to enable users to authenticate to Sprinklr with their account in Azure AD using federation based on the SAML protocol.</span></span> 


<span data-ttu-id="a63db-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="a63db-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  

<span data-ttu-id="a63db-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a63db-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="a63db-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a63db-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a63db-136">In the Azure classic portal, on the **Sprinklr** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a63db-136">In the Azure classic portal, on the **Sprinklr** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="a63db-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782903.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a63db-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782903.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="a63db-138">On the **How would you like users to sign on to Sprinklr** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a63db-138">On the **How would you like users to sign on to Sprinklr** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="a63db-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782904.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a63db-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782904.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="a63db-140">On the **Configure App URL** page, in the **Sprinklr Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.sprinklr.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a63db-140">On the **Configure App URL** page, in the **Sprinklr Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.sprinklr.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="a63db-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782905.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a63db-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782905.png "Configure App URL")</span></span>

4. <span data-ttu-id="a63db-142">On the **Configure single sign-on at Sprinklr** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a63db-142">On the **Configure single sign-on at Sprinklr** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="a63db-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782906.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a63db-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782906.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="a63db-144">In a different web browser window, log into your Sprinklr company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a63db-144">In a different web browser window, log into your Sprinklr company site as an administrator.</span></span>

6. <span data-ttu-id="a63db-145">Go to **Administration \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="a63db-145">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a63db-146">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="a63db-146">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782907.png "Administration")</span></span>

7. <span data-ttu-id="a63db-147">Go to **Manage Partner \> Single Sign** on from the left pane.</span><span class="sxs-lookup"><span data-stu-id="a63db-147">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="a63db-148">![Manage Partner](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782908.png "Manage Partner")</span><span class="sxs-lookup"><span data-stu-id="a63db-148">![Manage Partner](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782908.png "Manage Partner")</span></span>

8. <span data-ttu-id="a63db-149">Click **+Add Single Sign Ons**.</span><span class="sxs-lookup"><span data-stu-id="a63db-149">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="a63db-150">![Single Sign-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782909.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="a63db-150">![Single Sign-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782909.png "Single Sign-Ons")</span></span>

9. <span data-ttu-id="a63db-151">On the **Single Sign on** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a63db-151">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="a63db-152">![Single Sign-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782910.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="a63db-152">![Single Sign-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782910.png "Single Sign-Ons")</span></span>
  1. <span data-ttu-id="a63db-153">In the **Name** textbox, type a name for your configuration (e.g.: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="a63db-153">In the **Name** textbox, type a name for your configuration (e.g.: *WAADSSOTest*).</span></span>
  2. <span data-ttu-id="a63db-154">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="a63db-154">Select **Enabled**.</span></span>
  3. <span data-ttu-id="a63db-155">Select **Use new SSO Certificate**.</span><span class="sxs-lookup"><span data-stu-id="a63db-155">Select **Use new SSO Certificate**.</span></span>
  4. <span data-ttu-id="a63db-156">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="a63db-156">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
  
     >[!TIP]
     ><span data-ttu-id="a63db-157">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a63db-157">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
     >    
     
  5. <span data-ttu-id="a63db-158">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="a63db-158">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>
  6. <span data-ttu-id="a63db-159">In the Azure classic portal, in the **Configure SSO at Sprinklr** dialog:</span><span class="sxs-lookup"><span data-stu-id="a63db-159">In the Azure classic portal, in the **Configure SSO at Sprinklr** dialog:</span></span>
     *  <span data-ttu-id="a63db-160">Copy the **Identity Provider ID** value, and then paste it into the **Entity Id** textbox.</span><span class="sxs-lookup"><span data-stu-id="a63db-160">Copy the **Identity Provider ID** value, and then paste it into the **Entity Id** textbox.</span></span>
     * <span data-ttu-id="a63db-161">Copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a63db-161">Copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span>
     * <span data-ttu-id="a63db-162">Copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a63db-162">Copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span></span>
  7. <span data-ttu-id="a63db-163">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span><span class="sxs-lookup"><span data-stu-id="a63db-163">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>
  8. <span data-ttu-id="a63db-164">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="a63db-164">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>
  9. <span data-ttu-id="a63db-165">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a63db-165">Click **Save**.</span></span>
       
    <span data-ttu-id="a63db-166">![SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="a63db-166">![SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782911.png "SAML")</span></span>
10. <span data-ttu-id="a63db-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a63db-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="a63db-168">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782912.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a63db-168">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782912.png "Configure single sign-on")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="a63db-169">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a63db-169">Configure user provisioning</span></span>
<span data-ttu-id="a63db-170">For AAD users to be able to sign in, they must be provisioned for access inside the Sprinklr application.</span><span class="sxs-lookup"><span data-stu-id="a63db-170">For AAD users to be able to sign in, they must be provisioned for access inside the Sprinklr application.</span></span>  
<span data-ttu-id="a63db-171">This section describes how to create AAD user accounts inside Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a63db-171">This section describes how to create AAD user accounts inside Sprinklr.</span></span>

### <a name="to-provision-a-user-account-in-sprinklr-perform-the-following-steps"></a><span data-ttu-id="a63db-172">To provision a user account in Sprinklr, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a63db-172">To provision a user account in Sprinklr, perform the following steps:</span></span>
1. <span data-ttu-id="a63db-173">Log into your Sprinklr company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a63db-173">Log into your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="a63db-174">Go to **Administration \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="a63db-174">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a63db-175">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="a63db-175">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782907.png "Administration")</span></span>

3. <span data-ttu-id="a63db-176">Go to **Manage Client \> Users** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="a63db-176">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="a63db-177">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782914.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="a63db-177">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782914.png "Settings")</span></span>

4. <span data-ttu-id="a63db-178">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="a63db-178">Click **Add User**.</span></span>
   
    <span data-ttu-id="a63db-179">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782915.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="a63db-179">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782915.png "Settings")</span></span>

5. <span data-ttu-id="a63db-180">On the **Edit user** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a63db-180">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="a63db-181">![Edit user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782916.png "Edit user")</span><span class="sxs-lookup"><span data-stu-id="a63db-181">![Edit user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782916.png "Edit user")</span></span> 
  1. <span data-ttu-id="a63db-182">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="a63db-182">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>
  2. <span data-ttu-id="a63db-183">Select **Password Disabled**.</span><span class="sxs-lookup"><span data-stu-id="a63db-183">Select **Password Disabled**.</span></span>
  3. <span data-ttu-id="a63db-184">Select a **Language**.</span><span class="sxs-lookup"><span data-stu-id="a63db-184">Select a **Language**.</span></span>
  4. <span data-ttu-id="a63db-185">Select a **User Type**.</span><span class="sxs-lookup"><span data-stu-id="a63db-185">Select a **User Type**.</span></span>
  5. <span data-ttu-id="a63db-186">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="a63db-186">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="a63db-187">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span><span class="sxs-lookup"><span data-stu-id="a63db-187">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     > 

6. <span data-ttu-id="a63db-188">Go to **Role**, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a63db-188">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="a63db-189">![Partner Roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782917.png "Partner Roles")</span><span class="sxs-lookup"><span data-stu-id="a63db-189">![Partner Roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782917.png "Partner Roles")</span></span>
 1. <span data-ttu-id="a63db-190">From the **Global** list, select **ALL\_Permissions**.</span><span class="sxs-lookup"><span data-stu-id="a63db-190">From the **Global** list, select **ALL\_Permissions**.</span></span>  
 2. <span data-ttu-id="a63db-191">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="a63db-191">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="a63db-192">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a63db-192">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="a63db-193">Assign users</span><span class="sxs-lookup"><span data-stu-id="a63db-193">Assign users</span></span>
<span data-ttu-id="a63db-194">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a63db-194">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a63db-195">**To assign users to Sprinklr, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a63db-195">**To assign users to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="a63db-196">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a63db-196">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="a63db-197">On the \*\*Sprinklr \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a63db-197">On the \*\*Sprinklr \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="a63db-198">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782918.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="a63db-198">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC782918.png "Assign users")</span></span>

3. <span data-ttu-id="a63db-199">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a63db-199">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="a63db-200">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a63db-200">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sprinklr-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a63db-201">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a63db-201">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="a63db-202">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a63db-202">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

























