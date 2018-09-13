---
title: 'Tutorial: Azure Active Directory Integration with xMatters OnDemand | Microsoft Docs'
description: Learn how to use xMatters OnDemand with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 3536d48b117520824f0741366037c97902c833d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555468"
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="f94cc-103">Tutorial: Azure Active Directory Integration with xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="f94cc-103">Tutorial: Azure Active Directory Integration with xMatters OnDemand</span></span>
<span data-ttu-id="f94cc-104">The objective of this tutorial is to show the integration of Azure and xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="f94cc-104">The objective of this tutorial is to show the integration of Azure and xMatters OnDemand.</span></span> <span data-ttu-id="f94cc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="f94cc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="f94cc-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f94cc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f94cc-107">A xMatters OnDemand tenant</span><span class="sxs-lookup"><span data-stu-id="f94cc-107">A xMatters OnDemand tenant</span></span>

<span data-ttu-id="f94cc-108">After completing this tutorial, the Azure AD users you have assigned to xMatters OnDemand will be able to single sign into the application at your xMatters OnDemand company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f94cc-108">After completing this tutorial, the Azure AD users you have assigned to xMatters OnDemand will be able to single sign into the application at your xMatters OnDemand company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="f94cc-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f94cc-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="f94cc-110">Enabling the application integration for xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="f94cc-110">Enabling the application integration for xMatters OnDemand</span></span>
2. <span data-ttu-id="f94cc-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="f94cc-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="f94cc-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="f94cc-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="f94cc-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="f94cc-113">Assigning users</span></span>

<span data-ttu-id="f94cc-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776788.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="f94cc-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776788.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-xmatters-ondemand"></a><span data-ttu-id="f94cc-115">Enabling the application integration for xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="f94cc-115">Enabling the application integration for xMatters OnDemand</span></span>
<span data-ttu-id="f94cc-116">The objective of this section is to outline how to enable the application integration for xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="f94cc-116">The objective of this section is to outline how to enable the application integration for xMatters OnDemand.</span></span>

### <a name="to-enable-the-application-integration-for-xmatters-ondemand-perform-the-following-steps"></a><span data-ttu-id="f94cc-117">To enable the application integration for xMatters OnDemand, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-117">To enable the application integration for xMatters OnDemand, perform the following steps:</span></span>
1. <span data-ttu-id="f94cc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="f94cc-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f94cc-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="f94cc-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f94cc-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f94cc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f94cc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="f94cc-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="f94cc-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="f94cc-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f94cc-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="f94cc-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="f94cc-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="f94cc-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="f94cc-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="f94cc-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="f94cc-127">In the **search box**, type **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-127">In the **search box**, type **xMatters OnDemand**.</span></span>
   
    <span data-ttu-id="f94cc-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776789.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="f94cc-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776789.png "Application gallery")</span></span>

7. <span data-ttu-id="f94cc-129">In the results pane, select **XMatters OnDemand**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f94cc-129">In the results pane, select **XMatters OnDemand**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="f94cc-130">![xMatters OnDemand](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776790.png "xMatters OnDemand")</span><span class="sxs-lookup"><span data-stu-id="f94cc-130">![xMatters OnDemand](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776790.png "xMatters OnDemand")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="f94cc-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="f94cc-131">Configuring single sign-on</span></span>
<span data-ttu-id="f94cc-132">The objective of this section is to outline how to enable users to authenticate to XMatters OnDemand with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="f94cc-132">The objective of this section is to outline how to enable users to authenticate to XMatters OnDemand with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="f94cc-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="f94cc-134">In the Azure classic portal, on the **XMatters OnDemand** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="f94cc-134">In the Azure classic portal, on the **XMatters OnDemand** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="f94cc-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776791.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f94cc-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776791.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="f94cc-136">On the **How would you like users to sign on to XMatters OnDemand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-136">On the **How would you like users to sign on to XMatters OnDemand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="f94cc-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776792.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f94cc-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776792.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="f94cc-138">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="f94cc-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776793.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="f94cc-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776793.png "Configure app URL")</span></span>
   
    <span data-ttu-id="f94cc-140">a.</span><span class="sxs-lookup"><span data-stu-id="f94cc-140">a.</span></span> <span data-ttu-id="f94cc-141">In the **XMatters OnDemand Sign In URL** textbox, type your URL using the following pattern: `https://<tenant-name>.XMattersOnDemandapp.com`</span><span class="sxs-lookup"><span data-stu-id="f94cc-141">In the **XMatters OnDemand Sign In URL** textbox, type your URL using the following pattern: `https://<tenant-name>.XMattersOnDemandapp.com`</span></span>
   
    <span data-ttu-id="f94cc-142">b.</span><span class="sxs-lookup"><span data-stu-id="f94cc-142">b.</span></span> <span data-ttu-id="f94cc-143">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-143">Click **Next**.</span></span>

4. <span data-ttu-id="f94cc-144">On the **Configure single sign-on at XMatters OnDemand** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-144">On the **Configure single sign-on at XMatters OnDemand** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="f94cc-145">You need to forward the certificate to the xMatters support team.</span><span class="sxs-lookup"><span data-stu-id="f94cc-145">You need to forward the certificate to the xMatters support team.</span></span> <span data-ttu-id="f94cc-146">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="f94cc-146">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span>
    > 
    > 
   
    <span data-ttu-id="f94cc-147">![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776794.png "Configure single sign on")</span><span class="sxs-lookup"><span data-stu-id="f94cc-147">![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776794.png "Configure single sign on")</span></span>

5. <span data-ttu-id="f94cc-148">In a different web browser window, log into your XMatters OnDemand company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f94cc-148">In a different web browser window, log into your XMatters OnDemand company site as an administrator.</span></span>

6. <span data-ttu-id="f94cc-149">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span><span class="sxs-lookup"><span data-stu-id="f94cc-149">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="f94cc-150">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f94cc-150">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

7. <span data-ttu-id="f94cc-151">On the **SAML Configuration** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-151">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="f94cc-152">![SAML configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span><span class="sxs-lookup"><span data-stu-id="f94cc-152">![SAML configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="f94cc-153">a.</span><span class="sxs-lookup"><span data-stu-id="f94cc-153">a.</span></span> <span data-ttu-id="f94cc-154">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-154">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="f94cc-155">b.</span><span class="sxs-lookup"><span data-stu-id="f94cc-155">b.</span></span> <span data-ttu-id="f94cc-156">In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="f94cc-156">In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="f94cc-157">c.</span><span class="sxs-lookup"><span data-stu-id="f94cc-157">c.</span></span> <span data-ttu-id="f94cc-158">In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f94cc-158">In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="f94cc-159">d.</span><span class="sxs-lookup"><span data-stu-id="f94cc-159">d.</span></span> <span data-ttu-id="f94cc-160">In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Single Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f94cc-160">In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="f94cc-161">e.</span><span class="sxs-lookup"><span data-stu-id="f94cc-161">e.</span></span> <span data-ttu-id="f94cc-162">On the Company Details page, at the top, click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-162">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="f94cc-163">![Company details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span><span class="sxs-lookup"><span data-stu-id="f94cc-163">![Company details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

8. <span data-ttu-id="f94cc-164">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="f94cc-164">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="f94cc-165">![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776798.png "Configure single sign on")</span><span class="sxs-lookup"><span data-stu-id="f94cc-165">![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776798.png "Configure single sign on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="f94cc-166">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="f94cc-166">Configuring user provisioning</span></span>
<span data-ttu-id="f94cc-167">In order to enable Azure AD users to log into XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="f94cc-167">In order to enable Azure AD users to log into XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span>  
<span data-ttu-id="f94cc-168">In the case of XMatters OnDemand, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f94cc-168">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="f94cc-169">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-169">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="f94cc-170">Log in to your **XMatters OnDemand** tenant.</span><span class="sxs-lookup"><span data-stu-id="f94cc-170">Log in to your **XMatters OnDemand** tenant.</span></span>

2. <span data-ttu-id="f94cc-171">Click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="f94cc-171">Click the **Users** tab.</span></span>

3. <span data-ttu-id="f94cc-172">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-172">Click **Add User**.</span></span>
  
    <span data-ttu-id="f94cc-173">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span><span class="sxs-lookup"><span data-stu-id="f94cc-173">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

4. <span data-ttu-id="f94cc-174">Select **Active**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-174">Select **Active**.</span></span>

5. <span data-ttu-id="f94cc-175">In the **Add a User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-175">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f94cc-176">![Add a User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span><span class="sxs-lookup"><span data-stu-id="f94cc-176">![Add a User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>
   
    <span data-ttu-id="f94cc-177">a.</span><span class="sxs-lookup"><span data-stu-id="f94cc-177">a.</span></span> <span data-ttu-id="f94cc-178">Enter the **UserID**, **First name**, **Last name**, **Site** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="f94cc-178">Enter the **UserID**, **First name**, **Last name**, **Site** of a valid AAD account you want to provision.</span></span>
    
    <span data-ttu-id="f94cc-179">b.</span><span class="sxs-lookup"><span data-stu-id="f94cc-179">b.</span></span> <span data-ttu-id="f94cc-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-180">Click **Save**.</span></span>


## <a name="assigning-users"></a><span data-ttu-id="f94cc-181">Assigning users</span><span class="sxs-lookup"><span data-stu-id="f94cc-181">Assigning users</span></span>
<span data-ttu-id="f94cc-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="f94cc-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-xmatters-ondemand-perform-the-following-steps"></a><span data-ttu-id="f94cc-183">To assign users to XMatters OnDemand, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f94cc-183">To assign users to XMatters OnDemand, perform the following steps:</span></span>
1. <span data-ttu-id="f94cc-184">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="f94cc-184">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="f94cc-185">On the \*\*XMatters OnDemand \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="f94cc-185">On the \*\*XMatters OnDemand \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="f94cc-186">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776799.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="f94cc-186">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776799.png "Assign users")</span></span>

3. <span data-ttu-id="f94cc-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="f94cc-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="f94cc-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="f94cc-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f94cc-189">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f94cc-189">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f94cc-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f94cc-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















