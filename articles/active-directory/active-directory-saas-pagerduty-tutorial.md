---
title: 'Tutorial: Azure Active Directory Integration with Pagerduty | Microsoft Docs'
description: Learn how to use Pagerduty with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 297586f41196628ccd56f4f008b0515de029f250
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661838"
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="54e42-103">Tutorial: Azure Active Directory Integration with Pagerduty</span><span class="sxs-lookup"><span data-stu-id="54e42-103">Tutorial: Azure Active Directory Integration with Pagerduty</span></span>
<span data-ttu-id="54e42-104">The objective of this tutorial is to show the integration of Azure and Pagerduty.</span><span class="sxs-lookup"><span data-stu-id="54e42-104">The objective of this tutorial is to show the integration of Azure and Pagerduty.</span></span> <span data-ttu-id="54e42-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="54e42-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="54e42-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="54e42-106">A valid Azure subscription</span></span>
* <span data-ttu-id="54e42-107">A Pagerduty tenant</span><span class="sxs-lookup"><span data-stu-id="54e42-107">A Pagerduty tenant</span></span>

<span data-ttu-id="54e42-108">After completing this tutorial, the Azure AD users you have assigned to Pagerduty will be able to single sign-on (SSO) to the application at your Pagerduty company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54e42-108">After completing this tutorial, the Azure AD users you have assigned to Pagerduty will be able to single sign-on (SSO) to the application at your Pagerduty company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="54e42-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="54e42-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="54e42-110">Enabling the application integration for Pagerduty</span><span class="sxs-lookup"><span data-stu-id="54e42-110">Enabling the application integration for Pagerduty</span></span>
2. <span data-ttu-id="54e42-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="54e42-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="54e42-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="54e42-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="54e42-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="54e42-113">Assigning users</span></span>

<span data-ttu-id="54e42-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778528.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="54e42-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778528.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-pagerduty"></a><span data-ttu-id="54e42-115">Enabling the application integration for Pagerduty</span><span class="sxs-lookup"><span data-stu-id="54e42-115">Enabling the application integration for Pagerduty</span></span>
<span data-ttu-id="54e42-116">The objective of this section is to outline how to enable the application integration for Pagerduty.</span><span class="sxs-lookup"><span data-stu-id="54e42-116">The objective of this section is to outline how to enable the application integration for Pagerduty.</span></span>

<span data-ttu-id="54e42-117">**To enable the application integration for Pagerduty, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54e42-117">**To enable the application integration for Pagerduty, perform the following steps:**</span></span>

1. <span data-ttu-id="54e42-118">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54e42-118">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="54e42-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="54e42-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="54e42-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="54e42-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="54e42-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="54e42-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="54e42-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="54e42-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="54e42-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="54e42-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="54e42-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="54e42-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="54e42-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="54e42-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="54e42-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="54e42-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="54e42-127">In the **search box**, type **Pagerduty**.</span><span class="sxs-lookup"><span data-stu-id="54e42-127">In the **search box**, type **Pagerduty**.</span></span>
   
   <span data-ttu-id="54e42-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778529.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="54e42-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778529.png "Application gallery")</span></span>
7. <span data-ttu-id="54e42-129">In the results pane, select **Pagerduty**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="54e42-129">In the results pane, select **Pagerduty**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="54e42-130">![PagerDuty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778530.png "PagerDuty")</span><span class="sxs-lookup"><span data-stu-id="54e42-130">![PagerDuty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778530.png "PagerDuty")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="54e42-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="54e42-131">Configure single sign-on</span></span>

<span data-ttu-id="54e42-132">The objective of this section is to outline how to enable users to authenticate to Pagerduty with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="54e42-132">The objective of this section is to outline how to enable users to authenticate to Pagerduty with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="54e42-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="54e42-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  

<span data-ttu-id="54e42-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="54e42-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="54e42-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54e42-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="54e42-136">In the Azure classic portal, on the **Pagerduty** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="54e42-136">In the Azure classic portal, on the **Pagerduty** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="54e42-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778531.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54e42-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778531.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="54e42-138">On the **How would you like users to sign on to Pagerduty** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54e42-138">On the **How would you like users to sign on to Pagerduty** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="54e42-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778532.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54e42-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778532.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="54e42-140">On the **Configure App URL** page, in the **Pagerduty Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Pagerduty.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54e42-140">On the **Configure App URL** page, in the **Pagerduty Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Pagerduty.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="54e42-141">![Configure app url](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778533.png "Configure app url")</span><span class="sxs-lookup"><span data-stu-id="54e42-141">![Configure app url](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778533.png "Configure app url")</span></span>
4. <span data-ttu-id="54e42-142">On the **Configure single sign-on at Pagerduty** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="54e42-142">On the **Configure single sign-on at Pagerduty** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="54e42-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778534.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54e42-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778534.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="54e42-144">In a different web browser window, log into your Pagerduty company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="54e42-144">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>
6. <span data-ttu-id="54e42-145">In the menu on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="54e42-145">In the menu on the top, click **Account Settings**.</span></span>
   
   <span data-ttu-id="54e42-146">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778535.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="54e42-146">![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778535.png "Account Settings")</span></span>
7. <span data-ttu-id="54e42-147">Click **single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="54e42-147">Click **single sign-on**.</span></span>
   
   <span data-ttu-id="54e42-148">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778536.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54e42-148">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778536.png "Single sign-on")</span></span>
8. <span data-ttu-id="54e42-149">On the Enable Single Sign-on (SSO) page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54e42-149">On the Enable Single Sign-on (SSO) page, perform the following steps:</span></span>
   
   <span data-ttu-id="54e42-150">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778537.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54e42-150">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778537.png "Enable single sign-on")</span></span>
   
   1. <span data-ttu-id="54e42-151">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="54e42-151">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
      >[!TIP]
      ><span data-ttu-id="54e42-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="54e42-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
      >

  2. <span data-ttu-id="54e42-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="54e42-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  3. <span data-ttu-id="54e42-154">In the Azure classic portal, on the **Configure single sign-on at Pagerduty** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="54e42-154">In the Azure classic portal, on the **Configure single sign-on at Pagerduty** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
  4. <span data-ttu-id="54e42-155">In the Azure classic portal, on the **Configure single sign-on at Pagerduty** dialogue page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="54e42-155">In the Azure classic portal, on the **Configure single sign-on at Pagerduty** dialogue page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
  5. <span data-ttu-id="54e42-156">Select **Turn on Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="54e42-156">Select **Turn on Single Sign-on**.</span></span>
  6. <span data-ttu-id="54e42-157">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="54e42-157">Click **Save Changes**.</span></span>

9. <span data-ttu-id="54e42-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="54e42-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="54e42-159">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778538.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54e42-159">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778538.png "Configure single sign-on")</span></span>
   

## <a name="configure-user-provisioning"></a><span data-ttu-id="54e42-160">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="54e42-160">Configure user provisioning</span></span>

<span data-ttu-id="54e42-161">In order to enable Azure AD users to log into Pagerduty, they must be provisioned into Pagerduty.</span><span class="sxs-lookup"><span data-stu-id="54e42-161">In order to enable Azure AD users to log into Pagerduty, they must be provisioned into Pagerduty.</span></span>  

* <span data-ttu-id="54e42-162">In the case of Pagerduty, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="54e42-162">In the case of Pagerduty, provisioning is a manual task.</span></span>

<span data-ttu-id="54e42-163">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54e42-163">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="54e42-164">Log in to your **Pagerduty** tenant.</span><span class="sxs-lookup"><span data-stu-id="54e42-164">Log in to your **Pagerduty** tenant.</span></span>
2. <span data-ttu-id="54e42-165">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="54e42-165">In the menu on the top, click **Users**.</span></span>
3. <span data-ttu-id="54e42-166">Click **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="54e42-166">Click **Add Users**.</span></span>
   
   <span data-ttu-id="54e42-167">![Add Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778539.png "Add Users")</span><span class="sxs-lookup"><span data-stu-id="54e42-167">![Add Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778539.png "Add Users")</span></span>
4. <span data-ttu-id="54e42-168">On the **Invite your team** dialog, type the **First and Last Name** and the **Email** address of the Azure AD user you want to provision, click **Add**, and then click **Send Invites**.</span><span class="sxs-lookup"><span data-stu-id="54e42-168">On the **Invite your team** dialog, type the **First and Last Name** and the **Email** address of the Azure AD user you want to provision, click **Add**, and then click **Send Invites**.</span></span>
   
   <span data-ttu-id="54e42-169">![Invite your team](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778540.png "Invite your team")</span><span class="sxs-lookup"><span data-stu-id="54e42-169">![Invite your team](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778540.png "Invite your team")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="54e42-170">All added users will receive an invite to create a PagerDuty account.</span><span class="sxs-lookup"><span data-stu-id="54e42-170">All added users will receive an invite to create a PagerDuty account.</span></span>
   > 
   > 

>[!NOTE]
><span data-ttu-id="54e42-171">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="54e42-171">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="54e42-172">Assign users</span><span class="sxs-lookup"><span data-stu-id="54e42-172">Assign users</span></span>
<span data-ttu-id="54e42-173">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="54e42-173">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="54e42-174">**To assign users to Pagerduty, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54e42-174">**To assign users to Pagerduty, perform the following steps:**</span></span>

1. <span data-ttu-id="54e42-175">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="54e42-175">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="54e42-176">On the **Pagerduty** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="54e42-176">On the **Pagerduty** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="54e42-177">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778541.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="54e42-177">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC778541.png "Assign users")</span></span>
3. <span data-ttu-id="54e42-178">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="54e42-178">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="54e42-179">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="54e42-179">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pagerduty-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="54e42-180">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="54e42-180">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="54e42-181">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54e42-181">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54e42-182">Additional resources</span><span class="sxs-lookup"><span data-stu-id="54e42-182">Additional resources</span></span>

* [<span data-ttu-id="54e42-183">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54e42-183">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54e42-184">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54e42-184">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



















