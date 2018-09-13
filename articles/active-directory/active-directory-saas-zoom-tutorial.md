---
title: 'Tutorial: Azure Active Directory integration with Zoom | Microsoft Docs'
description: Learn how to use Zoom with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 35592787cb6f236fe3ec5e12ac4f555d5e66979a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672190"
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="d28d8-103">Tutorial: Azure Active Directory integration with Zoom</span><span class="sxs-lookup"><span data-stu-id="d28d8-103">Tutorial: Azure Active Directory integration with Zoom</span></span>
<span data-ttu-id="d28d8-104">The objective of this tutorial is to show the integration of Azure and Zoom.</span><span class="sxs-lookup"><span data-stu-id="d28d8-104">The objective of this tutorial is to show the integration of Azure and Zoom.</span></span>  
<span data-ttu-id="d28d8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="d28d8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d28d8-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d28d8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d28d8-107">A Zoom tenant</span><span class="sxs-lookup"><span data-stu-id="d28d8-107">A Zoom tenant</span></span>

<span data-ttu-id="d28d8-108">After completing this tutorial, the Azure AD users you have assigned to Zoom will be able to single sign into the application at your Zoom company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d28d8-108">After completing this tutorial, the Azure AD users you have assigned to Zoom will be able to single sign into the application at your Zoom company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

<span data-ttu-id="d28d8-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d28d8-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d28d8-110">Enabling the application integration for Zoom</span><span class="sxs-lookup"><span data-stu-id="d28d8-110">Enabling the application integration for Zoom</span></span>
2. <span data-ttu-id="d28d8-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="d28d8-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="d28d8-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="d28d8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d28d8-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="d28d8-113">Assigning users</span></span>

<span data-ttu-id="d28d8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784693.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="d28d8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784693.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-zoom"></a><span data-ttu-id="d28d8-115">Enabling the application integration for Zoom</span><span class="sxs-lookup"><span data-stu-id="d28d8-115">Enabling the application integration for Zoom</span></span>
<span data-ttu-id="d28d8-116">The objective of this section is to outline how to enable the application integration for Zoom.</span><span class="sxs-lookup"><span data-stu-id="d28d8-116">The objective of this section is to outline how to enable the application integration for Zoom.</span></span>

### <a name="to-enable-the-application-integration-for-zoom-perform-the-following-steps"></a><span data-ttu-id="d28d8-117">To enable the application integration for Zoom, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d28d8-117">To enable the application integration for Zoom, perform the following steps:</span></span>
1. <span data-ttu-id="d28d8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d28d8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d28d8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d28d8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d28d8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d28d8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d28d8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="d28d8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="d28d8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d28d8-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d28d8-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="d28d8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="d28d8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d28d8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="d28d8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="d28d8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d28d8-127">In the **search box**, type **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-127">In the **search box**, type **Zoom**.</span></span>
   
   <span data-ttu-id="d28d8-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784694.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="d28d8-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784694.png "Application Gallery")</span></span>
7. <span data-ttu-id="d28d8-129">In the results pane, select **Zoom**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d28d8-129">In the results pane, select **Zoom**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="d28d8-130">![Zoom](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784695.png "Zoom")</span><span class="sxs-lookup"><span data-stu-id="d28d8-130">![Zoom](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784695.png "Zoom")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="d28d8-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="d28d8-131">Configuring single sign-on</span></span>
<span data-ttu-id="d28d8-132">The objective of this section is to outline how to enable users to authenticate to Zoom with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="d28d8-132">The objective of this section is to outline how to enable users to authenticate to Zoom with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="d28d8-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="d28d8-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  
<span data-ttu-id="d28d8-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="d28d8-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="d28d8-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d28d8-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="d28d8-136">In the Azure classic portal, on the **Zoom** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="d28d8-136">In the Azure classic portal, on the **Zoom** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="d28d8-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784696.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d28d8-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784696.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d28d8-138">On the **How would you like users to sign on to Zoom** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-138">On the **How would you like users to sign on to Zoom** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d28d8-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784697.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d28d8-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784697.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="d28d8-140">On the **Configure App URL** page, in the **Zoom Sign In URL** textbox, type your URL using the following pattern "*http://company.zoom.us*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-140">On the **Configure App URL** page, in the **Zoom Sign In URL** textbox, type your URL using the following pattern "*http://company.zoom.us*", and then click **Next**.</span></span>
   
   <span data-ttu-id="d28d8-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784698.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="d28d8-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784698.png "Configure App URL")</span></span>
4. <span data-ttu-id="d28d8-142">On the **Configure single sign-on at Zoom** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d28d8-142">On the **Configure single sign-on at Zoom** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="d28d8-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784699.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d28d8-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784699.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="d28d8-144">In a different web browser window, log into your Zoom company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d28d8-144">In a different web browser window, log into your Zoom company site as an administrator.</span></span>
6. <span data-ttu-id="d28d8-145">Click the **Single Sign-On** tab.</span><span class="sxs-lookup"><span data-stu-id="d28d8-145">Click the **Single Sign-On** tab.</span></span>
   
   <span data-ttu-id="d28d8-146">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d28d8-146">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>
7. <span data-ttu-id="d28d8-147">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span><span class="sxs-lookup"><span data-stu-id="d28d8-147">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>
8. <span data-ttu-id="d28d8-148">In the Single Sign-On section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d28d8-148">In the Single Sign-On section, perform the following steps:</span></span>
   
   <span data-ttu-id="d28d8-149">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d28d8-149">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
   1. <span data-ttu-id="d28d8-150">In the Azure classic portal, on the **Configure single sign-on at Zoom** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d28d8-150">In the Azure classic portal, on the **Configure single sign-on at Zoom** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   2. <span data-ttu-id="d28d8-151">In the Azure classic portal, on the **Configure single sign-on at Zoom** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d28d8-151">In the Azure classic portal, on the **Configure single sign-on at Zoom** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   3. <span data-ttu-id="d28d8-152">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="d28d8-152">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
      > [!TIP]
      > <span data-ttu-id="d28d8-153">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="d28d8-153">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      > 
      > 
   4. <span data-ttu-id="d28d8-154">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="d28d8-154">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox</span></span>
   5. <span data-ttu-id="d28d8-155">In the Azure classic portal, on the **Configure single sign-on at Zoom** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="d28d8-155">In the Azure classic portal, on the **Configure single sign-on at Zoom** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
   6. <span data-ttu-id="d28d8-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-156">Click **Save**.</span></span>
9. <span data-ttu-id="d28d8-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="d28d8-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d28d8-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784702.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d28d8-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784702.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="d28d8-159">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="d28d8-159">Configuring user provisioning</span></span>
<span data-ttu-id="d28d8-160">In order to enable Azure AD users to log into Zoom, they must be provisioned into Zoom.</span><span class="sxs-lookup"><span data-stu-id="d28d8-160">In order to enable Azure AD users to log into Zoom, they must be provisioned into Zoom.</span></span>  
<span data-ttu-id="d28d8-161">In the case of Zoom, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="d28d8-161">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="d28d8-162">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d28d8-162">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="d28d8-163">Log in to your **Zoom** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d28d8-163">Log in to your **Zoom** company site as an administrator.</span></span>
2. <span data-ttu-id="d28d8-164">Click the **Account Management** tab, and then click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-164">Click the **Account Management** tab, and then click **User Management**.</span></span>
3. <span data-ttu-id="d28d8-165">In the User Management section, click **Add users**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-165">In the User Management section, click **Add users**.</span></span>
   
   <span data-ttu-id="d28d8-166">![User management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span><span class="sxs-lookup"><span data-stu-id="d28d8-166">![User management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>
4. <span data-ttu-id="d28d8-167">On the **Add users** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d28d8-167">On the **Add users** page, perform the following steps:</span></span>
   
   <span data-ttu-id="d28d8-168">![Add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span><span class="sxs-lookup"><span data-stu-id="d28d8-168">![Add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
   1. <span data-ttu-id="d28d8-169">As **User Type**, select **Basic**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-169">As **User Type**, select **Basic**.</span></span>
   2. <span data-ttu-id="d28d8-170">In the **Emails** textbox, type the email address of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="d28d8-170">In the **Emails** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   3. <span data-ttu-id="d28d8-171">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-171">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="d28d8-172">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="d28d8-172">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="d28d8-173">Assigning users</span><span class="sxs-lookup"><span data-stu-id="d28d8-173">Assigning users</span></span>
<span data-ttu-id="d28d8-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="d28d8-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-zoom-perform-the-following-steps"></a><span data-ttu-id="d28d8-175">To assign users to Zoom, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d28d8-175">To assign users to Zoom, perform the following steps:</span></span>
1. <span data-ttu-id="d28d8-176">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="d28d8-176">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d28d8-177">On the \*\*Zoom \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="d28d8-177">On the \*\*Zoom \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d28d8-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784705.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="d28d8-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC784705.png "Assign users")</span></span>
3. <span data-ttu-id="d28d8-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="d28d8-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="d28d8-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="d28d8-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoom-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d28d8-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d28d8-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d28d8-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d28d8-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















