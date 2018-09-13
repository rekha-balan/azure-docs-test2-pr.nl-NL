---
title: 'Tutorial: Azure Active Directory Integration with Picturepark | Microsoft Docs'
description: Learn how to use Picturepark with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: f8ef6b0353ab670140404e0dd5758e2693c40ddf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548848"
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="875fc-103">Tutorial: Azure Active Directory Integration with Picturepark</span><span class="sxs-lookup"><span data-stu-id="875fc-103">Tutorial: Azure Active Directory Integration with Picturepark</span></span>
<span data-ttu-id="875fc-104">The objective of this tutorial is to show the integration of Azure and Picturepark.</span><span class="sxs-lookup"><span data-stu-id="875fc-104">The objective of this tutorial is to show the integration of Azure and Picturepark.</span></span>  

<span data-ttu-id="875fc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="875fc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="875fc-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="875fc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="875fc-107">A Picturepark tenant</span><span class="sxs-lookup"><span data-stu-id="875fc-107">A Picturepark tenant</span></span>

<span data-ttu-id="875fc-108">After completing this tutorial, the Azure AD users you have assigned to Picturepark will be able to single sign into the application at your Picturepark company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="875fc-108">After completing this tutorial, the Azure AD users you have assigned to Picturepark will be able to single sign into the application at your Picturepark company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="875fc-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="875fc-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="875fc-110">Enabling the application integration for Picturepark</span><span class="sxs-lookup"><span data-stu-id="875fc-110">Enabling the application integration for Picturepark</span></span>
2. <span data-ttu-id="875fc-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="875fc-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="875fc-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="875fc-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="875fc-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="875fc-113">Assigning users</span></span>

<span data-ttu-id="875fc-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795055.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="875fc-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795055.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-picturepark"></a><span data-ttu-id="875fc-115">Enable the application integration for Picturepark</span><span class="sxs-lookup"><span data-stu-id="875fc-115">Enable the application integration for Picturepark</span></span>
<span data-ttu-id="875fc-116">The objective of this section is to outline how to enable the application integration for Picturepark.</span><span class="sxs-lookup"><span data-stu-id="875fc-116">The objective of this section is to outline how to enable the application integration for Picturepark.</span></span>

<span data-ttu-id="875fc-117">**To enable the application integration for Picturepark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="875fc-117">**To enable the application integration for Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="875fc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="875fc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="875fc-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="875fc-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="875fc-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="875fc-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="875fc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="875fc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="875fc-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="875fc-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="875fc-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="875fc-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="875fc-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="875fc-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="875fc-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="875fc-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="875fc-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="875fc-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="875fc-127">In the **search box**, type **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="875fc-127">In the **search box**, type **Picturepark**.</span></span>
   
   <span data-ttu-id="875fc-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795056.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="875fc-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795056.png "Application Gallery")</span></span>
7. <span data-ttu-id="875fc-129">In the results pane, select **Picturepark**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="875fc-129">In the results pane, select **Picturepark**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="875fc-130">![Picturepark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795057.png "Picturepark")</span><span class="sxs-lookup"><span data-stu-id="875fc-130">![Picturepark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795057.png "Picturepark")</span></span>


## <a name="configure-single-sign-on"></a><span data-ttu-id="875fc-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="875fc-131">Configure single sign-on</span></span>

<span data-ttu-id="875fc-132">The objective of this section is to outline how to enable users to authenticate to Picturepark with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="875fc-132">The objective of this section is to outline how to enable users to authenticate to Picturepark with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="875fc-133">Configuring SSO for Picturepark requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="875fc-133">Configuring SSO for Picturepark requires you to retrieve a thumbprint value from a certificate.</span></span>  

<span data-ttu-id="875fc-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)..</span><span class="sxs-lookup"><span data-stu-id="875fc-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)..</span></span>

<span data-ttu-id="875fc-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="875fc-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="875fc-136">In the Azure classic portal, on the **Picturepark** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="875fc-136">In the Azure classic portal, on the **Picturepark** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="875fc-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795058.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="875fc-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795058.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="875fc-138">On the **How would you like users to sign on to Picturepark** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="875fc-138">On the **How would you like users to sign on to Picturepark** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="875fc-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795059.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="875fc-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795059.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="875fc-140">On the **Configure App URL** page, in the **Picturepark Sign On URL** textbox, type your URL using the following pattern "*http://company.picturepark.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="875fc-140">On the **Configure App URL** page, in the **Picturepark Sign On URL** textbox, type your URL using the following pattern "*http://company.picturepark.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="875fc-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795060.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="875fc-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795060.png "Configure App URL")</span></span>
4. <span data-ttu-id="875fc-142">On the **Configure single sign-on at Picturepark** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="875fc-142">On the **Configure single sign-on at Picturepark** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="875fc-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795061.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="875fc-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795061.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="875fc-144">In a different web browser window, log into your Picturepark company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="875fc-144">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>
6. <span data-ttu-id="875fc-145">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span><span class="sxs-lookup"><span data-stu-id="875fc-145">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
   <span data-ttu-id="875fc-146">![Management Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795062.png "Management Console")</span><span class="sxs-lookup"><span data-stu-id="875fc-146">![Management Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795062.png "Management Console")</span></span>
7. <span data-ttu-id="875fc-147">Click **Authentication**, and then click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="875fc-147">Click **Authentication**, and then click **Identity providers**.</span></span>
   
   <span data-ttu-id="875fc-148">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795063.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="875fc-148">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795063.png "Authentication")</span></span>
8. <span data-ttu-id="875fc-149">In the **Identity provider configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="875fc-149">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
   <span data-ttu-id="875fc-150">![Identity provider configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795064.png "Identity provider configuration")</span><span class="sxs-lookup"><span data-stu-id="875fc-150">![Identity provider configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795064.png "Identity provider configuration")</span></span>
   
   1. <span data-ttu-id="875fc-151">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="875fc-151">Click **Add**.</span></span>
   2. <span data-ttu-id="875fc-152">Type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="875fc-152">Type a name for your configuration.</span></span>
   3. <span data-ttu-id="875fc-153">Select **Set as default**.</span><span class="sxs-lookup"><span data-stu-id="875fc-153">Select **Set as default**.</span></span>
   4. <span data-ttu-id="875fc-154">In the Azure classic portal, on the **Configure single sign-on at Picturepark** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Issuer URI** textbox.</span><span class="sxs-lookup"><span data-stu-id="875fc-154">In the Azure classic portal, on the **Configure single sign-on at Picturepark** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Issuer URI** textbox.</span></span>
   5. <span data-ttu-id="875fc-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Trusted Issuer Thumb Print** textbox.</span><span class="sxs-lookup"><span data-stu-id="875fc-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Trusted Issuer Thumb Print** textbox.</span></span>  
      
      >[!TIP]
      ><span data-ttu-id="875fc-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="875fc-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>
      >
      >

9. <span data-ttu-id="875fc-157">Click **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="875fc-157">Click **JoinDefaultUsersGroup**.</span></span>
10. <span data-ttu-id="875fc-158">To set the **Emailaddress** attribute in the **Claim** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="875fc-158">To set the **Emailaddress** attribute in the **Claim** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress** and click **Save**.</span></span>

      <span data-ttu-id="875fc-159">![Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795065.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="875fc-159">![Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795065.png "Configuration")</span></span>
11. <span data-ttu-id="875fc-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="875fc-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="875fc-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795066.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="875fc-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795066.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="875fc-162">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="875fc-162">Configure user provisioning</span></span>
<span data-ttu-id="875fc-163">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span><span class="sxs-lookup"><span data-stu-id="875fc-163">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span>  

 * <span data-ttu-id="875fc-164">In the case of Picturepark, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="875fc-164">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="875fc-165">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="875fc-165">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="875fc-166">Log in to your **Picturepark** tenant.</span><span class="sxs-lookup"><span data-stu-id="875fc-166">Log in to your **Picturepark** tenant.</span></span>
2. <span data-ttu-id="875fc-167">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="875fc-167">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
   <span data-ttu-id="875fc-168">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795067.png "Users")</span><span class="sxs-lookup"><span data-stu-id="875fc-168">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795067.png "Users")</span></span>
3. <span data-ttu-id="875fc-169">In the **Users overview** tab, click **New**.</span><span class="sxs-lookup"><span data-stu-id="875fc-169">In the **Users overview** tab, click **New**.</span></span>
   
   <span data-ttu-id="875fc-170">![User management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795068.png "User management")</span><span class="sxs-lookup"><span data-stu-id="875fc-170">![User management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795068.png "User management")</span></span>
4. <span data-ttu-id="875fc-171">On the **Create User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="875fc-171">On the **Create User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="875fc-172">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795069.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="875fc-172">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795069.png "Create User")</span></span>
   
  1. <span data-ttu-id="875fc-173">Type the : **Email Address**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Company**, **Country**, **ZIP**, **City** of a valid Azure Active Directory User you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="875fc-173">Type the : **Email Address**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Company**, **Country**, **ZIP**, **City** of a valid Azure Active Directory User you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="875fc-174">Select a **Language**.</span><span class="sxs-lookup"><span data-stu-id="875fc-174">Select a **Language**.</span></span>
  3. <span data-ttu-id="875fc-175">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="875fc-175">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="875fc-176">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="875fc-176">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="875fc-177">Assign users</span><span class="sxs-lookup"><span data-stu-id="875fc-177">Assign users</span></span>
<span data-ttu-id="875fc-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="875fc-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="875fc-179">**To assign users to Picturepark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="875fc-179">**To assign users to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="875fc-180">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="875fc-180">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="875fc-181">On the **Picturepark** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="875fc-181">On the **Picturepark** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="875fc-182">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795070.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="875fc-182">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC795070.png "Assign Users")</span></span>
3. <span data-ttu-id="875fc-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="875fc-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="875fc-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="875fc-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-picturepark-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="875fc-185">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="875fc-185">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="875fc-186">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="875fc-186">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















