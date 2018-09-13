---
title: 'Tutorial: Azure Active Directory integration with AirWatch | Microsoft Docs'
description: Learn how to use AirWatch with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: dd238be11bf911e2d9b28c6f5497ece91239bc8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548737"
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="6a783-103">Tutorial: Azure Active Directory integration with AirWatch</span><span class="sxs-lookup"><span data-stu-id="6a783-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>
<span data-ttu-id="6a783-104">The objective of this tutorial is to show the integration of Azure and AirWatch.</span><span class="sxs-lookup"><span data-stu-id="6a783-104">The objective of this tutorial is to show the integration of Azure and AirWatch.</span></span>  
<span data-ttu-id="6a783-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6a783-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6a783-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="6a783-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6a783-107">An AirWatch single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6a783-107">An AirWatch single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="6a783-108">After completing this tutorial, the Azure AD users you have assigned to AirWatch will be able to single sign into the application at your AirWatch company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a783-108">After completing this tutorial, the Azure AD users you have assigned to AirWatch will be able to single sign into the application at your AirWatch company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6a783-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6a783-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="6a783-110">Enabling the application integration for AirWatch</span><span class="sxs-lookup"><span data-stu-id="6a783-110">Enabling the application integration for AirWatch</span></span>
* <span data-ttu-id="6a783-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="6a783-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="6a783-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6a783-112">Configuring user provisioning</span></span>
* <span data-ttu-id="6a783-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6a783-113">Assigning users</span></span>

<span data-ttu-id="6a783-114">![AirWatch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791913.png "AirWatch")</span><span class="sxs-lookup"><span data-stu-id="6a783-114">![AirWatch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791913.png "AirWatch")</span></span>

## <a name="enable-the-application-integration-for-airwatch"></a><span data-ttu-id="6a783-115">Enable the application integration for AirWatch</span><span class="sxs-lookup"><span data-stu-id="6a783-115">Enable the application integration for AirWatch</span></span>
<span data-ttu-id="6a783-116">The objective of this section is to outline how to enable the application integration for AirWatch.</span><span class="sxs-lookup"><span data-stu-id="6a783-116">The objective of this section is to outline how to enable the application integration for AirWatch.</span></span>

<span data-ttu-id="6a783-117">**To enable the application integration for AirWatch, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a783-117">**To enable the application integration for AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="6a783-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a783-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6a783-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6a783-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6a783-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6a783-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6a783-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6a783-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="6a783-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6a783-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6a783-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6a783-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="6a783-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="6a783-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6a783-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6a783-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="6a783-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="6a783-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6a783-127">In the **search box**, type **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="6a783-127">In the **search box**, type **AirWatch**.</span></span>
   
   <span data-ttu-id="6a783-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791914.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="6a783-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791914.png "Application Gallery")</span></span>
7. <span data-ttu-id="6a783-129">In the results pane, select **AirWatch**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6a783-129">In the results pane, select **AirWatch**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="6a783-130">![AirWatch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791915.png "AirWatch")</span><span class="sxs-lookup"><span data-stu-id="6a783-130">![AirWatch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791915.png "AirWatch")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="6a783-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a783-131">Configure single sign-on</span></span>

<span data-ttu-id="6a783-132">The objective of this section is to outline how to enable users to authenticate to AirWatch with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="6a783-132">The objective of this section is to outline how to enable users to authenticate to AirWatch with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="6a783-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="6a783-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="6a783-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="6a783-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="6a783-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a783-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="6a783-136">In the Azure classic portal, on the **AirWatch** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a783-136">In the Azure classic portal, on the **AirWatch** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="6a783-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791916.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6a783-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791916.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="6a783-138">On the **How would you like users to sign on to AirWatch** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a783-138">On the **How would you like users to sign on to AirWatch** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6a783-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791917.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6a783-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791917.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="6a783-140">On the **Configure App URL** page, in the **AirWatch Sign On URL** textbox, type your URL used by your users to sign in to your AirWatch application (e.g.: "*https:// companycode.awmdm.com/AirWatch/Login?gid=companycode*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a783-140">On the **Configure App URL** page, in the **AirWatch Sign On URL** textbox, type your URL used by your users to sign in to your AirWatch application (e.g.: "*https:// companycode.awmdm.com/AirWatch/Login?gid=companycode*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="6a783-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791918.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="6a783-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791918.png "Configure App URL")</span></span>
4. <span data-ttu-id="6a783-142">On the **Configure single sign-on at AirWatch** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6a783-142">On the **Configure single sign-on at AirWatch** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="6a783-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791919.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6a783-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791919.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="6a783-144">In a different web browser window, log into your AirWatch company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6a783-144">In a different web browser window, log into your AirWatch company site as an administrator.</span></span>
6. <span data-ttu-id="6a783-145">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span><span class="sxs-lookup"><span data-stu-id="6a783-145">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="6a783-146">![Administrators](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791920.png "Administrators")</span><span class="sxs-lookup"><span data-stu-id="6a783-146">![Administrators](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791920.png "Administrators")</span></span>
7. <span data-ttu-id="6a783-147">Expand the **Settings** menu, and then click **Directory Services**.</span><span class="sxs-lookup"><span data-stu-id="6a783-147">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="6a783-148">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791921.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="6a783-148">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791921.png "Settings")</span></span>
8. <span data-ttu-id="6a783-149">Click the **User** tab, in the **Base DN** textfield, type your domain name, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a783-149">Click the **User** tab, in the **Base DN** textfield, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="6a783-150">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791922.png "User")</span><span class="sxs-lookup"><span data-stu-id="6a783-150">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791922.png "User")</span></span>
9. <span data-ttu-id="6a783-151">Click the **Server** tab.</span><span class="sxs-lookup"><span data-stu-id="6a783-151">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="6a783-152">![Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791923.png "Server")</span><span class="sxs-lookup"><span data-stu-id="6a783-152">![Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791923.png "Server")</span></span>
10. <span data-ttu-id="6a783-153">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a783-153">Perform the following steps:</span></span>
    
   <span data-ttu-id="6a783-154">![Upload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791924.png "Upload")</span><span class="sxs-lookup"><span data-stu-id="6a783-154">![Upload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791924.png "Upload")</span></span>    
    1. <span data-ttu-id="6a783-155">As **Directory Type**, select **None**.</span><span class="sxs-lookup"><span data-stu-id="6a783-155">As **Directory Type**, select **None**.</span></span>
    2. <span data-ttu-id="6a783-156">Select **Use SAML For Authentication**.</span><span class="sxs-lookup"><span data-stu-id="6a783-156">Select **Use SAML For Authentication**.</span></span>
    3. <span data-ttu-id="6a783-157">To upload the downloaded certificate, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="6a783-157">To upload the downloaded certificate, click **Upload**.</span></span>
11. <span data-ttu-id="6a783-158">In the **Request** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a783-158">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="6a783-159">![Request](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791925.png "Request")</span><span class="sxs-lookup"><span data-stu-id="6a783-159">![Request](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791925.png "Request")</span></span>  
    1. <span data-ttu-id="6a783-160">As **Request Binding Type**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="6a783-160">As **Request Binding Type**, select **POST**.</span></span>
    2. <span data-ttu-id="6a783-161">In the Azure classic portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6a783-161">In the Azure classic portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>
    3. <span data-ttu-id="6a783-162">As **NameID Format**, select **Email Address**.</span><span class="sxs-lookup"><span data-stu-id="6a783-162">As **NameID Format**, select **Email Address**.</span></span>
    4. <span data-ttu-id="6a783-163">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a783-163">Click **Save**.</span></span>
12. <span data-ttu-id="6a783-164">Click the **User** tab again.</span><span class="sxs-lookup"><span data-stu-id="6a783-164">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="6a783-165">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791926.png "User")</span><span class="sxs-lookup"><span data-stu-id="6a783-165">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791926.png "User")</span></span>
13. <span data-ttu-id="6a783-166">In the **Attribute** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a783-166">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="6a783-167">![Attribute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791927.png "Attribute")</span><span class="sxs-lookup"><span data-stu-id="6a783-167">![Attribute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791927.png "Attribute")</span></span>
    1. <span data-ttu-id="6a783-168">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="6a783-168">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>
    2. <span data-ttu-id="6a783-169">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="6a783-169">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
    3. <span data-ttu-id="6a783-170">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="6a783-170">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
    4. <span data-ttu-id="6a783-171">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="6a783-171">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
    5. <span data-ttu-id="6a783-172">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="6a783-172">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>
    6. <span data-ttu-id="6a783-173">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="6a783-173">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
    7. <span data-ttu-id="6a783-174">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a783-174">Click **Save**.</span></span>
14. <span data-ttu-id="6a783-175">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a783-175">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="6a783-176">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791928.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6a783-176">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791928.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="6a783-177">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="6a783-177">Configure user provisioning</span></span>

<span data-ttu-id="6a783-178">In order to enable Azure AD users to log into AirWatch, they must be provisioned into AirWatch.</span><span class="sxs-lookup"><span data-stu-id="6a783-178">In order to enable Azure AD users to log into AirWatch, they must be provisioned into AirWatch.</span></span>

* <span data-ttu-id="6a783-179">In the case of AirWatch, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="6a783-179">In the case of AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="6a783-180">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a783-180">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="6a783-181">Log in to your **AirWatch** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="6a783-181">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="6a783-182">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6a783-182">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="6a783-183">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791929.png "Users")</span><span class="sxs-lookup"><span data-stu-id="6a783-183">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791929.png "Users")</span></span>
3. <span data-ttu-id="6a783-184">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="6a783-184">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="6a783-185">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791930.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="6a783-185">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791930.png "Add User")</span></span>
4. <span data-ttu-id="6a783-186">On the **Add / Edit User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a783-186">On the **Add / Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="6a783-187">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791931.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="6a783-187">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791931.png "Add User")</span></span>   
   1. <span data-ttu-id="6a783-188">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="6a783-188">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="6a783-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a783-189">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="6a783-190">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="6a783-190">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="6a783-191">Assign users</span><span class="sxs-lookup"><span data-stu-id="6a783-191">Assign users</span></span>
<span data-ttu-id="6a783-192">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="6a783-192">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="6a783-193">**To assign users to AirWatch, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a783-193">**To assign users to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="6a783-194">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="6a783-194">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6a783-195">On the **AirWatch** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="6a783-195">On the **AirWatch** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6a783-196">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791932.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="6a783-196">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC791932.png "Assign Users")</span></span>
3. <span data-ttu-id="6a783-197">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="6a783-197">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="6a783-198">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="6a783-198">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-airwatch-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6a783-199">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6a783-199">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="6a783-200">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a783-200">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


























