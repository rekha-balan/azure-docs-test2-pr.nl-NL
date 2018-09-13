---
title: 'Tutorial: Azure Active Directory integration with Replicon | Microsoft Docs'
description: Learn how to use Replicon with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: a5d8c9e75f33a735a6300dfe94ecefcc5423bcd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553161"
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="c8e6b-103">Tutorial: Azure Active Directory integration with Replicon</span><span class="sxs-lookup"><span data-stu-id="c8e6b-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="c8e6b-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="c8e6b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c8e6b-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c8e6b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c8e6b-107">A Replicon tenant</span><span class="sxs-lookup"><span data-stu-id="c8e6b-107">A Replicon tenant</span></span>

<span data-ttu-id="c8e6b-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c8e6b-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="c8e6b-110">Enabling the application integration for Replicon</span><span class="sxs-lookup"><span data-stu-id="c8e6b-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="c8e6b-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="c8e6b-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="c8e6b-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="c8e6b-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="c8e6b-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="c8e6b-113">Assigning users</span></span>

<span data-ttu-id="c8e6b-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="c8e6b-115">Enable the application integration for Replicon</span><span class="sxs-lookup"><span data-stu-id="c8e6b-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="c8e6b-116">The objective of this section is to outline how to enable the application integration for Replicon.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="c8e6b-117">**To enable the application integration for Replicon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8e6b-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e6b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="c8e6b-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c8e6b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c8e6b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="c8e6b-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c8e6b-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="c8e6b-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c8e6b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="c8e6b-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c8e6b-127">In the **search box**, type **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="c8e6b-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="c8e6b-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="c8e6b-130">![Replicon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-130">![Replicon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c8e6b-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="c8e6b-131">Configure single sign-on</span></span>

<span data-ttu-id="c8e6b-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="c8e6b-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8e6b-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e6b-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="c8e6b-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="c8e6b-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="c8e6b-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="c8e6b-138">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="c8e6b-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="c8e6b-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="c8e6b-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="c8e6b-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="c8e6b-143">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-143">Click **Next**.</span></span>

4. <span data-ttu-id="c8e6b-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="c8e6b-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="c8e6b-146">In a different web browser window, log into your Replicon company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="c8e6b-147">To configure SAML 2.0, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="c8e6b-148">![Enable SAML authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-148">![Enable SAML authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="c8e6b-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="c8e6b-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="c8e6b-150">The following shows the schema of the complete URL:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-150">The following shows the schema of the complete URL:</span></span>  
   **https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. <span data-ttu-id="c8e6b-151">Click the **+** to expand the **v20Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-151">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="c8e6b-152">Click the **+** to expand the **metaDataConfiguration** section.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-152">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="c8e6b-153">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-153">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="c8e6b-154">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-154">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="c8e6b-155">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-155">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c8e6b-156">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="c8e6b-156">Configure user provisioning</span></span>

<span data-ttu-id="c8e6b-157">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-157">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="c8e6b-158">In the case of Replicon, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-158">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="c8e6b-159">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8e6b-159">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e6b-160">In a web browser window, log into your Replicon company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-160">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="c8e6b-161">Go to **Administration \> Users**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-161">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="c8e6b-162">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-162">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="c8e6b-163">Click **+Add User**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-163">Click **+Add User**.</span></span>
   
    <span data-ttu-id="c8e6b-164">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-164">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="c8e6b-165">In the **User Profile** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-165">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c8e6b-166">![User profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-166">![User profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="c8e6b-167">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-167">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="c8e6b-168">As **Authentication Type**, select **SSO**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-168">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="c8e6b-169">In the **Department** textbox, type the user’s department.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-169">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="c8e6b-170">As **Employee Type**, select **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-170">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="c8e6b-171">Click **Save User Profile**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-171">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="c8e6b-172">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-172">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="c8e6b-173">Assign users</span><span class="sxs-lookup"><span data-stu-id="c8e6b-173">Assign users</span></span>
<span data-ttu-id="c8e6b-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c8e6b-175">**To assign users to Replicon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8e6b-175">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e6b-176">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-176">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="c8e6b-177">On the **Replicon** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-177">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="c8e6b-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="c8e6b-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="c8e6b-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="c8e6b-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c8e6b-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c8e6b-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















