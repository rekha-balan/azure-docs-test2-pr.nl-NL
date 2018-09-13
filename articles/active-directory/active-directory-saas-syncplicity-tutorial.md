---
title: 'Tutorial: Azure Active Directory integration with Syncplicity | Microsoft Docs'
description: Learn how to use Syncplicity with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9a422466bc9edc37e8650b49b30a5e3f7a034d2e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540801"
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="73b65-103">Tutorial: Azure Active Directory integration with Syncplicity</span><span class="sxs-lookup"><span data-stu-id="73b65-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>
<span data-ttu-id="73b65-104">The objective of this tutorial is to show how to set up single sign-on between Azure Active Directory (Azure AD) and Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="73b65-104">The objective of this tutorial is to show how to set up single sign-on between Azure Active Directory (Azure AD) and Syncplicity.</span></span>

<span data-ttu-id="73b65-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="73b65-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="73b65-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="73b65-106">A valid Azure subscription</span></span>
* <span data-ttu-id="73b65-107">A Syncplicity tenant</span><span class="sxs-lookup"><span data-stu-id="73b65-107">A Syncplicity tenant</span></span>

<span data-ttu-id="73b65-108">After completing this tutorial, the Azure AD users to whom you have assign Syncplicity access will be able to single sign into the application at your Syncplicity company site (service provider initiated sign on), or using the Azure AD Access Panel.</span><span class="sxs-lookup"><span data-stu-id="73b65-108">After completing this tutorial, the Azure AD users to whom you have assign Syncplicity access will be able to single sign into the application at your Syncplicity company site (service provider initiated sign on), or using the Azure AD Access Panel.</span></span>

1. <span data-ttu-id="73b65-109">Enabling the application integration for Syncplicity</span><span class="sxs-lookup"><span data-stu-id="73b65-109">Enabling the application integration for Syncplicity</span></span>
2. <span data-ttu-id="73b65-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="73b65-110">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="73b65-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="73b65-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="73b65-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="73b65-112">Assigning users</span></span>

<span data-ttu-id="73b65-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769524.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="73b65-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769524.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-syncplicity"></a><span data-ttu-id="73b65-114">Enable the application integration for Syncplicity</span><span class="sxs-lookup"><span data-stu-id="73b65-114">Enable the application integration for Syncplicity</span></span>
<span data-ttu-id="73b65-115">The objective of this section is to outline how to enable the application integration for Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="73b65-115">The objective of this section is to outline how to enable the application integration for Syncplicity.</span></span>

<span data-ttu-id="73b65-116">**To enable the application integration for Syncplicity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73b65-116">**To enable the application integration for Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="73b65-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73b65-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="73b65-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="73b65-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="73b65-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="73b65-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="73b65-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="73b65-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="73b65-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="73b65-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="73b65-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="73b65-122">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="73b65-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="73b65-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="73b65-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="73b65-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="73b65-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="73b65-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="73b65-126">In the **search box**, type **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="73b65-126">In the **search box**, type **Syncplicity**.</span></span>
   
    <span data-ttu-id="73b65-127">![Syncplicity application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769532.png "Syncplicity application gallery")</span><span class="sxs-lookup"><span data-stu-id="73b65-127">![Syncplicity application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769532.png "Syncplicity application gallery")</span></span>

7. <span data-ttu-id="73b65-128">In the results pane, select **Syncplicity**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="73b65-128">In the results pane, select **Syncplicity**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="73b65-129">![Syncplicity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769533.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="73b65-129">![Syncplicity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769533.png "Syncplicity")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="73b65-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="73b65-130">Configure single sign-on</span></span>
<span data-ttu-id="73b65-131">This section outlines how to enable users to authenticate to Syncplicity with their account in Azure Active Directory, using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="73b65-131">This section outlines how to enable users to authenticate to Syncplicity with their account in Azure Active Directory, using federation based on the SAML protocol.</span></span>

<span data-ttu-id="73b65-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73b65-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="73b65-133">In the Azure classic portal, on the **Syncplicity** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="73b65-133">In the Azure classic portal, on the **Syncplicity** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="73b65-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769534.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="73b65-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769534.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="73b65-135">On the **How would you like users to sign on to Syncplicity** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="73b65-135">On the **How would you like users to sign on to Syncplicity** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="73b65-136">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769535.png "Microsoft Azure AD Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="73b65-136">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769535.png "Microsoft Azure AD Single Sign-On")</span></span>

3. <span data-ttu-id="73b65-137">On the **Configure App URL** page, in the **Syncplicity Sign In URL** textbox, type the URL users are using to sign into your Syncplicity application click **Next**.</span><span class="sxs-lookup"><span data-stu-id="73b65-137">On the **Configure App URL** page, in the **Syncplicity Sign In URL** textbox, type the URL users are using to sign into your Syncplicity application click **Next**.</span></span> 
   
    <span data-ttu-id="73b65-138">The app URL is your Syncplicity tenant URL (e.g.: *http://company.Syncplicity.com*):</span><span class="sxs-lookup"><span data-stu-id="73b65-138">The app URL is your Syncplicity tenant URL (e.g.: *http://company.Syncplicity.com*):</span></span>
   
    <span data-ttu-id="73b65-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769536.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="73b65-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769536.png "Configure app URL")</span></span>

4. <span data-ttu-id="73b65-140">On the **Configure single sign-on at Syncplicity** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span><span class="sxs-lookup"><span data-stu-id="73b65-140">On the **Configure single sign-on at Syncplicity** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span></span>
   
    <span data-ttu-id="73b65-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769543.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="73b65-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769543.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="73b65-142">Sign in to your **Syncplicity** tenant.</span><span class="sxs-lookup"><span data-stu-id="73b65-142">Sign in to your **Syncplicity** tenant.</span></span>

6. <span data-ttu-id="73b65-143">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="73b65-143">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="73b65-144">![Syncplicity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="73b65-144">![Syncplicity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769545.png "Syncplicity")</span></span>

7. <span data-ttu-id="73b65-145">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73b65-145">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="73b65-146">![Single Sign-On \(SSO\)](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="73b65-146">![Single Sign-On \(SSO\)](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   
  1. <span data-ttu-id="73b65-147">In the **Custom Domain** textbox, type the name of your domain.</span><span class="sxs-lookup"><span data-stu-id="73b65-147">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  2. <span data-ttu-id="73b65-148">Select **Enabled** as **Single Sign-On Status**.</span><span class="sxs-lookup"><span data-stu-id="73b65-148">Select **Enabled** as **Single Sign-On Status**.</span></span>
  3. <span data-ttu-id="73b65-149">In the Azure classic portal, on the **Configure single sign-on at Syncplicity** page, copy the **Entity ID** value, and then paste it into the **Entity Id** textbox.</span><span class="sxs-lookup"><span data-stu-id="73b65-149">In the Azure classic portal, on the **Configure single sign-on at Syncplicity** page, copy the **Entity ID** value, and then paste it into the **Entity Id** textbox.</span></span>
  4. <span data-ttu-id="73b65-150">In the Azure classic portal, on the **Configure single sign-on at Syncplicity** page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="73b65-150">In the Azure classic portal, on the **Configure single sign-on at Syncplicity** page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
  5. <span data-ttu-id="73b65-151">In the Azure classic portal, on the **Configure single sign-on at Syncplicity** page, copy the **Remote Logout URL** value, and then paste it into the **Logout page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="73b65-151">In the Azure classic portal, on the **Configure single sign-on at Syncplicity** page, copy the **Remote Logout URL** value, and then paste it into the **Logout page URL** textbox.</span></span>
  6. <span data-ttu-id="73b65-152">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate you have downloaded from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="73b65-152">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate you have downloaded from the Azure classic portal.</span></span> 
  7. <span data-ttu-id="73b65-153">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="73b65-153">Click **Save Changes**.</span></span>

8. <span data-ttu-id="73b65-154">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="73b65-154">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="73b65-155">![Confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769554.png "Confirmation")</span><span class="sxs-lookup"><span data-stu-id="73b65-155">![Confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769554.png "Confirmation")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="73b65-156">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="73b65-156">Configure user provisioning</span></span>
<span data-ttu-id="73b65-157">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span><span class="sxs-lookup"><span data-stu-id="73b65-157">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="73b65-158">This section describes how to create AAD user accounts in Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="73b65-158">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="73b65-159">**To provision a user account to Syncplicity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73b65-159">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="73b65-160">Log in to your **Syncplicity** tenant (e.g.: *https://company.Syncplicity.com*).</span><span class="sxs-lookup"><span data-stu-id="73b65-160">Log in to your **Syncplicity** tenant (e.g.: *https://company.Syncplicity.com*).</span></span>

2. <span data-ttu-id="73b65-161">Click **Admin** and select **user accounts**.</span><span class="sxs-lookup"><span data-stu-id="73b65-161">Click **Admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="73b65-162">Click **Add a user**.</span><span class="sxs-lookup"><span data-stu-id="73b65-162">Click **Add a user**.</span></span>
   
    <span data-ttu-id="73b65-163">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769764.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="73b65-163">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769764.png "Manage Users")</span></span>

4. <span data-ttu-id="73b65-164">Type the **Email address** of an AAD account you want to provision, select **User** as **Role**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="73b65-164">Type the **Email address** of an AAD account you want to provision, select **User** as **Role**, and then click **Next**.</span></span>
   
    <span data-ttu-id="73b65-165">![Account Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769765.png "Account Information")</span><span class="sxs-lookup"><span data-stu-id="73b65-165">![Account Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="73b65-166">The AAD account holder will get an email including a link to confirm and activate the account.</span><span class="sxs-lookup"><span data-stu-id="73b65-166">The AAD account holder will get an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="73b65-167">Select a group in your company that your new user should become a member of, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="73b65-167">Select a group in your company that your new user should become a member of, and then click **Next**.</span></span>
   
    <span data-ttu-id="73b65-168">![Group Membership](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769772.png "Group Membership")</span><span class="sxs-lookup"><span data-stu-id="73b65-168">![Group Membership](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="73b65-169">If there are no groups listed, just click **Next**.</span><span class="sxs-lookup"><span data-stu-id="73b65-169">If there are no groups listed, just click **Next**.</span></span> 
    > 

6. <span data-ttu-id="73b65-170">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="73b65-170">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="73b65-171">![Syncplicity Folders](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769773.png "Syncplicity Folders")</span><span class="sxs-lookup"><span data-stu-id="73b65-171">![Syncplicity Folders](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="73b65-172">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="73b65-172">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="73b65-173">Assign users</span><span class="sxs-lookup"><span data-stu-id="73b65-173">Assign users</span></span>
<span data-ttu-id="73b65-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="73b65-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="73b65-175">**To assign users to Syncplicity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73b65-175">**To assign users to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="73b65-176">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="73b65-176">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="73b65-177">On the **Syncplicity** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="73b65-177">On the **Syncplicity** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="73b65-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769557.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="73b65-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC769557.png "Assign users")</span></span>

3. <span data-ttu-id="73b65-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="73b65-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="73b65-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="73b65-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-syncplicity-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="73b65-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="73b65-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="73b65-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73b65-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















