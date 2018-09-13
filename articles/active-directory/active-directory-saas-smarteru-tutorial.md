---
title: 'Tutorial: Azure Active Directory integration with SmarterU | Microsoft Docs'
description: Learn how to use SmarterU with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: a5036606aacc2f26196658a0423802f5ce50281c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662218"
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="cbf41-103">Tutorial: Azure Active Directory Integration with SmarterU</span><span class="sxs-lookup"><span data-stu-id="cbf41-103">Tutorial: Azure Active Directory Integration with SmarterU</span></span>
<span data-ttu-id="cbf41-104">The objective of this tutorial is to show the integration of Azure and SmarterU.</span><span class="sxs-lookup"><span data-stu-id="cbf41-104">The objective of this tutorial is to show the integration of Azure and SmarterU.</span></span>  

<span data-ttu-id="cbf41-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="cbf41-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="cbf41-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="cbf41-106">A valid Azure subscription</span></span>
* <span data-ttu-id="cbf41-107">A SmarterU tenant</span><span class="sxs-lookup"><span data-stu-id="cbf41-107">A SmarterU tenant</span></span>

<span data-ttu-id="cbf41-108">After completing this tutorial, the Azure AD users you have assigned to SmarterU will be able to sign into the application using single sign-on (SSO) at your SmarterU company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cbf41-108">After completing this tutorial, the Azure AD users you have assigned to SmarterU will be able to sign into the application using single sign-on (SSO) at your SmarterU company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="cbf41-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cbf41-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="cbf41-110">Enabling the application integration for SmarterU</span><span class="sxs-lookup"><span data-stu-id="cbf41-110">Enabling the application integration for SmarterU</span></span>
2. <span data-ttu-id="cbf41-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="cbf41-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="cbf41-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="cbf41-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="cbf41-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="cbf41-113">Assigning users</span></span>

<span data-ttu-id="cbf41-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777320.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="cbf41-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777320.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-smarteru"></a><span data-ttu-id="cbf41-115">Enable the application integration for SmarterU</span><span class="sxs-lookup"><span data-stu-id="cbf41-115">Enable the application integration for SmarterU</span></span>
<span data-ttu-id="cbf41-116">The objective of this section is to outline how to enable the application integration for SmarterU.</span><span class="sxs-lookup"><span data-stu-id="cbf41-116">The objective of this section is to outline how to enable the application integration for SmarterU.</span></span>

<span data-ttu-id="cbf41-117">**To enable the application integration for SmarterU, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbf41-117">**To enable the application integration for SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="cbf41-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="cbf41-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="cbf41-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="cbf41-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="cbf41-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="cbf41-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="cbf41-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="cbf41-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="cbf41-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="cbf41-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="cbf41-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="cbf41-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="cbf41-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="cbf41-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="cbf41-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="cbf41-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="cbf41-127">In the **search box**, type **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-127">In the **search box**, type **SmarterU**.</span></span>
   
    <span data-ttu-id="cbf41-128">![Application fallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777321.png "Application fallery")</span><span class="sxs-lookup"><span data-stu-id="cbf41-128">![Application fallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777321.png "Application fallery")</span></span>

7. <span data-ttu-id="cbf41-129">In the results pane, select **SmarterU**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="cbf41-129">In the results pane, select **SmarterU**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="cbf41-130">![SmarterU](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777322.png "SmarterU")</span><span class="sxs-lookup"><span data-stu-id="cbf41-130">![SmarterU](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777322.png "SmarterU")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="cbf41-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="cbf41-131">Configure single sign-on</span></span>
<span data-ttu-id="cbf41-132">The objective of this section is to outline how to enable users to authenticate to SmarterU with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="cbf41-132">The objective of this section is to outline how to enable users to authenticate to SmarterU with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="cbf41-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbf41-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="cbf41-134">In the Azure classic portal, on the **SmarterU** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="cbf41-134">In the Azure classic portal, on the **SmarterU** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="cbf41-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777323.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbf41-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777323.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="cbf41-136">On the **How would you like users to sign on to SmarterU** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-136">On the **How would you like users to sign on to SmarterU** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="cbf41-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777324.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbf41-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777324.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="cbf41-138">On the **Configure single sign-on at SmarterU** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\SmarterUMetaData.cer**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-138">On the **Configure single sign-on at SmarterU** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\SmarterUMetaData.cer**.</span></span>
   
    <span data-ttu-id="cbf41-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777325.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbf41-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777325.png "Configure Single Sign-On")</span></span>

4. <span data-ttu-id="cbf41-140">In a different web browser window, log into your SmarterU company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cbf41-140">In a different web browser window, log into your SmarterU company site as an administrator.</span></span>

5. <span data-ttu-id="cbf41-141">In the toolbar on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-141">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="cbf41-142">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="cbf41-142">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

6. <span data-ttu-id="cbf41-143">On the account configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbf41-143">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="cbf41-144">![External Authorization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span><span class="sxs-lookup"><span data-stu-id="cbf41-144">![External Authorization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
  1. <span data-ttu-id="cbf41-145">Select **Enable External Authorization**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-145">Select **Enable External Authorization**.</span></span>
  2. <span data-ttu-id="cbf41-146">In the **Master Login Control** section, select the **SmarterU** tab.</span><span class="sxs-lookup"><span data-stu-id="cbf41-146">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  3. <span data-ttu-id="cbf41-147">In the **User Default Login** section, select the **SmarterU** tab.</span><span class="sxs-lookup"><span data-stu-id="cbf41-147">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  4. <span data-ttu-id="cbf41-148">Select **Enable Okta**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-148">Select **Enable Okta**.</span></span>
  5. <span data-ttu-id="cbf41-149">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="cbf41-149">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  6. <span data-ttu-id="cbf41-150">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-150">Click **Save**.</span></span>

7. <span data-ttu-id="cbf41-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="cbf41-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="cbf41-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777328.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbf41-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777328.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="cbf41-153">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="cbf41-153">Configure user provisioning</span></span>
<span data-ttu-id="cbf41-154">In order to enable Azure AD users to log into SmarterU, they must be provisioned into SmarterU.</span><span class="sxs-lookup"><span data-stu-id="cbf41-154">In order to enable Azure AD users to log into SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="cbf41-155">In the case of SmarterU, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="cbf41-155">In the case of SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="cbf41-156">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbf41-156">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="cbf41-157">Log in to your **SmarterU** tenant.</span><span class="sxs-lookup"><span data-stu-id="cbf41-157">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="cbf41-158">Go to **Users**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-158">Go to **Users**.</span></span>

3. <span data-ttu-id="cbf41-159">In the user section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbf41-159">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="cbf41-160">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span><span class="sxs-lookup"><span data-stu-id="cbf41-160">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>   
  1. <span data-ttu-id="cbf41-161">Click **+User**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-161">Click **+User**.</span></span>
  2. <span data-ttu-id="cbf41-162">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-162">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
  3. <span data-ttu-id="cbf41-163">Click **Active**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-163">Click **Active**.</span></span> 
  4. <span data-ttu-id="cbf41-164">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-164">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="cbf41-165">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="cbf41-165">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

## <a name="assign-users"></a><span data-ttu-id="cbf41-166">Assign users</span><span class="sxs-lookup"><span data-stu-id="cbf41-166">Assign users</span></span>
<span data-ttu-id="cbf41-167">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="cbf41-167">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="cbf41-168">**To assign users to SmarterU, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbf41-168">**To assign users to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="cbf41-169">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="cbf41-169">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="cbf41-170">On the **SmarterU** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="cbf41-170">On the **SmarterU** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="cbf41-171">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777330.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="cbf41-171">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777330.png "Assign Users")</span></span>

3. <span data-ttu-id="cbf41-172">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="cbf41-172">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="cbf41-173">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="cbf41-173">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="cbf41-174">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cbf41-174">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="cbf41-175">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cbf41-175">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















