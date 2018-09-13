---
title: 'Tutorial: Azure Active Directory integration with ThousandEyes | Microsoft Docs'
description: Learn how to use ThousandEyes with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: c50eb7b6897d37ffd10b19178ce3f01b8b94d7c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540679"
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="3abff-103">Tutorial: Azure Active Directory integration with ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="3abff-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>
<span data-ttu-id="3abff-104">The objective of this tutorial is to show how to set up single sign-on between Azure Active Directory (Azure AD) and ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="3abff-104">The objective of this tutorial is to show how to set up single sign-on between Azure Active Directory (Azure AD) and ThousandEyes.</span></span>

<span data-ttu-id="3abff-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="3abff-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="3abff-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="3abff-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3abff-107">A ThousandEyes single sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3abff-107">A ThousandEyes single sign on (SSO) enabled subscription</span></span>

<span data-ttu-id="3abff-108">After completing this tutorial, the AAD users to whom you have assign ThousandEyes access will be able to single sign into the application at your ThousandEyes company site (service provider initiated sign on), or using the AAD Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3abff-108">After completing this tutorial, the AAD users to whom you have assign ThousandEyes access will be able to single sign into the application at your ThousandEyes company site (service provider initiated sign on), or using the AAD Access Panel.</span></span>

1. <span data-ttu-id="3abff-109">Enabling the application integration for ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="3abff-109">Enabling the application integration for ThousandEyes</span></span>
2. <span data-ttu-id="3abff-110">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="3abff-110">Configuring single sign-on</span></span>
3. <span data-ttu-id="3abff-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="3abff-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="3abff-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="3abff-112">Assigning users</span></span>

<span data-ttu-id="3abff-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790059.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="3abff-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790059.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-thousandeyes"></a><span data-ttu-id="3abff-114">Enable the application integration for ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="3abff-114">Enable the application integration for ThousandEyes</span></span>
<span data-ttu-id="3abff-115">The objective of this section is to outline how to enable the application integration for ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="3abff-115">The objective of this section is to outline how to enable the application integration for ThousandEyes.</span></span>

<span data-ttu-id="3abff-116">**To enable the application integration for ThousandEyes, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3abff-116">**To enable the application integration for ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="3abff-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3abff-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="3abff-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3abff-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="3abff-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3abff-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3abff-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3abff-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="3abff-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="3abff-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="3abff-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3abff-122">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="3abff-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="3abff-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="3abff-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3abff-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="3abff-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="3abff-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="3abff-126">In the **search box**, type **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="3abff-126">In the **search box**, type **ThousandEyes**.</span></span>
   
    <span data-ttu-id="3abff-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790060.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="3abff-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790060.png "Application Gallery")</span></span>
7. <span data-ttu-id="3abff-128">In the results pane, select **ThousandEyes**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3abff-128">In the results pane, select **ThousandEyes**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="3abff-129">![ThousandEyes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790061.png "ThousandEyes")</span><span class="sxs-lookup"><span data-stu-id="3abff-129">![ThousandEyes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790061.png "ThousandEyes")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="3abff-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="3abff-130">Configure single sign-on</span></span>
<span data-ttu-id="3abff-131">This section outlines how to enable users to authenticate to ThousandEyes with their account in Azure Active Directory, using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="3abff-131">This section outlines how to enable users to authenticate to ThousandEyes with their account in Azure Active Directory, using federation based on the SAML protocol.</span></span>

<span data-ttu-id="3abff-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3abff-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="3abff-133">In the Azure classic portal, on the **ThousandEyes** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="3abff-133">In the Azure classic portal, on the **ThousandEyes** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="3abff-134">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790062.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="3abff-134">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790062.png "Configure Single SignOn")</span></span>

2. <span data-ttu-id="3abff-135">On the **How would you like users to sign on to ThousandEyes** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3abff-135">On the **How would you like users to sign on to ThousandEyes** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="3abff-136">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790063.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="3abff-136">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790063.png "Configure Single SignOn")</span></span>

3. <span data-ttu-id="3abff-137">On the **Configure App URL** page, in the **ThousandEyes Sign On URL** textbox, type the URL users are using to sign into your ThousandEyes application (e.g.: "*https://app.thousandeyes.com/login/sso*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3abff-137">On the **Configure App URL** page, in the **ThousandEyes Sign On URL** textbox, type the URL users are using to sign into your ThousandEyes application (e.g.: "*https://app.thousandeyes.com/login/sso*"), and then click **Next**.</span></span> 
   
    <span data-ttu-id="3abff-138">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790064.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="3abff-138">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790064.png "Configure App URL")</span></span>

4. <span data-ttu-id="3abff-139">On the **Configure single sign-on at ThousandEyes** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span><span class="sxs-lookup"><span data-stu-id="3abff-139">On the **Configure single sign-on at ThousandEyes** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span></span>
   
    <span data-ttu-id="3abff-140">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790065.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="3abff-140">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790065.png "Configure Single SignOn")</span></span>

5. <span data-ttu-id="3abff-141">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3abff-141">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

6. <span data-ttu-id="3abff-142">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="3abff-142">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="3abff-143">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="3abff-143">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

7. <span data-ttu-id="3abff-144">Click **Account**</span><span class="sxs-lookup"><span data-stu-id="3abff-144">Click **Account**</span></span>
   
    <span data-ttu-id="3abff-145">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="3abff-145">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

8. <span data-ttu-id="3abff-146">Click the **Security & Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="3abff-146">Click the **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="3abff-147">![Security & Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790068.png "Security & Authentication")</span><span class="sxs-lookup"><span data-stu-id="3abff-147">![Security & Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790068.png "Security & Authentication")</span></span>

9. <span data-ttu-id="3abff-148">In the **Setup Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3abff-148">In the **Setup Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3abff-149">![Setup Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790069.png "Setup Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="3abff-149">![Setup Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790069.png "Setup Single Sign-On")</span></span>
  1. <span data-ttu-id="3abff-150">Select **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3abff-150">Select **Enable Single Sign-On**.</span></span>
  2. <span data-ttu-id="3abff-151">In the Microsoft Azure classic portal, on the **Configure single sign-on at ThousandEyes** page, copy the **Remote Login URL** value, and then paste it into the **Login Page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3abff-151">In the Microsoft Azure classic portal, on the **Configure single sign-on at ThousandEyes** page, copy the **Remote Login URL** value, and then paste it into the **Login Page URL** textbox.</span></span>
  3. <span data-ttu-id="3abff-152">In the Microsoft Azure classic portal, on the **Configure single sign-on at ThousandEyes** page, copy the **Remote Logout URL** value, and then paste it into the **Logout Page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3abff-152">In the Microsoft Azure classic portal, on the **Configure single sign-on at ThousandEyes** page, copy the **Remote Logout URL** value, and then paste it into the **Logout Page URL** textbox.</span></span>
  4. <span data-ttu-id="3abff-153">In the Microsoft Azure classic portal, on the **Configure single sign-on at ThousandEyes** page, copy the **Issuer URL** value, and then paste it into the **Identity Provider Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="3abff-153">In the Microsoft Azure classic portal, on the **Configure single sign-on at ThousandEyes** page, copy the **Issuer URL** value, and then paste it into the **Identity Provider Issuer** textbox.</span></span>
  5. <span data-ttu-id="3abff-154">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate you have downloaded from the Microsoft Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="3abff-154">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate you have downloaded from the Microsoft Azure classic portal.</span></span>
  6. <span data-ttu-id="3abff-155">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3abff-155">Click **Save**.</span></span>

10. <span data-ttu-id="3abff-156">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="3abff-156">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="3abff-157">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790070.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="3abff-157">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790070.png "Configure Single SignOn")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="3abff-158">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="3abff-158">Configure user provisioning</span></span>
<span data-ttu-id="3abff-159">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="3abff-159">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="3abff-160">In the case of ThousandEyes, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3abff-160">In the case of ThousandEyes, provisioning is a manual task.</span></span>

<span data-ttu-id="3abff-161">**To provision a user account to ThousandEyes, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3abff-161">**To provision a user account to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="3abff-162">Log into your ThousandEyes company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3abff-162">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="3abff-163">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="3abff-163">Click **Settings**.</span></span>
   
    <span data-ttu-id="3abff-164">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="3abff-164">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="3abff-165">Click **Account**.</span><span class="sxs-lookup"><span data-stu-id="3abff-165">Click **Account**.</span></span>
   
    <span data-ttu-id="3abff-166">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="3abff-166">![Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="3abff-167">Click the **Accounts & Users** tab.</span><span class="sxs-lookup"><span data-stu-id="3abff-167">Click the **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="3abff-168">![Accounts & Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span><span class="sxs-lookup"><span data-stu-id="3abff-168">![Accounts & Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="3abff-169">In the **Add Users & Accounts** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3abff-169">In the **Add Users & Accounts** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3abff-170">![Add User Accounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span><span class="sxs-lookup"><span data-stu-id="3abff-170">![Add User Accounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  1. <span data-ttu-id="3abff-171">Type the **Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="3abff-171">Type the **Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="3abff-172">Click **Add New User to Account**.</span><span class="sxs-lookup"><span data-stu-id="3abff-172">Click **Add New User to Account**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="3abff-173">The AAD account holder will get an email including a link to confirm and activate the account.</span><span class="sxs-lookup"><span data-stu-id="3abff-173">The AAD account holder will get an email including a link to confirm and activate the account.</span></span>
     >  

>[!NOTE]
><span data-ttu-id="3abff-174">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="3abff-174">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="3abff-175">Assign users</span><span class="sxs-lookup"><span data-stu-id="3abff-175">Assign users</span></span>
<span data-ttu-id="3abff-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="3abff-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="3abff-177">**To assign users to ThousandEyes, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3abff-177">**To assign users to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="3abff-178">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="3abff-178">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="3abff-179">On the **ThousandEyes** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="3abff-179">On the **ThousandEyes** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="3abff-180">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790075.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="3abff-180">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC790075.png "Assign Users")</span></span>

3. <span data-ttu-id="3abff-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="3abff-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="3abff-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="3abff-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thousandeyes-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3abff-183">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3abff-183">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3abff-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3abff-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>























