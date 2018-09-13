---
title: 'Tutorial: Azure Active Directory integration with FM:Systems | Microsoft Docs'
description: Learn how to use FM:Systems with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 15d504bdf7a0ba034aaf73eecefeb848c3f2fbe9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540656"
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="19b3d-103">Tutorial: Azure Active Directory integration with FM:Systems</span><span class="sxs-lookup"><span data-stu-id="19b3d-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>
<span data-ttu-id="19b3d-104">The objective of this tutorial is to show the integration of Azure and FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="19b3d-104">The objective of this tutorial is to show the integration of Azure and FM:Systems.</span></span>  
<span data-ttu-id="19b3d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="19b3d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="19b3d-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="19b3d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="19b3d-107">A FM:Systems single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="19b3d-107">A FM:Systems single sign-on enabled subscription</span></span>

<span data-ttu-id="19b3d-108">After completing this tutorial, the Azure AD users you have assigned to FM:Systems will be able to single sign into the application at your FM:Systems company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19b3d-108">After completing this tutorial, the Azure AD users you have assigned to FM:Systems will be able to single sign into the application at your FM:Systems company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="19b3d-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19b3d-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="19b3d-110">Enabling the application integration for FM:Systems</span><span class="sxs-lookup"><span data-stu-id="19b3d-110">Enabling the application integration for FM:Systems</span></span>
2. <span data-ttu-id="19b3d-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="19b3d-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="19b3d-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="19b3d-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="19b3d-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="19b3d-113">Assigning users</span></span>

<span data-ttu-id="19b3d-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795899.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="19b3d-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795899.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-fmsystems"></a><span data-ttu-id="19b3d-115">Enabling the application integration for FM:Systems</span><span class="sxs-lookup"><span data-stu-id="19b3d-115">Enabling the application integration for FM:Systems</span></span>
<span data-ttu-id="19b3d-116">The objective of this section is to outline how to enable the application integration for FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="19b3d-116">The objective of this section is to outline how to enable the application integration for FM:Systems.</span></span>

### <a name="to-enable-the-application-integration-for-fmsystems-perform-the-following-steps"></a><span data-ttu-id="19b3d-117">To enable the application integration for FM:Systems, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19b3d-117">To enable the application integration for FM:Systems, perform the following steps:</span></span>
1. <span data-ttu-id="19b3d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="19b3d-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="19b3d-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="19b3d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19b3d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="19b3d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19b3d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="19b3d-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="19b3d-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="19b3d-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19b3d-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="19b3d-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="19b3d-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="19b3d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="19b3d-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="19b3d-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="19b3d-127">In the **search box**, type **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-127">In the **search box**, type **FM:Systems**.</span></span>
   
    <span data-ttu-id="19b3d-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795900.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="19b3d-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795900.png "Application Gallery")</span></span>

7. <span data-ttu-id="19b3d-129">In the results pane, select **FM:Systems**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="19b3d-129">In the results pane, select **FM:Systems**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="19b3d-130">![FM:Systems](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC800213.png "FM:Systems")</span><span class="sxs-lookup"><span data-stu-id="19b3d-130">![FM:Systems](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC800213.png "FM:Systems")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="19b3d-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="19b3d-131">Configuring single sign-on</span></span>

<span data-ttu-id="19b3d-132">The objective of this section is to outline how to enable users to authenticate to FM:Systems with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="19b3d-132">The objective of this section is to outline how to enable users to authenticate to FM:Systems with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="19b3d-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19b3d-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="19b3d-134">In the Azure classic portal, on the **FM:Systems** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="19b3d-134">In the Azure classic portal, on the **FM:Systems** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="19b3d-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC790810.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19b3d-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC790810.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="19b3d-136">On the **How would you like users to sign on to FM:Systems** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-136">On the **How would you like users to sign on to FM:Systems** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="19b3d-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795901.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19b3d-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795901.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="19b3d-138">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19b3d-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="19b3d-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795902.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="19b3d-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795902.png "Configure App URL")</span></span>
   
    <span data-ttu-id="19b3d-140">a.</span><span class="sxs-lookup"><span data-stu-id="19b3d-140">a.</span></span> <span data-ttu-id="19b3d-141">In the **FM:Systems Sign On URL** textbox, type your FM:Systems **Reply URL** (e.g.: *https://dpr.fmshosted.com/fminteract/ConsumerService2.aspx*).</span><span class="sxs-lookup"><span data-stu-id="19b3d-141">In the **FM:Systems Sign On URL** textbox, type your FM:Systems **Reply URL** (e.g.: *https://dpr.fmshosted.com/fminteract/ConsumerService2.aspx*).</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="19b3d-142">You can get this value from your FM:Systems support team.</span><span class="sxs-lookup"><span data-stu-id="19b3d-142">You can get this value from your FM:Systems support team.</span></span>
    > 
    > 
   
    <span data-ttu-id="19b3d-143">b.</span><span class="sxs-lookup"><span data-stu-id="19b3d-143">b.</span></span> <span data-ttu-id="19b3d-144">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="19b3d-144">Click **Next**</span></span>

4. <span data-ttu-id="19b3d-145">On the **Configure single sign-on at FM:Systems** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span><span class="sxs-lookup"><span data-stu-id="19b3d-145">On the **Configure single sign-on at FM:Systems** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="19b3d-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795903.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19b3d-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795903.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="19b3d-147">Submit the downloaded metadata file to your FM:Systems support team.</span><span class="sxs-lookup"><span data-stu-id="19b3d-147">Submit the downloaded metadata file to your FM:Systems support team.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="19b3d-148">Your FM:Systems support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="19b3d-148">Your FM:Systems support team has to do the actual SSO configuration.</span></span>
    > <span data-ttu-id="19b3d-149">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="19b3d-149">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    > 
6. <span data-ttu-id="19b3d-150">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="19b3d-150">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="19b3d-151">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795904.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19b3d-151">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795904.png "Configure Single Sign-On")</span></span>
   
## <a name="configuring-user-provisioning"></a><span data-ttu-id="19b3d-152">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="19b3d-152">Configuring user provisioning</span></span>

<span data-ttu-id="19b3d-153">In order to enable Azure AD users to log into FM:Systems, they must be provisioned into FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="19b3d-153">In order to enable Azure AD users to log into FM:Systems, they must be provisioned into FM:Systems.</span></span>  
<span data-ttu-id="19b3d-154">In the case of FM:Systems, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="19b3d-154">In the case of FM:Systems, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="19b3d-155">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19b3d-155">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="19b3d-156">In a web browser window, log into your FM:Systems company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="19b3d-156">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="19b3d-157">Go to **System Administration \> Manage Security \> Users \> User list**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-157">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="19b3d-158">![System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795905.png "System Administration")</span><span class="sxs-lookup"><span data-stu-id="19b3d-158">![System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795905.png "System Administration")</span></span>

3. <span data-ttu-id="19b3d-159">Click **Create new user**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-159">Click **Create new user**.</span></span>
   
    <span data-ttu-id="19b3d-160">![Create New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795906.png "Create New User")</span><span class="sxs-lookup"><span data-stu-id="19b3d-160">![Create New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795906.png "Create New User")</span></span>

4. <span data-ttu-id="19b3d-161">In the **Create User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19b3d-161">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="19b3d-162">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795907.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="19b3d-162">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795907.png "Create User")</span></span>
   
    <span data-ttu-id="19b3d-163">a.</span><span class="sxs-lookup"><span data-stu-id="19b3d-163">a.</span></span> <span data-ttu-id="19b3d-164">Type the user name, the password and its confirmation, the email address and the employee ID of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="19b3d-164">Type the user name, the password and its confirmation, the email address and the employee ID of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="19b3d-165">b.</span><span class="sxs-lookup"><span data-stu-id="19b3d-165">b.</span></span> <span data-ttu-id="19b3d-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-166">Click **Next**.</span></span>
 

## <a name="assigning-users"></a><span data-ttu-id="19b3d-167">Assigning users</span><span class="sxs-lookup"><span data-stu-id="19b3d-167">Assigning users</span></span>
<span data-ttu-id="19b3d-168">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="19b3d-168">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-fmsystems-perform-the-following-steps"></a><span data-ttu-id="19b3d-169">To assign users to FM:Systems, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19b3d-169">To assign users to FM:Systems, perform the following steps:</span></span>
1. <span data-ttu-id="19b3d-170">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="19b3d-170">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="19b3d-171">On the \*\*FM:Systems \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="19b3d-171">On the \*\*FM:Systems \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="19b3d-172">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795908.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="19b3d-172">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795908.png "Assign Users")</span></span>

3. <span data-ttu-id="19b3d-173">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="19b3d-173">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="19b3d-174">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="19b3d-174">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="19b3d-175">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="19b3d-175">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="19b3d-176">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19b3d-176">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















