---
title: 'Tutorial: Azure Active Directory integration with AppDynamics | Microsoft Docs'
description: Learn how to use AppDynamics with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 64b802c60502c347fd3fd4a3eb8ff44e371fb08e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551633"
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="a87a0-103">Tutorial: Azure Active Directory integration with AppDynamics</span><span class="sxs-lookup"><span data-stu-id="a87a0-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>
<span data-ttu-id="a87a0-104">The objective of this tutorial is to show the integration of Azure and AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="a87a0-104">The objective of this tutorial is to show the integration of Azure and AppDynamics.</span></span> <span data-ttu-id="a87a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a87a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a87a0-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a87a0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a87a0-107">An AppDynamics single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a87a0-107">An AppDynamics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a87a0-108">After completing this tutorial, the Azure AD users you have assigned to AppDynamics will be able to single sign into the application at your AppDynamics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a87a0-108">After completing this tutorial, the Azure AD users you have assigned to AppDynamics will be able to single sign into the application at your AppDynamics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a87a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a87a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="a87a0-110">Enabling the application integration for AppDynamics</span><span class="sxs-lookup"><span data-stu-id="a87a0-110">Enabling the application integration for AppDynamics</span></span>
* <span data-ttu-id="a87a0-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="a87a0-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="a87a0-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a87a0-112">Configuring user provisioning</span></span>
* <span data-ttu-id="a87a0-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a87a0-113">Assigning users</span></span>

<span data-ttu-id="a87a0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790209.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a87a0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790209.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-appdynamics"></a><span data-ttu-id="a87a0-115">Enabling the application integration for AppDynamics</span><span class="sxs-lookup"><span data-stu-id="a87a0-115">Enabling the application integration for AppDynamics</span></span>
<span data-ttu-id="a87a0-116">The objective of this section is to outline how to enable the application integration for AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="a87a0-116">The objective of this section is to outline how to enable the application integration for AppDynamics.</span></span>

<span data-ttu-id="a87a0-117">**To enable the application integration for AppDynamics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a87a0-117">**To enable the application integration for AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="a87a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a87a0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a87a0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a87a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a87a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a87a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a87a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a87a0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a87a0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a87a0-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a87a0-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a87a0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a87a0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a87a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a87a0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a87a0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a87a0-127">In the **search box**, type **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-127">In the **search box**, type **AppDynamics**.</span></span>
   
   <span data-ttu-id="a87a0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790210.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a87a0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790210.png "Application Gallery")</span></span>
7. <span data-ttu-id="a87a0-129">In the results pane, select **AppDynamics**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a87a0-129">In the results pane, select **AppDynamics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a87a0-130">![AppDynamics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790211.png "AppDynamics")</span><span class="sxs-lookup"><span data-stu-id="a87a0-130">![AppDynamics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790211.png "AppDynamics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a87a0-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a87a0-131">Configure single sign-on</span></span>

<span data-ttu-id="a87a0-132">The objective of this section is to outline how to enable users to authenticate to AppDynamics with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a87a0-132">The objective of this section is to outline how to enable users to authenticate to AppDynamics with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="a87a0-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="a87a0-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="a87a0-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a87a0-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="a87a0-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a87a0-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a87a0-136">In the Azure classic portal, on the **AppDynamics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a87a0-136">In the Azure classic portal, on the **AppDynamics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a87a0-137">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790212.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="a87a0-137">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790212.png "Configure Single SignOn")</span></span>
2. <span data-ttu-id="a87a0-138">On the **How would you like users to sign on to AppDynamics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-138">On the **How would you like users to sign on to AppDynamics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a87a0-139">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790213.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="a87a0-139">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790213.png "Configure Single SignOn")</span></span>
3. <span data-ttu-id="a87a0-140">On the **Configure App URL** page, in the **AppDynamics Sign On URL** textbox, type your URL used by your users to sign-on to AppDynamics ("*https://companyname.saas.appdynamics.com*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-140">On the **Configure App URL** page, in the **AppDynamics Sign On URL** textbox, type your URL used by your users to sign-on to AppDynamics ("*https://companyname.saas.appdynamics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="a87a0-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790214.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a87a0-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790214.png "Configure App URL")</span></span>
4. <span data-ttu-id="a87a0-142">On the **Configure single sign-on at AppDynamics** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a87a0-142">On the **Configure single sign-on at AppDynamics** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="a87a0-143">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790215.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="a87a0-143">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790215.png "Configure Single SignOn")</span></span>
5. <span data-ttu-id="a87a0-144">In a different web browser window, log into your AppDynamics company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a87a0-144">In a different web browser window, log into your AppDynamics company site as an administrator.</span></span>
6. <span data-ttu-id="a87a0-145">In the toolbar on the top, click **Settings**, and then click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-145">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
   <span data-ttu-id="a87a0-146">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790216.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="a87a0-146">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790216.png "Administration")</span></span>
7. <span data-ttu-id="a87a0-147">Click the **Authentication Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="a87a0-147">Click the **Authentication Provider** tab.</span></span>
   
   <span data-ttu-id="a87a0-148">![Authentication Provider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790224.png "Authentication Provider")</span><span class="sxs-lookup"><span data-stu-id="a87a0-148">![Authentication Provider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790224.png "Authentication Provider")</span></span>
8. <span data-ttu-id="a87a0-149">In the **Authentication Provider** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a87a0-149">In the **Authentication Provider** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a87a0-150">![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790225.png "SAML Configuration")</span><span class="sxs-lookup"><span data-stu-id="a87a0-150">![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790225.png "SAML Configuration")</span></span>   
   1. <span data-ttu-id="a87a0-151">As **Authentication Provider**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-151">As **Authentication Provider**, select **SAML**.</span></span>
   2. <span data-ttu-id="a87a0-152">In the Azure classic portal, on the **Configure single sign-on at AppDynamics** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a87a0-152">In the Azure classic portal, on the **Configure single sign-on at AppDynamics** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   3. <span data-ttu-id="a87a0-153">In the Azure classic portal, on the **Configure single sign-on at AppDynamics** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a87a0-153">In the Azure classic portal, on the **Configure single sign-on at AppDynamics** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
   4. <span data-ttu-id="a87a0-154">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="a87a0-154">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
   
      >[!TIP]
      ><span data-ttu-id="a87a0-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a87a0-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
      > 
   5. <span data-ttu-id="a87a0-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="a87a0-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>
   6. <span data-ttu-id="a87a0-157">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-157">Click **Save**.</span></span>

     <span data-ttu-id="a87a0-158">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC777673.png "Save")</span><span class="sxs-lookup"><span data-stu-id="a87a0-158">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC777673.png "Save")</span></span>
9. <span data-ttu-id="a87a0-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a87a0-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a87a0-160">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790226.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="a87a0-160">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790226.png "Configure Single SignOn")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="a87a0-161">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a87a0-161">Configure user provisioning</span></span>

<span data-ttu-id="a87a0-162">In order to enable Azure AD users to log into AppDynamics, they must be provisioned into AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="a87a0-162">In order to enable Azure AD users to log into AppDynamics, they must be provisioned into AppDynamics.</span></span>  
<span data-ttu-id="a87a0-163">In the case of AppDynamics, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a87a0-163">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="a87a0-164">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a87a0-164">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a87a0-165">Log into your AppDynamics company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a87a0-165">Log into your AppDynamics company site as an administrator.</span></span>
2. <span data-ttu-id="a87a0-166">Go to **Users**, and then click **+** to open the **Create User** dialog.</span><span class="sxs-lookup"><span data-stu-id="a87a0-166">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
   <span data-ttu-id="a87a0-167">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790229.png "Users")</span><span class="sxs-lookup"><span data-stu-id="a87a0-167">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790229.png "Users")</span></span>
3. <span data-ttu-id="a87a0-168">In the **Create User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a87a0-168">In the **Create User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a87a0-169">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790230.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="a87a0-169">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790230.png "Create User")</span></span>
   
   1. <span data-ttu-id="a87a0-170">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="a87a0-170">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="a87a0-171">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-171">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="a87a0-172">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a87a0-172">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>
> 

## <a name="assign-users"></a><span data-ttu-id="a87a0-173">Assign users</span><span class="sxs-lookup"><span data-stu-id="a87a0-173">Assign users</span></span>
<span data-ttu-id="a87a0-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a87a0-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a87a0-175">**To assign users to AppDynamics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a87a0-175">**To assign users to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="a87a0-176">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a87a0-176">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a87a0-177">On the **AppDynamics** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a87a0-177">On the **AppDynamics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a87a0-178">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790231.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="a87a0-178">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790231.png "Assign Users")</span></span>
3. <span data-ttu-id="a87a0-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a87a0-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a87a0-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a87a0-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a87a0-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a87a0-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a87a0-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a87a0-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















