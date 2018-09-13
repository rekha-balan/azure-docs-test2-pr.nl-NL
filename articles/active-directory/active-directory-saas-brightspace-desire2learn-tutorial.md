---
title: 'Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn | Microsoft Docs'
description: Learn how to use Brightspace by Desire2Learn with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 814dede9d6ef08addb2cbc6d5e3aa9fee23209fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554252"
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="be29c-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="be29c-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>
<span data-ttu-id="be29c-104">The objective of this tutorial is to show the integration of Azure and Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="be29c-104">The objective of this tutorial is to show the integration of Azure and Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="be29c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="be29c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="be29c-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="be29c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="be29c-107">A Brightspace by Desire2Learn single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="be29c-107">A Brightspace by Desire2Learn single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="be29c-108">After completing this tutorial, the Azure AD users you have assigned to Brightspace by Desire2Learn will be able to single sign into the application at your Brightspace by Desire2Learn company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be29c-108">After completing this tutorial, the Azure AD users you have assigned to Brightspace by Desire2Learn will be able to single sign into the application at your Brightspace by Desire2Learn company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="be29c-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="be29c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="be29c-110">Enabling the application integration for Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="be29c-110">Enabling the application integration for Brightspace by Desire2Learn</span></span>
* <span data-ttu-id="be29c-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="be29c-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="be29c-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="be29c-112">Configuring user provisioning</span></span>
* <span data-ttu-id="be29c-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="be29c-113">Assigning users</span></span>

<span data-ttu-id="be29c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798957.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="be29c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798957.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-brightspace-by-desire2learn"></a><span data-ttu-id="be29c-115">Enable the application integration for Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="be29c-115">Enable the application integration for Brightspace by Desire2Learn</span></span>
<span data-ttu-id="be29c-116">The objective of this section is to outline how to enable the application integration for Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="be29c-116">The objective of this section is to outline how to enable the application integration for Brightspace by Desire2Learn.</span></span>

<span data-ttu-id="be29c-117">**To enable the application integration for Brightspace by Desire2Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be29c-117">**To enable the application integration for Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="be29c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be29c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="be29c-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="be29c-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="be29c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="be29c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="be29c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="be29c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="be29c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="be29c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="be29c-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="be29c-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="be29c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="be29c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="be29c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="be29c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="be29c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="be29c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="be29c-127">In the **search box**, type **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="be29c-127">In the **search box**, type **Brightspace by Desire2Learn**.</span></span>
   
   <span data-ttu-id="be29c-128">![Apllication Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798958.png "Apllication Gallery")</span><span class="sxs-lookup"><span data-stu-id="be29c-128">![Apllication Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798958.png "Apllication Gallery")</span></span>
7. <span data-ttu-id="be29c-129">In the results pane, select **Brightspace by Desire2Learn**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="be29c-129">In the results pane, select **Brightspace by Desire2Learn**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="be29c-130">![Brightspace by Desire2Learn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC799321.png "Brightspace by Desire2Learn")</span><span class="sxs-lookup"><span data-stu-id="be29c-130">![Brightspace by Desire2Learn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC799321.png "Brightspace by Desire2Learn")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="be29c-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="be29c-131">Configure single sign-on</span></span>

<span data-ttu-id="be29c-132">The objective of this section is to outline how to enable users to authenticate to Brightspace by Desire2Learn with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="be29c-132">The objective of this section is to outline how to enable users to authenticate to Brightspace by Desire2Learn with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="be29c-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be29c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="be29c-134">In the Azure classic portal, on the **Brightspace by Desire2Learn** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="be29c-134">In the Azure classic portal, on the **Brightspace by Desire2Learn** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="be29c-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798959.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be29c-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798959.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="be29c-136">On the **How would you like users to sign on to Brightspace by Desire2Learn** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="be29c-136">On the **How would you like users to sign on to Brightspace by Desire2Learn** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="be29c-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798960.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be29c-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798960.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="be29c-138">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="be29c-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="be29c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798961.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="be29c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798961.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="be29c-140">In the **Sign On URL** textbox, type the URL used by your users to sign into your **Brightspace by Desire2Learn** (e.g.: *https://partnershowcase.desire2learn.com/Shibboleth.sso/Login?entityID=https://sts.windows-ppe.net/5caf9349-fd93-4a74-b064-0070f65bfb49/&target=https%3A%2F%2Fpartnershowcase.desire2learn.com%2Fd2l%2FshibbolethSSO%2Faspinfo.asp*).</span><span class="sxs-lookup"><span data-stu-id="be29c-140">In the **Sign On URL** textbox, type the URL used by your users to sign into your **Brightspace by Desire2Learn** (e.g.: *https://partnershowcase.desire2learn.com/Shibboleth.sso/Login?entityID=https://sts.windows-ppe.net/5caf9349-fd93-4a74-b064-0070f65bfb49/&target=https%3A%2F%2Fpartnershowcase.desire2learn.com%2Fd2l%2FshibbolethSSO%2Faspinfo.asp*).</span></span>
   2. <span data-ttu-id="be29c-141">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="be29c-141">Click **Next**.</span></span>
4. <span data-ttu-id="be29c-142">On the **Configure single sign-on at Brightspace by Desire2Learn** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span><span class="sxs-lookup"><span data-stu-id="be29c-142">On the **Configure single sign-on at Brightspace by Desire2Learn** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
   <span data-ttu-id="be29c-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798962.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be29c-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798962.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="be29c-144">Send the downloaded metadata file to your Brightspace by Desire2Learn support team.</span><span class="sxs-lookup"><span data-stu-id="be29c-144">Send the downloaded metadata file to your Brightspace by Desire2Learn support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="be29c-145">Your Brightspace by Desire2Learn support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="be29c-145">Your Brightspace by Desire2Learn support team has to do the actual SSO configuration.</span></span>
   ><span data-ttu-id="be29c-146">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="be29c-146">You will get a notification when SSO has been enabled for your subscription.</span></span>
   > 
 
6. <span data-ttu-id="be29c-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="be29c-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="be29c-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798963.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be29c-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798963.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="be29c-149">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="be29c-149">Configure user provisioning</span></span>

<span data-ttu-id="be29c-150">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="be29c-150">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="be29c-151">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your Brightspace by Desire2Learn support team.</span><span class="sxs-lookup"><span data-stu-id="be29c-151">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your Brightspace by Desire2Learn support team.</span></span>

>[!NOTE]
><span data-ttu-id="be29c-152">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="be29c-152">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="be29c-153">Assign users</span><span class="sxs-lookup"><span data-stu-id="be29c-153">Assign users</span></span>
<span data-ttu-id="be29c-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="be29c-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="be29c-155">**To assign users to Brightspace by Desire2Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be29c-155">**To assign users to Brightspace by Desire2Learn, perform the following steps:**</span></span>
1. <span data-ttu-id="be29c-156">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="be29c-156">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="be29c-157">On the \*\*Brightspace by Desire2Learn \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="be29c-157">On the \*\*Brightspace by Desire2Learn \*\*application integration page, click **Assign users**.</span></span>
   
  <span data-ttu-id="be29c-158">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798964.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="be29c-158">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC798964.png "Assign Users")</span></span>
3. <span data-ttu-id="be29c-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="be29c-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
  <span data-ttu-id="be29c-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="be29c-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-brightspace-desire2learn-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="be29c-161">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="be29c-161">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="be29c-162">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be29c-162">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















