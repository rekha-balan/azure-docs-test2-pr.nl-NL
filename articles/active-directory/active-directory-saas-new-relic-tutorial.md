---
title: 'Tutorial: Azure Active Directory integration with New Relic | Microsoft Docs'
description: Learn how to use New Relic with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 413e9ac8d089a844bc0345c70b961d2a4f78fb9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669199"
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="50e7d-103">Tutorial: Azure Active Directory integration with New Relic</span><span class="sxs-lookup"><span data-stu-id="50e7d-103">Tutorial: Azure Active Directory integration with New Relic</span></span>
<span data-ttu-id="50e7d-104">The objective of this tutorial is to show how to set up single sign-on (SSO) between Azure Active Directory and New Relic.</span><span class="sxs-lookup"><span data-stu-id="50e7d-104">The objective of this tutorial is to show how to set up single sign-on (SSO) between Azure Active Directory and New Relic.</span></span>

<span data-ttu-id="50e7d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="50e7d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="50e7d-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="50e7d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="50e7d-107">A New Relic single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="50e7d-107">A New Relic single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="50e7d-108">After completing this tutorial, the Azure Active Directory users you have assigned to New Relic will be able to SSO using the AAD Access Panel.</span><span class="sxs-lookup"><span data-stu-id="50e7d-108">After completing this tutorial, the Azure Active Directory users you have assigned to New Relic will be able to SSO using the AAD Access Panel.</span></span>

1. <span data-ttu-id="50e7d-109">Enabling the application integration for New Relic</span><span class="sxs-lookup"><span data-stu-id="50e7d-109">Enabling the application integration for New Relic</span></span>
2. <span data-ttu-id="50e7d-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="50e7d-110">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="50e7d-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="50e7d-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="50e7d-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="50e7d-112">Assigning users</span></span>

<span data-ttu-id="50e7d-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797030.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="50e7d-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797030.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-new-relic"></a><span data-ttu-id="50e7d-114">Enabling the application integration for New Relic</span><span class="sxs-lookup"><span data-stu-id="50e7d-114">Enabling the application integration for New Relic</span></span>
<span data-ttu-id="50e7d-115">The objective of this section is to outline how to enable the application integration for New Relic.</span><span class="sxs-lookup"><span data-stu-id="50e7d-115">The objective of this section is to outline how to enable the application integration for New Relic.</span></span>

<span data-ttu-id="50e7d-116">**To enable the application integration for New Relic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50e7d-116">**To enable the application integration for New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="50e7d-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="50e7d-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="50e7d-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="50e7d-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="50e7d-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="50e7d-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="50e7d-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="50e7d-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="50e7d-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="50e7d-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="50e7d-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="50e7d-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="50e7d-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="50e7d-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="50e7d-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="50e7d-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="50e7d-126">In the **search box**, type **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-126">In the **search box**, type **New Relic**.</span></span>
   
   <span data-ttu-id="50e7d-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797031.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="50e7d-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797031.png "Application Gallery")</span></span>
7. <span data-ttu-id="50e7d-128">In the results pane, select **New Relic**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="50e7d-128">In the results pane, select **New Relic**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="50e7d-129">![New Relic](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797032.png "New Relic")</span><span class="sxs-lookup"><span data-stu-id="50e7d-129">![New Relic](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797032.png "New Relic")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="50e7d-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="50e7d-130">Configure single sign-on</span></span>

<span data-ttu-id="50e7d-131">This section outlines how to enable users to authenticate to New Relic with their account in Azure Active Directory, using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="50e7d-131">This section outlines how to enable users to authenticate to New Relic with their account in Azure Active Directory, using federation based on the SAML protocol.</span></span>

<span data-ttu-id="50e7d-132">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50e7d-132">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="50e7d-133">In the Azure classic portal, on the **New Relic** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="50e7d-133">In the Azure classic portal, on the **New Relic** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="50e7d-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC769534.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="50e7d-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC769534.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="50e7d-135">On the **How would you like users to sign on to New Relic** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-135">On the **How would you like users to sign on to New Relic** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="50e7d-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797033.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="50e7d-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797033.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="50e7d-137">On the **Configure App URL** page, in the **New Relic Sign On URL** textbox, type the URL used by your users to sign on to your New Relic application, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-137">On the **Configure App URL** page, in the **New Relic Sign On URL** textbox, type the URL used by your users to sign on to your New Relic application, and then click **Next**.</span></span> 
   
   <span data-ttu-id="50e7d-138">The app URL is your New Relic tenant URL (e.g.: *https://rpm.newrelic.com*):</span><span class="sxs-lookup"><span data-stu-id="50e7d-138">The app URL is your New Relic tenant URL (e.g.: *https://rpm.newrelic.com*):</span></span>
   
   <span data-ttu-id="50e7d-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797034.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="50e7d-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797034.png "Configure App URL")</span></span>
4. <span data-ttu-id="50e7d-140">On the **Configure single sign-on at New Relic** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span><span class="sxs-lookup"><span data-stu-id="50e7d-140">On the **Configure single sign-on at New Relic** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span></span>
   
   <span data-ttu-id="50e7d-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797035.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="50e7d-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797035.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="50e7d-142">In a different web browser window, sign on to your **New Relic** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="50e7d-142">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>
6. <span data-ttu-id="50e7d-143">In the menu on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-143">In the menu on the top, click **Account Settings**.</span></span>
   
   <span data-ttu-id="50e7d-144">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797036.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="50e7d-144">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797036.png "Account Settings")</span></span>
7. <span data-ttu-id="50e7d-145">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span><span class="sxs-lookup"><span data-stu-id="50e7d-145">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
   <span data-ttu-id="50e7d-146">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797037.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="50e7d-146">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797037.png "Single Sign-On")</span></span>
8. <span data-ttu-id="50e7d-147">On the SAML dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50e7d-147">On the SAML dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="50e7d-148">![SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="50e7d-148">![SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797038.png "SAML")</span></span>
   
   1. <span data-ttu-id="50e7d-149">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span><span class="sxs-lookup"><span data-stu-id="50e7d-149">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>
   2. <span data-ttu-id="50e7d-150">In the Azure classic portal, on the **Configure single sign-on at New Relic** page, copy the **Remote Login URL** value, and then paste it into the **Remote login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="50e7d-150">In the Azure classic portal, on the **Configure single sign-on at New Relic** page, copy the **Remote Login URL** value, and then paste it into the **Remote login URL** textbox.</span></span>
   3. <span data-ttu-id="50e7d-151">In the Azure classic portal, on the **Configure single sign-on at New Relic** page, copy the **Remote Logout URL** value, and then paste it into the **Logout landing URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="50e7d-151">In the Azure classic portal, on the **Configure single sign-on at New Relic** page, copy the **Remote Logout URL** value, and then paste it into the **Logout landing URL** textbox.</span></span>
   4. <span data-ttu-id="50e7d-152">Click **Save my changes**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-152">Click **Save my changes**.</span></span>
9. <span data-ttu-id="50e7d-153">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="50e7d-153">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="50e7d-154">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797039.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="50e7d-154">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797039.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="50e7d-155">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="50e7d-155">Configure user provisioning</span></span>

<span data-ttu-id="50e7d-156">In order to enable Azure Active Directory users to log into New Relic, they must be provisioned into New Relic.</span><span class="sxs-lookup"><span data-stu-id="50e7d-156">In order to enable Azure Active Directory users to log into New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="50e7d-157">In the case of New Relic, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="50e7d-157">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="50e7d-158">**To provision a user account to New Relic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50e7d-158">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="50e7d-159">Log in to your **New Relic** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="50e7d-159">Log in to your **New Relic** company site as administrator.</span></span>
2. <span data-ttu-id="50e7d-160">In the menu on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-160">In the menu on the top, click **Account Settings**.</span></span>
   
   <span data-ttu-id="50e7d-161">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797040.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="50e7d-161">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797040.png "Account Settings")</span></span>
3. <span data-ttu-id="50e7d-162">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-162">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
   <span data-ttu-id="50e7d-163">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797041.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="50e7d-163">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797041.png "Account Settings")</span></span>
4. <span data-ttu-id="50e7d-164">On the **Active users** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50e7d-164">On the **Active users** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="50e7d-165">![Active Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797042.png "Active Users")</span><span class="sxs-lookup"><span data-stu-id="50e7d-165">![Active Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797042.png "Active Users")</span></span>
   
   1. <span data-ttu-id="50e7d-166">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="50e7d-166">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>
   2. <span data-ttu-id="50e7d-167">As **Role** select **User**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-167">As **Role** select **User**.</span></span>
   3. <span data-ttu-id="50e7d-168">Click **Add this user**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-168">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="50e7d-169">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="50e7d-169">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="50e7d-170">Assign users</span><span class="sxs-lookup"><span data-stu-id="50e7d-170">Assign users</span></span>
<span data-ttu-id="50e7d-171">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="50e7d-171">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="50e7d-172">**To assign users to New Relic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50e7d-172">**To assign users to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="50e7d-173">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="50e7d-173">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="50e7d-174">On the **New Relic** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="50e7d-174">On the **New Relic** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="50e7d-175">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797043.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="50e7d-175">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC797043.png "Assign Users")</span></span>
3. <span data-ttu-id="50e7d-176">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="50e7d-176">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="50e7d-177">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="50e7d-177">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-new-relic-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="50e7d-178">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="50e7d-178">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="50e7d-179">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50e7d-179">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50e7d-180">Additional resources</span><span class="sxs-lookup"><span data-stu-id="50e7d-180">Additional resources</span></span>

* [<span data-ttu-id="50e7d-181">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50e7d-181">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50e7d-182">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50e7d-182">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



















