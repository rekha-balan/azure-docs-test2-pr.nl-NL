---
title: 'Tutorial: Azure Active Directory integration with BlueJeans | Microsoft Docs'
description: Learn how to use BlueJeans with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 47099ad7ccae49435ba92ec66f7b573a3673900d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553749"
---
# <a name="tutorial-azure-ad-integration-with-bluejeans"></a><span data-ttu-id="71b9c-103">Tutorial: Azure AD Integration with BlueJeans</span><span class="sxs-lookup"><span data-stu-id="71b9c-103">Tutorial: Azure AD Integration with BlueJeans</span></span>
<span data-ttu-id="71b9c-104">The objective of this tutorial is to show the integration of Azure and BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="71b9c-104">The objective of this tutorial is to show the integration of Azure and BlueJeans.</span></span>  

<span data-ttu-id="71b9c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="71b9c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="71b9c-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="71b9c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="71b9c-107">A BlueJeans single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="71b9c-107">A BlueJeans single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="71b9c-108">After completing this tutorial, the Azure AD users you have assigned to BlueJeans will be able to single sign into the application at your BlueJeans company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71b9c-108">After completing this tutorial, the Azure AD users you have assigned to BlueJeans will be able to single sign into the application at your BlueJeans company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="71b9c-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="71b9c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="71b9c-110">Enabling the application integration for BlueJeans</span><span class="sxs-lookup"><span data-stu-id="71b9c-110">Enabling the application integration for BlueJeans</span></span>
* <span data-ttu-id="71b9c-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="71b9c-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="71b9c-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="71b9c-112">Configuring user provisioning</span></span>
* <span data-ttu-id="71b9c-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="71b9c-113">Assigning users</span></span>

<span data-ttu-id="71b9c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785860.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="71b9c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785860.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-bluejeans"></a><span data-ttu-id="71b9c-115">Enable the application integration for BlueJeans</span><span class="sxs-lookup"><span data-stu-id="71b9c-115">Enable the application integration for BlueJeans</span></span>
<span data-ttu-id="71b9c-116">The objective of this section is to outline how to enable the application integration for BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="71b9c-116">The objective of this section is to outline how to enable the application integration for BlueJeans.</span></span>

<span data-ttu-id="71b9c-117">**To enable the application integration for BlueJeans, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71b9c-117">**To enable the application integration for BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="71b9c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="71b9c-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="71b9c-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="71b9c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="71b9c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="71b9c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="71b9c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="71b9c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="71b9c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="71b9c-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="71b9c-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="71b9c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="71b9c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="71b9c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="71b9c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="71b9c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="71b9c-127">In the **search box**, type **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-127">In the **search box**, type **BlueJeans**.</span></span>
   
   <span data-ttu-id="71b9c-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785861.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="71b9c-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785861.png "Application Gallery")</span></span>
7. <span data-ttu-id="71b9c-129">In the results pane, select **BlueJeans**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="71b9c-129">In the results pane, select **BlueJeans**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="71b9c-130">![BlueJeans](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785862.png "BlueJeans")</span><span class="sxs-lookup"><span data-stu-id="71b9c-130">![BlueJeans](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785862.png "BlueJeans")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="71b9c-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="71b9c-131">Configure single sign-on</span></span>

<span data-ttu-id="71b9c-132">The objective of this section is to outline how to enable users to authenticate to BlueJeans with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="71b9c-132">The objective of this section is to outline how to enable users to authenticate to BlueJeans with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="71b9c-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71b9c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="71b9c-134">In the Azure classic portal, on the **BlueJeans** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="71b9c-134">In the Azure classic portal, on the **BlueJeans** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="71b9c-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785863.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="71b9c-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785863.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="71b9c-136">On the **How would you like users to sign on to BlueJeans** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-136">On the **How would you like users to sign on to BlueJeans** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="71b9c-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785864.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="71b9c-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785864.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="71b9c-138">On the **Configure App URL** page, in the **BlueJeans Sign On URL** textbox, type your URL using the following pattern "*https://company.BlueJeans.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-138">On the **Configure App URL** page, in the **BlueJeans Sign On URL** textbox, type your URL using the following pattern "*https://company.BlueJeans.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="71b9c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785865.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="71b9c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785865.png "Configure App URL")</span></span>
4. <span data-ttu-id="71b9c-140">On the **Configure single sign-on at BlueJeans** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="71b9c-140">On the **Configure single sign-on at BlueJeans** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="71b9c-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785866.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="71b9c-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785866.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="71b9c-142">In a different web browser window, log into your **BlueJeans** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="71b9c-142">In a different web browser window, log into your **BlueJeans** company site as an administrator.</span></span>
6. <span data-ttu-id="71b9c-143">Go to **ADMIN \> Group Settings \> Security**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-143">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="71b9c-144">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="71b9c-144">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>
7. <span data-ttu-id="71b9c-145">In the **Security** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71b9c-145">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="71b9c-146">![SAML Single Sign On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="71b9c-146">![SAML Single Sign On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   1. <span data-ttu-id="71b9c-147">Select **SAML Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-147">Select **SAML Single Sign On**.</span></span>
   2. <span data-ttu-id="71b9c-148">Select **Enable automatic provisioning**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-148">Select **Enable automatic provisioning**.</span></span>
8. <span data-ttu-id="71b9c-149">Move on with the following steps:</span><span class="sxs-lookup"><span data-stu-id="71b9c-149">Move on with the following steps:</span></span>
   
   <span data-ttu-id="71b9c-150">![Certificate Path](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span><span class="sxs-lookup"><span data-stu-id="71b9c-150">![Certificate Path](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
   
   1. <span data-ttu-id="71b9c-151">Click **Choose File**, and then upload the downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="71b9c-151">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   2. <span data-ttu-id="71b9c-152">In the Azure classic portal, on the **Configure single sign-on at BlueJeans** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="71b9c-152">In the Azure classic portal, on the **Configure single sign-on at BlueJeans** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   3. <span data-ttu-id="71b9c-153">In the Azure classic portal, on the **Configure single sign-on at BlueJeans** dialog page, copy the **Change Password URL** value, and then paste it into the **Password Change URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="71b9c-153">In the Azure classic portal, on the **Configure single sign-on at BlueJeans** dialog page, copy the **Change Password URL** value, and then paste it into the **Password Change URL** textbox.</span></span>
   4. <span data-ttu-id="71b9c-154">In the Azure classic portal, on the **Configure single sign-on at BlueJeans** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="71b9c-154">In the Azure classic portal, on the **Configure single sign-on at BlueJeans** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
9. <span data-ttu-id="71b9c-155">Move on with the following steps:</span><span class="sxs-lookup"><span data-stu-id="71b9c-155">Move on with the following steps:</span></span>
   
   <span data-ttu-id="71b9c-156">![Save Changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span><span class="sxs-lookup"><span data-stu-id="71b9c-156">![Save Changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
   1. <span data-ttu-id="71b9c-157">In the **User id** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-157">In the **User id** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span></span>
   2. <span data-ttu-id="71b9c-158">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-158">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span></span>
   3. <span data-ttu-id="71b9c-159">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-159">Click **Save Changes**.</span></span>
10. <span data-ttu-id="71b9c-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="71b9c-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="71b9c-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785876.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="71b9c-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785876.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="71b9c-162">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="71b9c-162">Configure user provisioning</span></span>

<span data-ttu-id="71b9c-163">In order to enable Azure AD users to log into BlueJeans, they must be provisioned into BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="71b9c-163">In order to enable Azure AD users to log into BlueJeans, they must be provisioned into BlueJeans.</span></span>  

* <span data-ttu-id="71b9c-164">In the case of BlueJeans, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="71b9c-164">In the case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="71b9c-165">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71b9c-165">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="71b9c-166">Log in to your **BlueJeans** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="71b9c-166">Log in to your **BlueJeans** company site as an administrator.</span></span>
2. <span data-ttu-id="71b9c-167">Go to **ADMIN \> Manage Users \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-167">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="71b9c-168">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="71b9c-168">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="71b9c-169">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span><span class="sxs-lookup"><span data-stu-id="71b9c-169">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   > 
3. <span data-ttu-id="71b9c-170">In the **Add User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71b9c-170">In the **Add User** section, perform the following steps:</span></span>
   
  <span data-ttu-id="71b9c-171">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="71b9c-171">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
   
  1. <span data-ttu-id="71b9c-172">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="71b9c-172">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="71b9c-173">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-173">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="71b9c-174">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="71b9c-174">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="71b9c-175">Assign users</span><span class="sxs-lookup"><span data-stu-id="71b9c-175">Assign users</span></span>
<span data-ttu-id="71b9c-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="71b9c-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="71b9c-177">**To assign users to BlueJeans, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71b9c-177">**To assign users to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="71b9c-178">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="71b9c-178">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="71b9c-179">On the **BlueJeans** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="71b9c-179">On the **BlueJeans** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="71b9c-180">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785887.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="71b9c-180">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC785887.png "Assign Users")</span></span>
3. <span data-ttu-id="71b9c-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="71b9c-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="71b9c-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="71b9c-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bluejeans-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="71b9c-183">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="71b9c-183">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="71b9c-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71b9c-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















