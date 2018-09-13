---
title: 'Tutorial: Azure Active Directory Integration with ITRP | Microsoft Docs'
description: Learn how to use ITRP with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/09/2017
ms.author: jeedes
ms.openlocfilehash: 1ebe8031fb8a7bcb48e1a84bf69869b942f25d6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563418"
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="06d15-103">Tutorial: Azure Active Directory Integration with ITRP</span><span class="sxs-lookup"><span data-stu-id="06d15-103">Tutorial: Azure Active Directory Integration with ITRP</span></span>
<span data-ttu-id="06d15-104">The objective of this tutorial is to show the integration of Azure and ITRP.</span><span class="sxs-lookup"><span data-stu-id="06d15-104">The objective of this tutorial is to show the integration of Azure and ITRP.</span></span>  
<span data-ttu-id="06d15-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="06d15-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="06d15-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="06d15-106">A valid Azure subscription</span></span>
* <span data-ttu-id="06d15-107">A ITRP tenant</span><span class="sxs-lookup"><span data-stu-id="06d15-107">A ITRP tenant</span></span>

<span data-ttu-id="06d15-108">After completing this tutorial, the Azure AD users you have assigned to ITRP will be able to single sign into the application at your ITRP company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06d15-108">After completing this tutorial, the Azure AD users you have assigned to ITRP will be able to single sign into the application at your ITRP company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="06d15-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="06d15-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="06d15-110">Enabling the application integration for ITRP</span><span class="sxs-lookup"><span data-stu-id="06d15-110">Enabling the application integration for ITRP</span></span>
2. <span data-ttu-id="06d15-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="06d15-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="06d15-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="06d15-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="06d15-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="06d15-113">Assigning users</span></span>

<span data-ttu-id="06d15-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775551.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="06d15-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775551.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-itrp"></a><span data-ttu-id="06d15-115">Enable the application integration for ITRP</span><span class="sxs-lookup"><span data-stu-id="06d15-115">Enable the application integration for ITRP</span></span>
<span data-ttu-id="06d15-116">The objective of this section is to outline how to enable the application integration for ITRP.</span><span class="sxs-lookup"><span data-stu-id="06d15-116">The objective of this section is to outline how to enable the application integration for ITRP.</span></span>

<span data-ttu-id="06d15-117">**To enable the application integration for ITRP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06d15-117">**To enable the application integration for ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="06d15-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="06d15-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="06d15-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="06d15-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="06d15-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="06d15-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="06d15-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="06d15-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="06d15-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="06d15-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="06d15-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="06d15-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="06d15-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="06d15-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="06d15-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="06d15-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="06d15-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="06d15-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="06d15-127">In the **search box**, type **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="06d15-127">In the **search box**, type **ITRP**.</span></span>
   
    <span data-ttu-id="06d15-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775565.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="06d15-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775565.png "Application Gallery")</span></span>

7. <span data-ttu-id="06d15-129">In the results pane, select **ITRP**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="06d15-129">In the results pane, select **ITRP**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="06d15-130">![ITRP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775566.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="06d15-130">![ITRP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775566.png "ITRP")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="06d15-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="06d15-131">Configure single sign-on</span></span>

<span data-ttu-id="06d15-132">The objective of this section is to outline how to enable users to authenticate to ITRP with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="06d15-132">The objective of this section is to outline how to enable users to authenticate to ITRP with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="06d15-133">Configuring single sign-on for ITRP requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="06d15-133">Configuring single sign-on for ITRP requires you to retrieve a thumbprint value from a certificate.</span></span>  

<span data-ttu-id="06d15-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="06d15-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="06d15-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06d15-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="06d15-136">In the Azure classic portal, on the **ITRP** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="06d15-136">In the Azure classic portal, on the **ITRP** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="06d15-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC771709.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="06d15-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC771709.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="06d15-138">On the **How would you like users to sign on to ITRP** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="06d15-138">On the **How would you like users to sign on to ITRP** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="06d15-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775567.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06d15-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775567.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="06d15-140">On the **Configure App URL** page, in the **ITRP Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.ITRP.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="06d15-140">On the **Configure App URL** page, in the **ITRP Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.ITRP.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="06d15-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775568.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="06d15-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775568.png "Configure App URL")</span></span>

4. <span data-ttu-id="06d15-142">On the **Configure single sign-on at ITRP** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\ITRP.cer**.</span><span class="sxs-lookup"><span data-stu-id="06d15-142">On the **Configure single sign-on at ITRP** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\ITRP.cer**.</span></span>
   
    <span data-ttu-id="06d15-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775569.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06d15-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775569.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="06d15-144">In a different web browser window, log into your ITRP company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="06d15-144">In a different web browser window, log into your ITRP company site as an administrator.</span></span>

6. <span data-ttu-id="06d15-145">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="06d15-145">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="06d15-146">![ITRP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="06d15-146">![ITRP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775570.png "ITRP")</span></span>

7. <span data-ttu-id="06d15-147">In the left navigation pane, select **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="06d15-147">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="06d15-148">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775571.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06d15-148">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775571.png "Single Sign-On")</span></span>

8. <span data-ttu-id="06d15-149">In the Single Sign-On configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="06d15-149">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="06d15-150">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775572.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06d15-150">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="06d15-151">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775573.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06d15-151">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775573.png "Single Sign-On")</span></span>   
  1. <span data-ttu-id="06d15-152">Click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="06d15-152">Click **Enable**.</span></span>
  2. <span data-ttu-id="06d15-153">In the Azure classic portal, on the **Configure single sign-on at ITRP** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="06d15-153">In the Azure classic portal, on the **Configure single sign-on at ITRP** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.</span></span>
  3. <span data-ttu-id="06d15-154">In the Azure classic portal, on the **Configure single sign-on at ITRP** dialog page, copy the **SAML SSO URL** value, and then paste it into the **SAML SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="06d15-154">In the Azure classic portal, on the **Configure single sign-on at ITRP** dialog page, copy the **SAML SSO URL** value, and then paste it into the **SAML SSO URL** textbox.</span></span>
  4. <span data-ttu-id="06d15-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="06d15-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span></span>
      
     >[!TIP]
     ><span data-ttu-id="06d15-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="06d15-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>
     >
    
  5. <span data-ttu-id="06d15-157">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="06d15-157">Click **Save**.</span></span>

9. <span data-ttu-id="06d15-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="06d15-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="06d15-159">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775574.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06d15-159">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775574.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="06d15-160">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="06d15-160">Configure user provisioning</span></span>

<span data-ttu-id="06d15-161">In order to enable Azure AD users to log into ITRP, they must be provisioned into ITRP.</span><span class="sxs-lookup"><span data-stu-id="06d15-161">In order to enable Azure AD users to log into ITRP, they must be provisioned into ITRP.</span></span>  

<span data-ttu-id="06d15-162">In the case of ITRP, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="06d15-162">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="06d15-163">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06d15-163">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="06d15-164">Log in to your **ITRP** tenant.</span><span class="sxs-lookup"><span data-stu-id="06d15-164">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="06d15-165">In the toolbar on the top, click **Records**.</span><span class="sxs-lookup"><span data-stu-id="06d15-165">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="06d15-166">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775575.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="06d15-166">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775575.png "Admin")</span></span>

3. <span data-ttu-id="06d15-167">From the popup menu, select **People**.</span><span class="sxs-lookup"><span data-stu-id="06d15-167">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="06d15-168">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775587.png "People")</span><span class="sxs-lookup"><span data-stu-id="06d15-168">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775587.png "People")</span></span>

4. <span data-ttu-id="06d15-169">Click **Add New Person** (“+”).</span><span class="sxs-lookup"><span data-stu-id="06d15-169">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="06d15-170">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775576.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="06d15-170">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775576.png "Admin")</span></span>

5. <span data-ttu-id="06d15-171">On the Add New Person dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="06d15-171">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="06d15-172">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775577.png "User")</span><span class="sxs-lookup"><span data-stu-id="06d15-172">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775577.png "User")</span></span>   
  1. <span data-ttu-id="06d15-173">Type the **Name**, **Email** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="06d15-173">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>
  2. <span data-ttu-id="06d15-174">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="06d15-174">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="06d15-175">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="06d15-175">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="06d15-176">Assign users</span><span class="sxs-lookup"><span data-stu-id="06d15-176">Assign users</span></span>
<span data-ttu-id="06d15-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="06d15-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="06d15-178">**To assign users to ITRP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06d15-178">**To assign users to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="06d15-179">In the Azure AD portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="06d15-179">In the Azure AD portal, create a test account.</span></span>

2. <span data-ttu-id="06d15-180">On the \*\*ITRP \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="06d15-180">On the \*\*ITRP \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="06d15-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775588.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="06d15-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC775588.png "Assign Users")</span></span>

3. <span data-ttu-id="06d15-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="06d15-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="06d15-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="06d15-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-itrp-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="06d15-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="06d15-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="06d15-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06d15-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>























