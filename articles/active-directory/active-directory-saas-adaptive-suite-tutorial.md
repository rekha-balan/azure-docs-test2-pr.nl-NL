---
title: 'Tutorial: Azure Active Directory integration with Adaptive Suite | Microsoft Docs'
description: Learn how to use Adaptive Suite with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/12/2017
ms.author: jeedes
ms.openlocfilehash: b8ecda8dbb1cce5dca76e20de16228db8440961e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548879"
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="634f9-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="634f9-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>
<span data-ttu-id="634f9-104">The objective of this tutorial is to show the integration of Azure and Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="634f9-104">The objective of this tutorial is to show the integration of Azure and Adaptive Suite.</span></span>  

<span data-ttu-id="634f9-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="634f9-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="634f9-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="634f9-106">A valid Azure subscription</span></span>
* <span data-ttu-id="634f9-107">An Adaptive Suite tenant</span><span class="sxs-lookup"><span data-stu-id="634f9-107">An Adaptive Suite tenant</span></span>

<span data-ttu-id="634f9-108">After completing this tutorial, the Azure AD users you have assigned to Adaptive Suite will be able to single sign into the application at your Adaptive Suite company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="634f9-108">After completing this tutorial, the Azure AD users you have assigned to Adaptive Suite will be able to single sign into the application at your Adaptive Suite company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="634f9-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="634f9-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="634f9-110">Enabling the application integration for Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="634f9-110">Enabling the application integration for Adaptive Suite</span></span>
* <span data-ttu-id="634f9-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="634f9-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="634f9-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="634f9-112">Configuring user provisioning</span></span>
* <span data-ttu-id="634f9-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="634f9-113">Assigning users</span></span>

<span data-ttu-id="634f9-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805637.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="634f9-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805637.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-adaptive-suite"></a><span data-ttu-id="634f9-115">Enable the application integration for Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="634f9-115">Enable the application integration for Adaptive Suite</span></span>
<span data-ttu-id="634f9-116">The objective of this section is to outline how to enable the application integration for Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="634f9-116">The objective of this section is to outline how to enable the application integration for Adaptive Suite.</span></span>

<span data-ttu-id="634f9-117">**To enable the application integration for Adaptive Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="634f9-117">**To enable the application integration for Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="634f9-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="634f9-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="634f9-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="634f9-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="634f9-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="634f9-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="634f9-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="634f9-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="634f9-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="634f9-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="634f9-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="634f9-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="634f9-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="634f9-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="634f9-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="634f9-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="634f9-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="634f9-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="634f9-127">In the **search box**, type **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="634f9-127">In the **search box**, type **Adaptive Suite**.</span></span>
   
   <span data-ttu-id="634f9-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805638.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="634f9-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805638.png "Application Gallery")</span></span>
7. <span data-ttu-id="634f9-129">In the results pane, select **Adaptive Suite**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="634f9-129">In the results pane, select **Adaptive Suite**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="634f9-130">![Adaptive Suite](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805639.png "Adaptive Suite")</span><span class="sxs-lookup"><span data-stu-id="634f9-130">![Adaptive Suite](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805639.png "Adaptive Suite")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="634f9-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="634f9-131">Configure single sign-on</span></span>

<span data-ttu-id="634f9-132">The objective of this section is to outline how to enable users to authenticate to Adaptive Suite with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="634f9-132">The objective of this section is to outline how to enable users to authenticate to Adaptive Suite with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="634f9-133">Configuring single sign-on for Adaptive Suite requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="634f9-133">Configuring single sign-on for Adaptive Suite requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="634f9-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="634f9-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="634f9-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="634f9-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="634f9-136">In the Azure classic portal, on the **Adaptive Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="634f9-136">In the Azure classic portal, on the **Adaptive Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="634f9-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805640.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="634f9-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805640.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="634f9-138">On the **How would you like users to sign on to Adaptive Suite** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="634f9-138">On the **How would you like users to sign on to Adaptive Suite** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="634f9-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805641.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="634f9-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805641.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="634f9-140">On the **Configure App Settings** page, in the **Reply URL** textbox, type your URL using the following pattern "*https://login.adaptiveinsights.com:443/samlsso/RlJFRVRSSUFMMTI3MTE=*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="634f9-140">On the **Configure App Settings** page, in the **Reply URL** textbox, type your URL using the following pattern "*https://login.adaptiveinsights.com:443/samlsso/RlJFRVRSSUFMMTI3MTE=*", and then click **Next**.</span></span>
   
>[!NOTE]
> <span data-ttu-id="634f9-141">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span><span class="sxs-lookup"><span data-stu-id="634f9-141">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
>  
   
  <span data-ttu-id="634f9-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805642.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="634f9-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805642.png "Configure App Settings")</span></span>
4. <span data-ttu-id="634f9-143">On the **Configure single sign-on at Adaptive Suite** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="634f9-143">On the **Configure single sign-on at Adaptive Suite** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
  <span data-ttu-id="634f9-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805643.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="634f9-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805643.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="634f9-145">In a different web browser window, log into your Adaptive Suite company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="634f9-145">In a different web browser window, log into your Adaptive Suite company site as an administrator.</span></span>
6. <span data-ttu-id="634f9-146">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="634f9-146">Go to **Admin**.</span></span>
   
  <span data-ttu-id="634f9-147">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="634f9-147">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805644.png "Admin")</span></span>
7. <span data-ttu-id="634f9-148">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span><span class="sxs-lookup"><span data-stu-id="634f9-148">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
  <span data-ttu-id="634f9-149">![Manage SAML SSO Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805645.png "Manage SAML SSO Settings")</span><span class="sxs-lookup"><span data-stu-id="634f9-149">![Manage SAML SSO Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>
8. <span data-ttu-id="634f9-150">On the **SAML SSO Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="634f9-150">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="634f9-151">![SAML SSO Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805646.png "SAML SSO Settings")</span><span class="sxs-lookup"><span data-stu-id="634f9-151">![SAML SSO Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805646.png "SAML SSO Settings")</span></span>
   
  1. <span data-ttu-id="634f9-152">In the **Identity provider name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="634f9-152">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
  2. <span data-ttu-id="634f9-153">In the Azure classic portal, on the **Configure single sign-on at Adaptive Suite** dialog page, copy the **Entity ID** value, and then paste it into the **Identity provider Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="634f9-153">In the Azure classic portal, on the **Configure single sign-on at Adaptive Suite** dialog page, copy the **Entity ID** value, and then paste it into the **Identity provider Entity ID** textbox.</span></span>
  3. <span data-ttu-id="634f9-154">In the Azure classic portal, on the **Configure single sign-on at Adaptive Suite** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Identity provider SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="634f9-154">In the Azure classic portal, on the **Configure single sign-on at Adaptive Suite** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Identity provider SSO URL** textbox.</span></span>
  4. <span data-ttu-id="634f9-155">In the Azure classic portal, on the **Configure single sign-on at Adaptive Suite** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Custom logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="634f9-155">In the Azure classic portal, on the **Configure single sign-on at Adaptive Suite** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Custom logout URL** textbox.</span></span>
  5. <span data-ttu-id="634f9-156">To upload your downloaded certificate, click **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="634f9-156">To upload your downloaded certificate, click **Choose file**.</span></span>
  6. <span data-ttu-id="634f9-157">Select the following, for:</span><span class="sxs-lookup"><span data-stu-id="634f9-157">Select the following, for:</span></span>
    * <span data-ttu-id="634f9-158">**SAML user id**, select **User’s Adaptive Insights user name**.</span><span class="sxs-lookup"><span data-stu-id="634f9-158">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="634f9-159">**SAML user id location**, select **User id in NameID of Subject**.</span><span class="sxs-lookup"><span data-stu-id="634f9-159">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="634f9-160">**SAML NameID format**, select **Email address**.</span><span class="sxs-lookup"><span data-stu-id="634f9-160">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="634f9-161">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span><span class="sxs-lookup"><span data-stu-id="634f9-161">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
   7. <span data-ttu-id="634f9-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="634f9-162">Click **Save**.</span></span>
9. <span data-ttu-id="634f9-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="634f9-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="634f9-164">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805647.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="634f9-164">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805647.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="634f9-165">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="634f9-165">Configure user provisioning</span></span>

<span data-ttu-id="634f9-166">In order to enable Azure AD users to log into Adaptive Suite, they must be provisioned into Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="634f9-166">In order to enable Azure AD users to log into Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="634f9-167">In the case of Adaptive Suite, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="634f9-167">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="634f9-168">\*\* To configure user provisioning, perform the following steps:\*\*</span><span class="sxs-lookup"><span data-stu-id="634f9-168">\*\* To configure user provisioning, perform the following steps:\*\*</span></span> 

1. <span data-ttu-id="634f9-169">Log in to your **Adaptive Suite** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="634f9-169">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="634f9-170">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="634f9-170">Go to **Admin**.</span></span>
   
   <span data-ttu-id="634f9-171">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="634f9-171">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="634f9-172">In the **Users and Roles** section, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="634f9-172">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="634f9-173">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805648.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="634f9-173">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="634f9-174">In the **New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="634f9-174">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="634f9-175">![Submit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805649.png "Submit")</span><span class="sxs-lookup"><span data-stu-id="634f9-175">![Submit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805649.png "Submit")</span></span>   
  1. <span data-ttu-id="634f9-176">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="634f9-176">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="634f9-177">Select a **Role**.</span><span class="sxs-lookup"><span data-stu-id="634f9-177">Select a **Role**.</span></span>
  3. <span data-ttu-id="634f9-178">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="634f9-178">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="634f9-179">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="634f9-179">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="634f9-180">Assign users</span><span class="sxs-lookup"><span data-stu-id="634f9-180">Assign users</span></span>
<span data-ttu-id="634f9-181">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="634f9-181">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="634f9-182">**To assign users to Adaptive Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="634f9-182">**To assign users to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="634f9-183">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="634f9-183">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="634f9-184">On the **Adaptive Suite** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="634f9-184">On the **Adaptive Suite** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="634f9-185">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805650.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="634f9-185">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC805650.png "Assign Users")</span></span>
3. <span data-ttu-id="634f9-186">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="634f9-186">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="634f9-187">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="634f9-187">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adaptive-suite-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="634f9-188">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="634f9-188">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="634f9-189">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="634f9-189">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















