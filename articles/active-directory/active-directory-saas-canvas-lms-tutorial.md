---
title: 'Tutorial: Azure Active Directory Integration with Canvas LMS | Microsoft Docs'
description: Learn how to use Canvas LMS with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: db0f6bee52fe5ef7bf3e2ada4057057d14b862cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554517"
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="05e72-103">Tutorial: Azure Active Directory Integration with Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="05e72-103">Tutorial: Azure Active Directory Integration with Canvas LMS</span></span>
<span data-ttu-id="05e72-104">The objective of this tutorial is to show the integration of Azure and Canvas.</span><span class="sxs-lookup"><span data-stu-id="05e72-104">The objective of this tutorial is to show the integration of Azure and Canvas.</span></span>  
<span data-ttu-id="05e72-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="05e72-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="05e72-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="05e72-106">A valid Azure subscription</span></span>
* <span data-ttu-id="05e72-107">A Canvas tenant</span><span class="sxs-lookup"><span data-stu-id="05e72-107">A Canvas tenant</span></span>

<span data-ttu-id="05e72-108">After completing this tutorial, the Azure AD users you have assigned to Canvas will be able to single sign into the application at your Canvas company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05e72-108">After completing this tutorial, the Azure AD users you have assigned to Canvas will be able to single sign into the application at your Canvas company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="05e72-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="05e72-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="05e72-110">Enabling the application integration for Canvas</span><span class="sxs-lookup"><span data-stu-id="05e72-110">Enabling the application integration for Canvas</span></span>
* <span data-ttu-id="05e72-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="05e72-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="05e72-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="05e72-112">Configuring user provisioning</span></span>
* <span data-ttu-id="05e72-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="05e72-113">Assigning users</span></span>

<span data-ttu-id="05e72-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775984.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="05e72-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775984.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-canvas"></a><span data-ttu-id="05e72-115">Enable the application integration for Canvas</span><span class="sxs-lookup"><span data-stu-id="05e72-115">Enable the application integration for Canvas</span></span>
<span data-ttu-id="05e72-116">The objective of this section is to outline how to enable the application integration for Canvas.</span><span class="sxs-lookup"><span data-stu-id="05e72-116">The objective of this section is to outline how to enable the application integration for Canvas.</span></span>

<span data-ttu-id="05e72-117">**To enable the application integration for Canvas, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05e72-117">**To enable the application integration for Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="05e72-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05e72-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="05e72-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="05e72-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="05e72-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="05e72-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="05e72-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="05e72-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="05e72-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="05e72-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="05e72-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="05e72-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="05e72-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="05e72-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="05e72-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="05e72-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="05e72-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="05e72-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="05e72-127">In the **search box**, type **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="05e72-127">In the **search box**, type **Canvas**.</span></span>
   
   <span data-ttu-id="05e72-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775985.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="05e72-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775985.png "Application Gallery")</span></span>
7. <span data-ttu-id="05e72-129">In the results pane, select **Canvas**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="05e72-129">In the results pane, select **Canvas**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="05e72-130">![Canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775986.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="05e72-130">![Canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775986.png "Canvas")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="05e72-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="05e72-131">Configure single sign-on</span></span>

<span data-ttu-id="05e72-132">The objective of this section is to outline how to enable users to authenticate to Canvas with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="05e72-132">The objective of this section is to outline how to enable users to authenticate to Canvas with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="05e72-133">Configuring SSO for Canvas requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="05e72-133">Configuring SSO for Canvas requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="05e72-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="05e72-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span>

<span data-ttu-id="05e72-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05e72-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="05e72-136">In the Azure classic portal, on the **Canvas** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="05e72-136">In the Azure classic portal, on the **Canvas** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="05e72-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC771709.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="05e72-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC771709.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="05e72-138">On the **How would you like users to sign on to Canvas** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e72-138">On the **How would you like users to sign on to Canvas** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="05e72-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775987.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="05e72-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775987.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="05e72-140">On the **Configure App URL** page, in the **Canvas Sign In URL** textbox, type your URL using the following pattern `https://<tenant-name>.instructure.com`, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e72-140">On the **Configure App URL** page, in the **Canvas Sign In URL** textbox, type your URL using the following pattern `https://<tenant-name>.instructure.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="05e72-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775988.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="05e72-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775988.png "Configure App URL")</span></span>
4. <span data-ttu-id="05e72-142">On the **Configure single sign-on at Canvas** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="05e72-142">On the **Configure single sign-on at Canvas** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="05e72-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775989.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="05e72-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775989.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="05e72-144">In a different web browser window, log into your Canvas company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="05e72-144">In a different web browser window, log into your Canvas company site as an administrator.</span></span>
6. <span data-ttu-id="05e72-145">Go to **Courses \> Managed Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="05e72-145">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="05e72-146">![Canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="05e72-146">![Canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>
7. <span data-ttu-id="05e72-147">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span><span class="sxs-lookup"><span data-stu-id="05e72-147">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
   <span data-ttu-id="05e72-148">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="05e72-148">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>
8. <span data-ttu-id="05e72-149">On the Current Integration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05e72-149">On the Current Integration page, perform the following steps:</span></span>
   
   <span data-ttu-id="05e72-150">![Current Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span><span class="sxs-lookup"><span data-stu-id="05e72-150">![Current Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

  1. <span data-ttu-id="05e72-151">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="05e72-151">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox.</span></span>
   2. <span data-ttu-id="05e72-152">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Remote Login URL** value, and then paste it into the **Log On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="05e72-152">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Remote Login URL** value, and then paste it into the **Log On URL** textbox.</span></span>
   3. <span data-ttu-id="05e72-153">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Remote Login URL** value, and then paste it into the **Log Out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="05e72-153">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Remote Login URL** value, and then paste it into the **Log Out URL** textbox.</span></span>
   4. <span data-ttu-id="05e72-154">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Change Password URL** value, and then paste it into the **Change Password Link** textbox.</span><span class="sxs-lookup"><span data-stu-id="05e72-154">In the Azure classic portal, on the **Configure single sign-on at Canvas** dialog page, copy the **Change Password URL** value, and then paste it into the **Change Password Link** textbox.</span></span>
   5. <span data-ttu-id="05e72-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="05e72-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span></span>      
      >[!TIP]
      ><span data-ttu-id="05e72-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="05e72-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span> 
      > 
   6. <span data-ttu-id="05e72-157">From the **Login Attribute** list, select **NameID**.</span><span class="sxs-lookup"><span data-stu-id="05e72-157">From the **Login Attribute** list, select **NameID**.</span></span>
   7. <span data-ttu-id="05e72-158">From the **Identifier Format** list, select **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="05e72-158">From the **Identifier Format** list, select **emailAddress**.</span></span>
   8. <span data-ttu-id="05e72-159">Click **Save Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="05e72-159">Click **Save Authentication Settings**.</span></span>
9. <span data-ttu-id="05e72-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="05e72-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="05e72-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775993.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="05e72-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775993.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="05e72-162">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="05e72-162">Configure user provisioning</span></span>

<span data-ttu-id="05e72-163">In order to enable Azure AD users to log into Canvas, they must be provisioned into Canvas.</span><span class="sxs-lookup"><span data-stu-id="05e72-163">In order to enable Azure AD users to log into Canvas, they must be provisioned into Canvas.</span></span>

* <span data-ttu-id="05e72-164">In the case of Canvas, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="05e72-164">In the case of Canvas, provisioning is a manual task.</span></span>

<span data-ttu-id="05e72-165">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05e72-165">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="05e72-166">Log in to your **Canvas** tenant.</span><span class="sxs-lookup"><span data-stu-id="05e72-166">Log in to your **Canvas** tenant.</span></span>
2. <span data-ttu-id="05e72-167">Go to **Courses \> Managed Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="05e72-167">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="05e72-168">![Canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="05e72-168">![Canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>
3. <span data-ttu-id="05e72-169">Click **Users**.</span><span class="sxs-lookup"><span data-stu-id="05e72-169">Click **Users**.</span></span>
   
   <span data-ttu-id="05e72-170">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span><span class="sxs-lookup"><span data-stu-id="05e72-170">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>
4. <span data-ttu-id="05e72-171">Click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="05e72-171">Click **Add New User**.</span></span>
   
   <span data-ttu-id="05e72-172">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span><span class="sxs-lookup"><span data-stu-id="05e72-172">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>
5. <span data-ttu-id="05e72-173">On the Add a New User dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05e72-173">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="05e72-174">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="05e72-174">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   1. <span data-ttu-id="05e72-175">In the **Full Name** textbox, type the user’s name.</span><span class="sxs-lookup"><span data-stu-id="05e72-175">In the **Full Name** textbox, type the user’s name.</span></span>
   2. <span data-ttu-id="05e72-176">In the **Email** textbox, type the user’s email address.</span><span class="sxs-lookup"><span data-stu-id="05e72-176">In the **Email** textbox, type the user’s email address.</span></span>
   3. <span data-ttu-id="05e72-177">In the **Login** textbox, type the user’s Azure AD email address.</span><span class="sxs-lookup"><span data-stu-id="05e72-177">In the **Login** textbox, type the user’s Azure AD email address.</span></span>
   4. <span data-ttu-id="05e72-178">Select **Email the user about this account creation**.</span><span class="sxs-lookup"><span data-stu-id="05e72-178">Select **Email the user about this account creation**.</span></span>
   5. <span data-ttu-id="05e72-179">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="05e72-179">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="05e72-180">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="05e72-180">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="05e72-181">Assign users</span><span class="sxs-lookup"><span data-stu-id="05e72-181">Assign users</span></span>
<span data-ttu-id="05e72-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="05e72-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="05e72-183">**To assign users to Canvas, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05e72-183">**To assign users to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="05e72-184">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="05e72-184">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="05e72-185">On the \*\*Canvas \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="05e72-185">On the \*\*Canvas \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="05e72-186">![Assigning users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775998.png "Assigning users")</span><span class="sxs-lookup"><span data-stu-id="05e72-186">![Assigning users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC775998.png "Assigning users")</span></span>
3. <span data-ttu-id="05e72-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="05e72-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="05e72-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="05e72-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-canvas-lms-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="05e72-189">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="05e72-189">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="05e72-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05e72-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















