---
title: 'Tutorial: Azure Active Directory Integration with Citrix ShareFile | Microsoft Docs'
description: Learn how to use Citrix ShareFile with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 75add885cb636f4bc667de91bcd2b7015c94cbea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563450"
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="2117c-103">Tutorial: Azure Active Directory Integration with Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="2117c-103">Tutorial: Azure Active Directory Integration with Citrix ShareFile</span></span>
<span data-ttu-id="2117c-104">The objective of this tutorial is to show the integration of Azure and Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="2117c-104">The objective of this tutorial is to show the integration of Azure and Citrix ShareFile.</span></span>  

<span data-ttu-id="2117c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="2117c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2117c-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="2117c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2117c-107">A Citrix ShareFile tenant</span><span class="sxs-lookup"><span data-stu-id="2117c-107">A Citrix ShareFile tenant</span></span>

<span data-ttu-id="2117c-108">After completing this tutorial, the Azure AD users you have assigned to Citrix ShareFile will be able to single sign into the application at your Citrix ShareFile company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2117c-108">After completing this tutorial, the Azure AD users you have assigned to Citrix ShareFile will be able to single sign into the application at your Citrix ShareFile company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="2117c-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2117c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="2117c-110">Enabling the application integration for Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="2117c-110">Enabling the application integration for Citrix ShareFile</span></span>
* <span data-ttu-id="2117c-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="2117c-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="2117c-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="2117c-112">Configuring user provisioning</span></span>
* <span data-ttu-id="2117c-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="2117c-113">Assigning users</span></span>

<span data-ttu-id="2117c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773620.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="2117c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773620.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-citrix-sharefile"></a><span data-ttu-id="2117c-115">Enable the application integration for Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="2117c-115">Enable the application integration for Citrix ShareFile</span></span>
<span data-ttu-id="2117c-116">The objective of this section is to outline how to enable the application integration for Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="2117c-116">The objective of this section is to outline how to enable the application integration for Citrix ShareFile.</span></span>

<span data-ttu-id="2117c-117">**To enable the application integration for Citrix ShareFile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2117c-117">**To enable the application integration for Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="2117c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2117c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
<span data-ttu-id="2117c-119">=   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2117c-119">=   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2117c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2117c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2117c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2117c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2117c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="2117c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2117c-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2117c-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="2117c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="2117c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2117c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="2117c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="2117c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="2117c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2117c-127">In the **search box**, type **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="2117c-127">In the **search box**, type **Citrix ShareFile**.</span></span>
   
   <span data-ttu-id="2117c-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773621.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="2117c-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773621.png "Application gallery")</span></span>
7. <span data-ttu-id="2117c-129">In the results pane, select **Citrix ShareFile**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="2117c-129">In the results pane, select **Citrix ShareFile**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2117c-130">![Citrix ShareFile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773622.png "Citrix ShareFile")</span><span class="sxs-lookup"><span data-stu-id="2117c-130">![Citrix ShareFile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773622.png "Citrix ShareFile")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2117c-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="2117c-131">Configure single sign-on</span></span>

<span data-ttu-id="2117c-132">The objective of this section is to outline how to enable users to authenticate to Citrix ShareFile with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="2117c-132">The objective of this section is to outline how to enable users to authenticate to Citrix ShareFile with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="2117c-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2117c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2117c-134">In the Azure classic portal, on the **Citrix ShareFile** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="2117c-134">In the Azure classic portal, on the **Citrix ShareFile** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="2117c-135">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773623.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2117c-135">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773623.png "Enable single sign-on")</span></span>
2. <span data-ttu-id="2117c-136">On the **How would you like users to sign on to Citrix ShareFile** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2117c-136">On the **How would you like users to sign on to Citrix ShareFile** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2117c-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773624.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2117c-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773624.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="2117c-138">On the **Configure App URL** page, in the **Citrix ShareFile Sign On URL** textbox, type your URL using the following pattern `https://<tenant-name>.shareFile.com`, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2117c-138">On the **Configure App URL** page, in the **Citrix ShareFile Sign On URL** textbox, type your URL using the following pattern `https://<tenant-name>.shareFile.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="2117c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773625.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="2117c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773625.png "Configure App URL")</span></span>
4. <span data-ttu-id="2117c-140">On the **Configure single sign-on at Citrix ShareFile** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2117c-140">On the **Configure single sign-on at Citrix ShareFile** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="2117c-141">![ConfigureSingle Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773626.png "ConfigureSingle Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2117c-141">![ConfigureSingle Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773626.png "ConfigureSingle Sign-On")</span></span>
5. <span data-ttu-id="2117c-142">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2117c-142">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>
6. <span data-ttu-id="2117c-143">In the toolbar on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2117c-143">In the toolbar on the top, click **Admin**.</span></span>
7. <span data-ttu-id="2117c-144">In the left navigation pane, select **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2117c-144">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
   <span data-ttu-id="2117c-145">![Account Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773627.png "Account Administration")</span><span class="sxs-lookup"><span data-stu-id="2117c-145">![Account Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773627.png "Account Administration")</span></span>
8. <span data-ttu-id="2117c-146">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2117c-146">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
   <span data-ttu-id="2117c-147">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773628.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2117c-147">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773628.png "Single sign-on")</span></span>
   1. <span data-ttu-id="2117c-148">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="2117c-148">Click **Enable SAML**.</span></span>
   2. <span data-ttu-id="2117c-149">In the Azure classic portal, on the **Configure single sign-on at Citrix ShareFile** dialog page, copy the **Entity ID** value, and then paste it into the **Your IDP Issuer/ Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="2117c-149">In the Azure classic portal, on the **Configure single sign-on at Citrix ShareFile** dialog page, copy the **Entity ID** value, and then paste it into the **Your IDP Issuer/ Entity ID** textbox.</span></span>
   3. <span data-ttu-id="2117c-150">In the Azure classic portal, on the **Configure single sign-on at Citrix ShareFile** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2117c-150">In the Azure classic portal, on the **Configure single sign-on at Citrix ShareFile** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   4. <span data-ttu-id="2117c-151">In the Azure classic portal, on **the Configure single sign-on at Citrix ShareFile** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2117c-151">In the Azure classic portal, on **the Configure single sign-on at Citrix ShareFile** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
   5. <span data-ttu-id="2117c-152">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure AD classic portal.</span><span class="sxs-lookup"><span data-stu-id="2117c-152">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure AD classic portal.</span></span> 
   
      <span data-ttu-id="2117c-153">![Basic Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773629.png "Basic Settings")</span><span class="sxs-lookup"><span data-stu-id="2117c-153">![Basic Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773629.png "Basic Settings")</span></span>
9. <span data-ttu-id="2117c-154">Click **Save** on the Citrix ShareFile management portal.</span><span class="sxs-lookup"><span data-stu-id="2117c-154">Click **Save** on the Citrix ShareFile management portal.</span></span>
10. <span data-ttu-id="2117c-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="2117c-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="2117c-156">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773630.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2117c-156">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773630.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="2117c-157">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="2117c-157">Configure user provisioning</span></span>

<span data-ttu-id="2117c-158">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="2117c-158">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span>  

* <span data-ttu-id="2117c-159">In the case of Citrix ShareFile, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="2117c-159">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="2117c-160">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2117c-160">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="2117c-161">Log in to your **Citrix ShareFile** tenant.</span><span class="sxs-lookup"><span data-stu-id="2117c-161">Log in to your **Citrix ShareFile** tenant.</span></span>
2. <span data-ttu-id="2117c-162">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span><span class="sxs-lookup"><span data-stu-id="2117c-162">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="2117c-163">![Create Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC781050.png "Create Employee")</span><span class="sxs-lookup"><span data-stu-id="2117c-163">![Create Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC781050.png "Create Employee")</span></span>
3. <span data-ttu-id="2117c-164">Enter the **Email**, **First name** and **Last name** of a valid Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="2117c-164">Enter the **Email**, **First name** and **Last name** of a valid Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="2117c-165">![Basic Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC799951.png "Basic Information")</span><span class="sxs-lookup"><span data-stu-id="2117c-165">![Basic Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
4. <span data-ttu-id="2117c-166">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2117c-166">Click **Add User**.</span></span>
   >[!NOTE]
   ><span data-ttu-id="2117c-167">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="2117c-167">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="2117c-168">You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="2117c-168">You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="2117c-169">Assign users</span><span class="sxs-lookup"><span data-stu-id="2117c-169">Assign users</span></span>
<span data-ttu-id="2117c-170">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="2117c-170">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2117c-171">**To assign users to Citrix ShareFile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2117c-171">**To assign users to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="2117c-172">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="2117c-172">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2117c-173">On the **Citrix ShareFile** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="2117c-173">On the **Citrix ShareFile** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2117c-174">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773631.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="2117c-174">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773631.png "Assign users")</span></span>
3. <span data-ttu-id="2117c-175">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="2117c-175">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2117c-176">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="2117c-176">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2117c-177">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2117c-177">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2117c-178">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2117c-178">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















