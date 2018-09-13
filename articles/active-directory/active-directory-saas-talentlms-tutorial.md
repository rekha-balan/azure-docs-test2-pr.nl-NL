---
title: 'Tutorial: Azure Active Directory Integration with TalentLMS | Microsoft Docs'
description: Learn how to use TalentLMS with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/07/2017
ms.author: jeedes
ms.openlocfilehash: 64d9b3b532a87ae853decf2c19c21114a74daf6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553167"
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="136ab-103">Tutorial: Azure Active Directory Integration with TalentLMS</span><span class="sxs-lookup"><span data-stu-id="136ab-103">Tutorial: Azure Active Directory Integration with TalentLMS</span></span>
<span data-ttu-id="136ab-104">The objective of this tutorial is to show the integration of Azure and TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="136ab-104">The objective of this tutorial is to show the integration of Azure and TalentLMS.</span></span>  

<span data-ttu-id="136ab-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="136ab-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="136ab-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="136ab-106">A valid Azure subscription</span></span>
* <span data-ttu-id="136ab-107">A TalentLMS tenant</span><span class="sxs-lookup"><span data-stu-id="136ab-107">A TalentLMS tenant</span></span>

<span data-ttu-id="136ab-108">After completing this tutorial, the Azure AD users you have assigned to TalentLMS will be able to single sign into the application at your TalentLMS company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="136ab-108">After completing this tutorial, the Azure AD users you have assigned to TalentLMS will be able to single sign into the application at your TalentLMS company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="136ab-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="136ab-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="136ab-110">Enabling the application integration for TalentLMS</span><span class="sxs-lookup"><span data-stu-id="136ab-110">Enabling the application integration for TalentLMS</span></span>
2. <span data-ttu-id="136ab-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="136ab-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="136ab-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="136ab-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="136ab-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="136ab-113">Assigning users</span></span>

<span data-ttu-id="136ab-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777289.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="136ab-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777289.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-talentlms"></a><span data-ttu-id="136ab-115">Enable the application integration for TalentLMS</span><span class="sxs-lookup"><span data-stu-id="136ab-115">Enable the application integration for TalentLMS</span></span>
<span data-ttu-id="136ab-116">The objective of this section is to outline how to enable the application integration for TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="136ab-116">The objective of this section is to outline how to enable the application integration for TalentLMS.</span></span>

<span data-ttu-id="136ab-117">**To enable the application integration for TalentLMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="136ab-117">**To enable the application integration for TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="136ab-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="136ab-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="136ab-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="136ab-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="136ab-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="136ab-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="136ab-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="136ab-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="136ab-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="136ab-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="136ab-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="136ab-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="136ab-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="136ab-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="136ab-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="136ab-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="136ab-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="136ab-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="136ab-127">In the **search box**, type **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="136ab-127">In the **search box**, type **TalentLMS**.</span></span>
   
    <span data-ttu-id="136ab-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777290.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="136ab-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777290.png "Application gallery")</span></span>

7. <span data-ttu-id="136ab-129">In the results pane, select **TalentLMS**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="136ab-129">In the results pane, select **TalentLMS**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="136ab-130">![TalentLMS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777291.png "TalentLMS")</span><span class="sxs-lookup"><span data-stu-id="136ab-130">![TalentLMS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777291.png "TalentLMS")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="136ab-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="136ab-131">Configure single sign-on</span></span>
<span data-ttu-id="136ab-132">The objective of this section is to outline how to enable users to authenticate to TalentLMS with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="136ab-132">The objective of this section is to outline how to enable users to authenticate to TalentLMS with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="136ab-133">Configuring SSO for TalentLMS requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="136ab-133">Configuring SSO for TalentLMS requires you to retrieve a thumbprint value from a certificate.</span></span>  

<span data-ttu-id="136ab-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="136ab-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="136ab-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="136ab-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="136ab-136">In the Azure classic portal, on the **TalentLMS** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="136ab-136">In the Azure classic portal, on the **TalentLMS** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="136ab-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777292.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="136ab-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777292.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="136ab-138">On the **How would you like users to sign on to TalentLMS** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="136ab-138">On the **How would you like users to sign on to TalentLMS** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="136ab-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777293.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="136ab-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777293.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="136ab-140">On the **Configure App URL** page, in the **TalentLMS Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.TalentLMSapp.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="136ab-140">On the **Configure App URL** page, in the **TalentLMS Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.TalentLMSapp.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="136ab-141">![Sign on URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777294.png "Sign on URL")</span><span class="sxs-lookup"><span data-stu-id="136ab-141">![Sign on URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777294.png "Sign on URL")</span></span>

4. <span data-ttu-id="136ab-142">On the **Configure single sign-on at TalentLMS** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\TalentLMS.cer**.</span><span class="sxs-lookup"><span data-stu-id="136ab-142">On the **Configure single sign-on at TalentLMS** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\TalentLMS.cer**.</span></span>
   
    <span data-ttu-id="136ab-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777295.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="136ab-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777295.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="136ab-144">In a different web browser window, log into your TalentLMS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="136ab-144">In a different web browser window, log into your TalentLMS company site as an administrator.</span></span>

6. <span data-ttu-id="136ab-145">In the **Account & Settings** section, click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="136ab-145">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="136ab-146">![Account & Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span><span class="sxs-lookup"><span data-stu-id="136ab-146">![Account & Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

7. <span data-ttu-id="136ab-147">Click **Single Sign-On (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="136ab-147">Click **Single Sign-On (SSO)**,</span></span>

8. <span data-ttu-id="136ab-148">In the Single Sign-On section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="136ab-148">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="136ab-149">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="136ab-149">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   
  1. <span data-ttu-id="136ab-150">From the **SSO integration type** list, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="136ab-150">From the **SSO integration type** list, select **SAML 2.0**.</span></span>
  2. <span data-ttu-id="136ab-151">In the Azure classic portal, on the **Configure single sign-on at TalentLMS** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity provider (IdP)** textbox.</span><span class="sxs-lookup"><span data-stu-id="136ab-151">In the Azure classic portal, on the **Configure single sign-on at TalentLMS** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity provider (IdP)** textbox.</span></span>
  3. <span data-ttu-id="136ab-152">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="136ab-152">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span></span>
      
     >[!TIP]
     ><span data-ttu-id="136ab-153">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="136ab-153">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
     >    

  4. <span data-ttu-id="136ab-154">In the Azure classic portal, on the **Configure single sign-on at TalentLMS** dialog page, copy the **Remote Login URL** value, and then paste it into the **Remote sign-in URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="136ab-154">In the Azure classic portal, on the **Configure single sign-on at TalentLMS** dialog page, copy the **Remote Login URL** value, and then paste it into the **Remote sign-in URL** textbox.</span></span> 
  5. <span data-ttu-id="136ab-155">In the Azure classic portal, on the **Configure single sign-on at TalentLMS** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote sign-out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="136ab-155">In the Azure classic portal, on the **Configure single sign-on at TalentLMS** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote sign-out URL** textbox.</span></span>
  6. <span data-ttu-id="136ab-156">Fill in the following:</span><span class="sxs-lookup"><span data-stu-id="136ab-156">Fill in the following:</span></span> 
    * <span data-ttu-id="136ab-157">In the **TargetedID** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span><span class="sxs-lookup"><span data-stu-id="136ab-157">In the **TargetedID** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span></span>
    * <span data-ttu-id="136ab-158">In the **First name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="136ab-158">In the **First name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
    * <span data-ttu-id="136ab-159">In the **Last name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="136ab-159">In the **Last name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>
    * <span data-ttu-id="136ab-160">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="136ab-160">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
  7. <span data-ttu-id="136ab-161">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="136ab-161">Click **Save**.</span></span>

9. <span data-ttu-id="136ab-162">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="136ab-162">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="136ab-163">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777298.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="136ab-163">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777298.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="136ab-164">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="136ab-164">Configure user provisioning</span></span>
<span data-ttu-id="136ab-165">In order to enable Azure AD users to log into TalentLMS, they must be provisioned into TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="136ab-165">In order to enable Azure AD users to log into TalentLMS, they must be provisioned into TalentLMS.</span></span>  

* <span data-ttu-id="136ab-166">In the case of TalentLMS, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="136ab-166">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="136ab-167">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="136ab-167">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="136ab-168">Log in to your **TalentLMS** tenant.</span><span class="sxs-lookup"><span data-stu-id="136ab-168">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="136ab-169">Click **Users**, and then click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="136ab-169">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="136ab-170">On the **Add user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="136ab-170">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="136ab-171">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="136ab-171">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>   
  1. <span data-ttu-id="136ab-172">Type the related attribute values of the Azure AD user account into the following textboxes: **First name**, **Last name**, **Email address**.</span><span class="sxs-lookup"><span data-stu-id="136ab-172">Type the related attribute values of the Azure AD user account into the following textboxes: **First name**, **Last name**, **Email address**.</span></span>
  2. <span data-ttu-id="136ab-173">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="136ab-173">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="136ab-174">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="136ab-174">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="136ab-175">Assign users</span><span class="sxs-lookup"><span data-stu-id="136ab-175">Assign users</span></span>
<span data-ttu-id="136ab-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="136ab-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="136ab-177">**To assign users to TalentLMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="136ab-177">**To assign users to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="136ab-178">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="136ab-178">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="136ab-179">On the \*\*TalentLMS \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="136ab-179">On the \*\*TalentLMS \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="136ab-180">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777300.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="136ab-180">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC777300.png "Assign users")</span></span>

3. <span data-ttu-id="136ab-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="136ab-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="136ab-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="136ab-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-talentlms-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="136ab-183">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="136ab-183">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="136ab-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="136ab-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















