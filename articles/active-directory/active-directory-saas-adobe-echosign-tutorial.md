---
title: 'Tutorial: Azure Active Directory integration with Adobe EchoSign | Microsoft Docs'
description: Learn how to use Adobe EchoSign with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: 81c62288ced69e4d719675b4259695a622a7e694
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549786"
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-echosign"></a><span data-ttu-id="d9d52-103">Tutorial: Azure Active Directory integration with Adobe EchoSign</span><span class="sxs-lookup"><span data-stu-id="d9d52-103">Tutorial: Azure Active Directory integration with Adobe EchoSign</span></span>
<span data-ttu-id="d9d52-104">The objective of this tutorial is to show the integration of Azure and Adobe EchoSign.</span><span class="sxs-lookup"><span data-stu-id="d9d52-104">The objective of this tutorial is to show the integration of Azure and Adobe EchoSign.</span></span>  

<span data-ttu-id="d9d52-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="d9d52-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d9d52-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d9d52-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d9d52-107">An Adobe EchoSign single sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d9d52-107">An Adobe EchoSign single sign on (SSO) enabled subscription</span></span>

<span data-ttu-id="d9d52-108">After completing this tutorial, the Azure AD users you have assigned to Adobe EchoSign will be able to single sign into the application at your Adobe EchoSign company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9d52-108">After completing this tutorial, the Azure AD users you have assigned to Adobe EchoSign will be able to single sign into the application at your Adobe EchoSign company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d9d52-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d9d52-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d9d52-110">Enabling the application integration for Adobe EchoSign</span><span class="sxs-lookup"><span data-stu-id="d9d52-110">Enabling the application integration for Adobe EchoSign</span></span>
2. <span data-ttu-id="d9d52-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="d9d52-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d9d52-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="d9d52-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d9d52-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="d9d52-113">Assigning users</span></span>

<span data-ttu-id="d9d52-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789511.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="d9d52-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789511.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-adobe-echosign"></a><span data-ttu-id="d9d52-115">Enable the application integration for Adobe EchoSign</span><span class="sxs-lookup"><span data-stu-id="d9d52-115">Enable the application integration for Adobe EchoSign</span></span>
<span data-ttu-id="d9d52-116">The objective of this section is to outline how to enable the application integration for Adobe EchoSign.</span><span class="sxs-lookup"><span data-stu-id="d9d52-116">The objective of this section is to outline how to enable the application integration for Adobe EchoSign.</span></span>

<span data-ttu-id="d9d52-117">**To enable the application integration for Adobe EchoSign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d9d52-117">**To enable the application integration for Adobe EchoSign, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d52-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d9d52-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d9d52-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d9d52-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d9d52-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d9d52-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d9d52-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="d9d52-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="d9d52-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d9d52-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d9d52-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="d9d52-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="d9d52-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d9d52-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="d9d52-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="d9d52-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d9d52-127">In the **search box**, type **Adobe EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-127">In the **search box**, type **Adobe EchoSign**.</span></span>
   
   <span data-ttu-id="d9d52-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789514.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="d9d52-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789514.png "Application Gallery")</span></span>
7. <span data-ttu-id="d9d52-129">In the results pane, select **Adobe EchoSign**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d9d52-129">In the results pane, select **Adobe EchoSign**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="d9d52-130">![Adobe EchoSign](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789515.png "Adobe EchoSign")</span><span class="sxs-lookup"><span data-stu-id="d9d52-130">![Adobe EchoSign](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789515.png "Adobe EchoSign")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d9d52-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="d9d52-131">Configure single sign-on</span></span>

<span data-ttu-id="d9d52-132">The objective of this section is to outline how to enable users to authenticate to Adobe EchoSign with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="d9d52-132">The objective of this section is to outline how to enable users to authenticate to Adobe EchoSign with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="d9d52-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="d9d52-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="d9d52-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="d9d52-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="d9d52-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d9d52-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="d9d52-136">In the Azure classic portal, on the **Adobe EchoSign** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="d9d52-136">In the Azure classic portal, on the **Adobe EchoSign** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d9d52-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789516.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d9d52-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789516.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="d9d52-138">On the **How would you like users to sign on to Adobe EchoSign** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-138">On the **How would you like users to sign on to Adobe EchoSign** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d9d52-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789517.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d9d52-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789517.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="d9d52-140">On the **Configure App URL** page, in the **Adobe EchoSign Sign On URL** textbox, type your URL using the following pattern "*https://company.echosign.com/*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-140">On the **Configure App URL** page, in the **Adobe EchoSign Sign On URL** textbox, type your URL using the following pattern "*https://company.echosign.com/*", and then click **Next**.</span></span>
   
   <span data-ttu-id="d9d52-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789518.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="d9d52-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789518.png "Configure App URL")</span></span>
4. <span data-ttu-id="d9d52-142">On the **Configure single sign-on at Adobe EchoSign** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d9d52-142">On the **Configure single sign-on at Adobe EchoSign** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="d9d52-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789519.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d9d52-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789519.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="d9d52-144">In a different web browser window, log into your Adobe EchoSign company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d9d52-144">In a different web browser window, log into your Adobe EchoSign company site as an administrator.</span></span>
6. <span data-ttu-id="d9d52-145">In the menu on the top, click **Account**, and then, in the navigation pane on the left die, click **SAML Settings** under **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-145">In the menu on the top, click **Account**, and then, in the navigation pane on the left die, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="d9d52-146">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789520.png "Account")</span><span class="sxs-lookup"><span data-stu-id="d9d52-146">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789520.png "Account")</span></span>
7. <span data-ttu-id="d9d52-147">In the SAML Settings section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d9d52-147">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="d9d52-148">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789521.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="d9d52-148">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789521.png "SAML Settings")</span></span>
   
   1. <span data-ttu-id="d9d52-149">As **SAML Mode**, select **SAML Mandatory**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-149">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   2. <span data-ttu-id="d9d52-150">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-150">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   3. <span data-ttu-id="d9d52-151">As **User Creation**, select **Automatically add users authenticated through SAML**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-151">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>
8. <span data-ttu-id="d9d52-152">Move on, performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="d9d52-152">Move on, performing the following steps:</span></span>
   
   <span data-ttu-id="d9d52-153">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789522.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="d9d52-153">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789522.png "SAML Settings")</span></span>
   
   1. <span data-ttu-id="d9d52-154">In the Azure classic portal, on the **Configure single sign-on at Adobe EchoSign** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="d9d52-154">In the Azure classic portal, on the **Configure single sign-on at Adobe EchoSign** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox.</span></span>
   2. <span data-ttu-id="d9d52-155">In the Azure classic portal, on the **Configure single sign-on at Adobe EchoSign** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d9d52-155">In the Azure classic portal, on the **Configure single sign-on at Adobe EchoSign** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP Login URL** textbox.</span></span>
   3. <span data-ttu-id="d9d52-156">In the Azure classic portal, on the **Configure single sign-on at Adobe EchoSign** dialog page, copy the **Remote Logout URL** value, and then paste it into the **IdP Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d9d52-156">In the Azure classic portal, on the **Configure single sign-on at Adobe EchoSign** dialog page, copy the **Remote Logout URL** value, and then paste it into the **IdP Logout URL** textbox.</span></span>
   4. <span data-ttu-id="d9d52-157">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="d9d52-157">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
      >[!TIP]
      ><span data-ttu-id="d9d52-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="d9d52-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
      >  
   5. <span data-ttu-id="d9d52-159">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="d9d52-159">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>
   6. <span data-ttu-id="d9d52-160">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-160">Click **Save Changes**.</span></span>
9. <span data-ttu-id="d9d52-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="d9d52-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d9d52-162">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789523.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d9d52-162">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789523.png "Configure Single Sign-On")</span></span>
   
   ## <a name="configure-user-provisioning"></a><span data-ttu-id="d9d52-163">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="d9d52-163">Configure user provisioning</span></span>

<span data-ttu-id="d9d52-164">In order to enable Azure AD users to log into Adobe EchoSign, they must be provisioned into Adobe EchoSign.</span><span class="sxs-lookup"><span data-stu-id="d9d52-164">In order to enable Azure AD users to log into Adobe EchoSign, they must be provisioned into Adobe EchoSign.</span></span>  

* <span data-ttu-id="d9d52-165">In the case of Adobe EchoSign, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="d9d52-165">In the case of Adobe EchoSign, provisioning is a manual task.</span></span>

<span data-ttu-id="d9d52-166">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d9d52-166">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d52-167">Log in to your **Adobe EchoSign** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="d9d52-167">Log in to your **Adobe EchoSign** company site as administrator.</span></span>
2. <span data-ttu-id="d9d52-168">In the menu on the top, click **Account**, and then, in the navigation pane on the left die, click **Users & Groups**, and then, click **Create a new user**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-168">In the menu on the top, click **Account**, and then, in the navigation pane on the left die, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="d9d52-169">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789524.png "Account")</span><span class="sxs-lookup"><span data-stu-id="d9d52-169">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789524.png "Account")</span></span>
3. <span data-ttu-id="d9d52-170">In the **Create New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d9d52-170">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="d9d52-171">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789525.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="d9d52-171">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789525.png "Create User")</span></span>
   
   1. <span data-ttu-id="d9d52-172">Type the **Email Address**, **First Name** and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="d9d52-172">Type the **Email Address**, **First Name** and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="d9d52-173">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-173">Click **Create User**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="d9d52-174">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="d9d52-174">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span> 
      > 

>[!NOTE]
><span data-ttu-id="d9d52-175">You can use any other Adobe EchoSign user account creation tools or APIs provided by Adobe EchoSign to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="d9d52-175">You can use any other Adobe EchoSign user account creation tools or APIs provided by Adobe EchoSign to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="d9d52-176">Assign users</span><span class="sxs-lookup"><span data-stu-id="d9d52-176">Assign users</span></span>
<span data-ttu-id="d9d52-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="d9d52-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="d9d52-178">**To assign users to Adobe EchoSign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d9d52-178">**To assign users to Adobe EchoSign, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d52-179">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="d9d52-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d9d52-180">On the **Adobe EchoSign** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="d9d52-180">On the **Adobe EchoSign** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d9d52-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789526.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="d9d52-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC789526.png "Assign Users")</span></span>
3. <span data-ttu-id="d9d52-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="d9d52-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="d9d52-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="d9d52-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-echosign-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d9d52-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d9d52-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d9d52-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9d52-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















