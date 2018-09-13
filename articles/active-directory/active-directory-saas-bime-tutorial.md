---
title: 'Tutorial: Azure Active Directory Integration with Bime | Microsoft Docs'
description: Learn how to use Bime with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 212aed469958b7add4b0bf69af945ecb72d674bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554258"
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="4a91d-103">Tutorial: Azure Active Directory Integration with Bime</span><span class="sxs-lookup"><span data-stu-id="4a91d-103">Tutorial: Azure Active Directory Integration with Bime</span></span>
<span data-ttu-id="4a91d-104">The objective of this tutorial is to show the integration of Azure and Bime.</span><span class="sxs-lookup"><span data-stu-id="4a91d-104">The objective of this tutorial is to show the integration of Azure and Bime.</span></span>  
<span data-ttu-id="4a91d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="4a91d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="4a91d-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4a91d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4a91d-107">A Bime tenant</span><span class="sxs-lookup"><span data-stu-id="4a91d-107">A Bime tenant</span></span>

<span data-ttu-id="4a91d-108">After completing this tutorial, the Azure AD users you have assigned to Bime will be able to single sign into the application at your Bime company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a91d-108">After completing this tutorial, the Azure AD users you have assigned to Bime will be able to single sign into the application at your Bime company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4a91d-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4a91d-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="4a91d-110">Enabling the application integration for Bime</span><span class="sxs-lookup"><span data-stu-id="4a91d-110">Enabling the application integration for Bime</span></span>
* <span data-ttu-id="4a91d-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="4a91d-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="4a91d-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="4a91d-112">Configuring user provisioning</span></span>
* <span data-ttu-id="4a91d-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="4a91d-113">Assigning users</span></span>

<span data-ttu-id="4a91d-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775552.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="4a91d-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775552.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-bime"></a><span data-ttu-id="4a91d-115">Enable the application integration for Bime</span><span class="sxs-lookup"><span data-stu-id="4a91d-115">Enable the application integration for Bime</span></span>
<span data-ttu-id="4a91d-116">The objective of this section is to outline how to enable the application integration for Bime.</span><span class="sxs-lookup"><span data-stu-id="4a91d-116">The objective of this section is to outline how to enable the application integration for Bime.</span></span>

<span data-ttu-id="4a91d-117">**To enable the application integration for Bime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a91d-117">**To enable the application integration for Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="4a91d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4a91d-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4a91d-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4a91d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4a91d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4a91d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4a91d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="4a91d-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4a91d-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4a91d-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4a91d-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="4a91d-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="4a91d-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4a91d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="4a91d-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="4a91d-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4a91d-127">In the **search box**, type **Bime**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-127">In the **search box**, type **Bime**.</span></span>
   
   <span data-ttu-id="4a91d-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775553.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="4a91d-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775553.png "Application Gallery")</span></span>
7. <span data-ttu-id="4a91d-129">In the results pane, select **Bime**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4a91d-129">In the results pane, select **Bime**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="4a91d-130">![Bime](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775554.png "Bime")</span><span class="sxs-lookup"><span data-stu-id="4a91d-130">![Bime](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775554.png "Bime")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4a91d-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a91d-131">Configure single sign-on</span></span>

<span data-ttu-id="4a91d-132">The objective of this section is to outline how to enable users to authenticate to Bime with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="4a91d-132">The objective of this section is to outline how to enable users to authenticate to Bime with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="4a91d-133">Configuring SSO for Bime requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="4a91d-133">Configuring SSO for Bime requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="4a91d-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="4a91d-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="4a91d-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a91d-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="4a91d-136">In the Azure classic portal, on the **Bime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a91d-136">In the Azure classic portal, on the **Bime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4a91d-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC771709.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4a91d-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC771709.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="4a91d-138">On the **How would you like users to sign on to Bime** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-138">On the **How would you like users to sign on to Bime** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4a91d-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775555.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a91d-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775555.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="4a91d-140">On the **Configure App URL** page, in the **Bime Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Bimeapp.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-140">On the **Configure App URL** page, in the **Bime Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Bimeapp.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="4a91d-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775556.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="4a91d-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775556.png "Configure App URL")</span></span>
4. <span data-ttu-id="4a91d-142">On the **Configure single sign-on at Bime** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Bime.cer**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-142">On the **Configure single sign-on at Bime** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Bime.cer**.</span></span>
   
   <span data-ttu-id="4a91d-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775557.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a91d-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775557.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="4a91d-144">In a different web browser window, log into your Bime company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4a91d-144">In a different web browser window, log into your Bime company site as an administrator.</span></span>
6. <span data-ttu-id="4a91d-145">In the toolbar, click **Admin**, and then **Account**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-145">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
   <span data-ttu-id="4a91d-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775558.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="4a91d-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775558.png "Admin")</span></span>
7. <span data-ttu-id="4a91d-147">On the account configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a91d-147">On the account configuration page, perform the following steps:</span></span>
   
   <span data-ttu-id="4a91d-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775559.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a91d-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775559.png "Configure Single Sign-On")</span></span>
   
   1. <span data-ttu-id="4a91d-149">Select **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-149">Select **Enable SAML authentication**.</span></span>
   2. <span data-ttu-id="4a91d-150">In the Azure classic portal, on the **Configure single sign-on at Bime** dialog page, copy the **Remote Login URL** value, and then paste it into the **Remote Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4a91d-150">In the Azure classic portal, on the **Configure single sign-on at Bime** dialog page, copy the **Remote Login URL** value, and then paste it into the **Remote Login URL** textbox.</span></span>
   3. <span data-ttu-id="4a91d-151">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="4a91d-151">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span></span>       
      
      >[!TIP]
      ><span data-ttu-id="4a91d-152">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="4a91d-152">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
      > 
   4. <span data-ttu-id="4a91d-153">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-153">Click **Save**.</span></span>
8. <span data-ttu-id="4a91d-154">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a91d-154">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4a91d-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775560.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a91d-155">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775560.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="4a91d-156">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="4a91d-156">Configure user provisioning</span></span>

<span data-ttu-id="4a91d-157">In order to enable Azure AD users to log into Bime, they must be provisioned into Bime.</span><span class="sxs-lookup"><span data-stu-id="4a91d-157">In order to enable Azure AD users to log into Bime, they must be provisioned into Bime.</span></span>  

* <span data-ttu-id="4a91d-158">In the case of Bime, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="4a91d-158">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="4a91d-159">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a91d-159">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="4a91d-160">Log in to your **Bime** tenant.</span><span class="sxs-lookup"><span data-stu-id="4a91d-160">Log in to your **Bime** tenant.</span></span>
2. <span data-ttu-id="4a91d-161">In the toolbar, click **Admin**, and then **Users**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-161">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
   <span data-ttu-id="4a91d-162">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775561.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="4a91d-162">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775561.png "Admin")</span></span>
3. <span data-ttu-id="4a91d-163">In the **Users List**, click **Add New User** (“+”).</span><span class="sxs-lookup"><span data-stu-id="4a91d-163">In the **Users List**, click **Add New User** (“+”).</span></span>
   
   <span data-ttu-id="4a91d-164">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775562.png "Users")</span><span class="sxs-lookup"><span data-stu-id="4a91d-164">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775562.png "Users")</span></span>
4. <span data-ttu-id="4a91d-165">On the **User Details** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a91d-165">On the **User Details** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="4a91d-166">![User Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775563.png "User Details")</span><span class="sxs-lookup"><span data-stu-id="4a91d-166">![User Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775563.png "User Details")</span></span>   
  1. <span data-ttu-id="4a91d-167">Enter the First Name, Last Name, Login, Email of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="4a91d-167">Enter the First Name, Last Name, Login, Email of a valid AAD account you want to provision.</span></span>
  2. <span data-ttu-id="4a91d-168">Click Save.</span><span class="sxs-lookup"><span data-stu-id="4a91d-168">Click Save.</span></span>

>[!NOTE]
><span data-ttu-id="4a91d-169">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="4a91d-169">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="4a91d-170">Assign users</span><span class="sxs-lookup"><span data-stu-id="4a91d-170">Assign users</span></span>
<span data-ttu-id="4a91d-171">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="4a91d-171">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="4a91d-172">**To assign users to Bime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a91d-172">**To assign users to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="4a91d-173">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="4a91d-173">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4a91d-174">On the \*\*Bime \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="4a91d-174">On the \*\*Bime \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4a91d-175">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775564.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="4a91d-175">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC775564.png "Assign users")</span></span>
3. <span data-ttu-id="4a91d-176">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="4a91d-176">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="4a91d-177">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="4a91d-177">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bime-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4a91d-178">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4a91d-178">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="4a91d-179">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a91d-179">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















