---
title: 'Tutorial: Azure Active Directory integration with Panorama9 | Microsoft Docs'
description: Learn how to use Panorama9 with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: bcb1dc6abf5d87d32ee692e7a2446e1b6f8ec859
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554413"
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="cb8ae-103">Tutorial: Azure Active Directory integration with Panorama9</span><span class="sxs-lookup"><span data-stu-id="cb8ae-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>
<span data-ttu-id="cb8ae-104">The objective of this tutorial is to show the integration of Azure and Panorama9.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-104">The objective of this tutorial is to show the integration of Azure and Panorama9.</span></span>  

<span data-ttu-id="cb8ae-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="cb8ae-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="cb8ae-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="cb8ae-106">A valid Azure subscription</span></span>
* <span data-ttu-id="cb8ae-107">A Panorama9 single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cb8ae-107">A Panorama9 single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="cb8ae-108">After completing this tutorial, the Azure AD users you have assigned to Panorama9 will be able to single sign into the application at your Panorama9 company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb8ae-108">After completing this tutorial, the Azure AD users you have assigned to Panorama9 will be able to single sign into the application at your Panorama9 company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="cb8ae-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cb8ae-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="cb8ae-110">Enabling the application integration for Panorama9</span><span class="sxs-lookup"><span data-stu-id="cb8ae-110">Enabling the application integration for Panorama9</span></span>
2. <span data-ttu-id="cb8ae-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="cb8ae-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="cb8ae-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="cb8ae-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="cb8ae-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="cb8ae-113">Assigning users</span></span>

<span data-ttu-id="cb8ae-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790016.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790016.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-panorama9"></a><span data-ttu-id="cb8ae-115">Enable the application integration for Panorama9</span><span class="sxs-lookup"><span data-stu-id="cb8ae-115">Enable the application integration for Panorama9</span></span>
<span data-ttu-id="cb8ae-116">The objective of this section is to outline how to enable the application integration for Panorama9.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-116">The objective of this section is to outline how to enable the application integration for Panorama9.</span></span>

<span data-ttu-id="cb8ae-117">**To enable the application integration for Panorama9, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb8ae-117">**To enable the application integration for Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="cb8ae-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="cb8ae-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="cb8ae-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="cb8ae-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="cb8ae-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="cb8ae-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="cb8ae-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="cb8ae-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="cb8ae-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="cb8ae-127">In the **search box**, type **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-127">In the **search box**, type **Panorama9**.</span></span>
   
   <span data-ttu-id="cb8ae-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790017.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790017.png "Application Gallery")</span></span>
7. <span data-ttu-id="cb8ae-129">In the results pane, select **Panorama9**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-129">In the results pane, select **Panorama9**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="cb8ae-130">![Panorama9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790018.png "Panorama9")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-130">![Panorama9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790018.png "Panorama9")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="cb8ae-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="cb8ae-131">Configure single sign-on</span></span>

<span data-ttu-id="cb8ae-132">The objective of this section is to outline how to enable users to authenticate to Panorama9 with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-132">The objective of this section is to outline how to enable users to authenticate to Panorama9 with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="cb8ae-133">Configuring SSO for Panorama9 requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-133">Configuring SSO for Panorama9 requires you to retrieve a thumbprint value from a certificate.</span></span>  

<span data-ttu-id="cb8ae-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="cb8ae-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="cb8ae-135">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb8ae-135">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="cb8ae-136">In the Azure classic portal, on the **Panorama9** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-136">In the Azure classic portal, on the **Panorama9** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="cb8ae-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790019.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790019.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="cb8ae-138">On the **How would you like users to sign on to Panorama9** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-138">On the **How would you like users to sign on to Panorama9** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="cb8ae-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790020.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790020.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="cb8ae-140">On the **Configure App URL** page, in the **Panorama9 Sign On URL** textbox, type your URL used by your users to sign in to Panorama9 (e.g.: “*https://dashboard.panorama9.com/saml/access/3262*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-140">On the **Configure App URL** page, in the **Panorama9 Sign On URL** textbox, type your URL used by your users to sign in to Panorama9 (e.g.: “*https://dashboard.panorama9.com/saml/access/3262*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="cb8ae-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790021.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790021.png "Configure App URL")</span></span>
4. <span data-ttu-id="cb8ae-142">On the **Configure single sign-on at Panorama9** page, to download your certificate, click **Download certificate**, and then save it locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-142">On the **Configure single sign-on at Panorama9** page, to download your certificate, click **Download certificate**, and then save it locally on your computer.</span></span>
   
   <span data-ttu-id="cb8ae-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790022.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790022.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="cb8ae-144">In a different web browser window, log into your Panorama9 company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-144">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>
6. <span data-ttu-id="cb8ae-145">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-145">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="cb8ae-146">![Extensions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790023.png "Extensions")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-146">![Extensions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790023.png "Extensions")</span></span>
7. <span data-ttu-id="cb8ae-147">On the **Extensions** dialog, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-147">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="cb8ae-148">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790024.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-148">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="cb8ae-149">In the **Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cb8ae-149">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="cb8ae-150">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790025.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-150">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790025.png "Settings")</span></span>
   
   1. <span data-ttu-id="cb8ae-151">In the Azure classic portal, on the **Configure single sign-on at Panorama9** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-151">In the Azure classic portal, on the **Configure single sign-on at Panorama9** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity provider URL** textbox.</span></span>
   2. <span data-ttu-id="cb8ae-152">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-152">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate fingerprint** textbox.</span></span>    
   
      >[!TIP]
      ><span data-ttu-id="cb8ae-153">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="cb8ae-153">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>
      > 
      
   3. <span data-ttu-id="cb8ae-154">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-154">Click **Save**.</span></span>
9. <span data-ttu-id="cb8ae-155">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-155">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="cb8ae-156">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790026.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-156">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790026.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="cb8ae-157">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="cb8ae-157">Configure user provisioning</span></span>

<span data-ttu-id="cb8ae-158">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-158">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

* <span data-ttu-id="cb8ae-159">In the case of Panorama9, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-159">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="cb8ae-160">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb8ae-160">**To configure user provisioning, perform the following steps:**</span></span>
1. <span data-ttu-id="cb8ae-161">Log in to your **Panorama9** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-161">Log in to your **Panorama9** company site as an administrator.</span></span>
2. <span data-ttu-id="cb8ae-162">In the menu on the top, click **Manage**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-162">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="cb8ae-163">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790027.png "Users")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-163">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790027.png "Users")</span></span>
3. <span data-ttu-id="cb8ae-164">Click **+**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-164">Click **+**.</span></span>
4. <span data-ttu-id="cb8ae-165">In the User data section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cb8ae-165">In the User data section, perform the following steps:</span></span>
   
  <span data-ttu-id="cb8ae-166">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790028.png "Users")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-166">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790028.png "Users")</span></span>

  1. <span data-ttu-id="cb8ae-167">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-167">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>
  2. <span data-ttu-id="cb8ae-168">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-168">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="cb8ae-169">You can use any other Panorama9 user account creation tools or APIs provided by Panorama9 to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-169">You can use any other Panorama9 user account creation tools or APIs provided by Panorama9 to provision AAD user accounts.</span></span>
>
>

## <a name="assign-users"></a><span data-ttu-id="cb8ae-170">Assign users</span><span class="sxs-lookup"><span data-stu-id="cb8ae-170">Assign users</span></span>
<span data-ttu-id="cb8ae-171">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-171">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="cb8ae-172">**To assign users to Panorama9, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb8ae-172">**To assign users to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="cb8ae-173">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-173">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="cb8ae-174">On the **Panorama9** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-174">On the **Panorama9** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="cb8ae-175">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790029.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-175">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC790029.png "Assign Users")</span></span>
3. <span data-ttu-id="cb8ae-176">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-176">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="cb8ae-177">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="cb8ae-177">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panorama9-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="cb8ae-178">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cb8ae-178">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="cb8ae-179">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb8ae-179">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















