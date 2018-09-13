---
title: 'Tutorial: Azure Active Directory integration with Zendesk | Microsoft Docs'
description: Learn how to use Zendesk with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: d8112df1f6290e719b6ecbd647c8da5c45ab81a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564318"
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="1f843-103">Tutorial: Azure Active Directory integration with Zendesk</span><span class="sxs-lookup"><span data-stu-id="1f843-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>
<span data-ttu-id="1f843-104">The objective of this tutorial is to show the integration of Azure and Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1f843-104">The objective of this tutorial is to show the integration of Azure and Zendesk.</span></span>  
<span data-ttu-id="1f843-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="1f843-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1f843-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="1f843-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1f843-107">A Zendesk tenant</span><span class="sxs-lookup"><span data-stu-id="1f843-107">A Zendesk tenant</span></span>

<span data-ttu-id="1f843-108">After completing this tutorial, the Azure AD users you have assigned to Zendesk will be able to single sign into the application at your Zendesk company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f843-108">After completing this tutorial, the Azure AD users you have assigned to Zendesk will be able to single sign into the application at your Zendesk company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="1f843-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1f843-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="1f843-110">Enabling the application integration for Zendesk</span><span class="sxs-lookup"><span data-stu-id="1f843-110">Enabling the application integration for Zendesk</span></span>
2. <span data-ttu-id="1f843-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="1f843-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="1f843-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="1f843-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="1f843-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="1f843-113">Assigning users</span></span>

<span data-ttu-id="1f843-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773083.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="1f843-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773083.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-zendesk"></a><span data-ttu-id="1f843-115">Enabling the application integration for Zendesk</span><span class="sxs-lookup"><span data-stu-id="1f843-115">Enabling the application integration for Zendesk</span></span>
<span data-ttu-id="1f843-116">The objective of this section is to outline how to enable the application integration for Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1f843-116">The objective of this section is to outline how to enable the application integration for Zendesk.</span></span>

### <a name="to-enable-the-application-integration-for-zendesk-perform-the-following-steps"></a><span data-ttu-id="1f843-117">To enable the application integration for Zendesk, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f843-117">To enable the application integration for Zendesk, perform the following steps:</span></span>
1. <span data-ttu-id="1f843-118">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f843-118">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="1f843-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1f843-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="1f843-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1f843-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1f843-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1f843-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="1f843-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="1f843-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="1f843-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1f843-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="1f843-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="1f843-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="1f843-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1f843-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="1f843-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="1f843-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="1f843-127">In the **search box**, type **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="1f843-127">In the **search box**, type **Zendesk**.</span></span>
   
    <span data-ttu-id="1f843-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773084.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="1f843-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773084.png "Application Gallery")</span></span>

7. <span data-ttu-id="1f843-129">In the results pane, select **Zendesk**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1f843-129">In the results pane, select **Zendesk**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="1f843-130">![Zendesk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773085.png "Zendesk")</span><span class="sxs-lookup"><span data-stu-id="1f843-130">![Zendesk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773085.png "Zendesk")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="1f843-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="1f843-131">Configuring single sign-on</span></span>
<span data-ttu-id="1f843-132">The objective of this section is to outline how to enable users to authenticate to Zendesk with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="1f843-132">The objective of this section is to outline how to enable users to authenticate to Zendesk with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="1f843-133">Configuring single sign-on for Zendesk requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="1f843-133">Configuring single sign-on for Zendesk requires you to retrieve a thumbprint value from a certificate.</span></span>  
<span data-ttu-id="1f843-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="1f843-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="1f843-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f843-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="1f843-136">In the Azure AD portal, on the **Zendesk** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="1f843-136">In the Azure AD portal, on the **Zendesk** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="1f843-137">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773086.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1f843-137">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773086.png "Single sign-on")</span></span>

2. <span data-ttu-id="1f843-138">On the **How would you like users to sign on to Zendesk** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1f843-138">On the **How would you like users to sign on to Zendesk** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="1f843-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773087.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1f843-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773087.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="1f843-140">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f843-140">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="1f843-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773088.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="1f843-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773088.png "Configure app URL")</span></span>
   
    <span data-ttu-id="1f843-142">a.</span><span class="sxs-lookup"><span data-stu-id="1f843-142">a.</span></span> <span data-ttu-id="1f843-143">In the **Zendesk Sign In URL** textbox, type your URL using the following pattern: `https://<tenant-name>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="1f843-143">In the **Zendesk Sign In URL** textbox, type your URL using the following pattern: `https://<tenant-name>.zendesk.com`</span></span>
   
    <span data-ttu-id="1f843-144">b.</span><span class="sxs-lookup"><span data-stu-id="1f843-144">b.</span></span> <span data-ttu-id="1f843-145">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1f843-145">Click **Next**.</span></span>

4. <span data-ttu-id="1f843-146">On the **Configure single sign-on at Zendesk** page, click **Download certificate**, and then save the certificate file locally on your compiter.</span><span class="sxs-lookup"><span data-stu-id="1f843-146">On the **Configure single sign-on at Zendesk** page, click **Download certificate**, and then save the certificate file locally on your compiter.</span></span>
   
    <span data-ttu-id="1f843-147">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC777534.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1f843-147">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC777534.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="1f843-148">In a different web browser window, log into your Zendesk company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1f843-148">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

6. <span data-ttu-id="1f843-149">Click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="1f843-149">Click **Admin**.</span></span>

7. <span data-ttu-id="1f843-150">In the left navigation pane, click **Settings**, and then click **Security**.</span><span class="sxs-lookup"><span data-stu-id="1f843-150">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>
   
    <span data-ttu-id="1f843-151">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773089.png "Security")</span><span class="sxs-lookup"><span data-stu-id="1f843-151">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773089.png "Security")</span></span>

8. <span data-ttu-id="1f843-152">On the **Security** page, click the **Admin & Agents** tab.</span><span class="sxs-lookup"><span data-stu-id="1f843-152">On the **Security** page, click the **Admin & Agents** tab.</span></span>

9. <span data-ttu-id="1f843-153">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1f843-153">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

10. <span data-ttu-id="1f843-154">In the Azure AD portal, on the **Configure single sign-on at Zendesk** page, copy the **SAML SSO URL** value, and then paste it into the **SAML SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1f843-154">In the Azure AD portal, on the **Configure single sign-on at Zendesk** page, copy the **SAML SSO URL** value, and then paste it into the **SAML SSO URL** textbox.</span></span>

11. <span data-ttu-id="1f843-155">In the Azure AD portal, on the **Configure single sign-on at Zendesk** page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="1f843-155">In the Azure AD portal, on the **Configure single sign-on at Zendesk** page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.</span></span>
    
    <span data-ttu-id="1f843-156">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773090.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1f843-156">![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773090.png "Single sign-on")</span></span>

12. <span data-ttu-id="1f843-157">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="1f843-157">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.</span></span>
    
    > [!TIP]
    > <span data-ttu-id="1f843-158">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="1f843-158">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span>
    > 
    > 

13. <span data-ttu-id="1f843-159">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1f843-159">Click **Save**.</span></span>

14. <span data-ttu-id="1f843-160">On the Azure AD portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="1f843-160">On the Azure AD portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="1f843-161">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773093.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1f843-161">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773093.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="1f843-162">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="1f843-162">Configuring user provisioning</span></span>
<span data-ttu-id="1f843-163">In order to enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="1f843-163">In order to enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="1f843-164">In the case of **Zendesk**, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="1f843-164">In the case of **Zendesk**, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-to-zendesk-perform-the-following-steps"></a><span data-ttu-id="1f843-165">To provision a user account to Zendesk, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f843-165">To provision a user account to Zendesk, perform the following steps:</span></span>
1. <span data-ttu-id="1f843-166">Log in to your **Zendesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="1f843-166">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="1f843-167">Select the **Customer List** tab.</span><span class="sxs-lookup"><span data-stu-id="1f843-167">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="1f843-168">Select the **User** tab, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1f843-168">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="1f843-169">![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773632.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="1f843-169">![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773632.png "Add user")</span></span>
4. <span data-ttu-id="1f843-170">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1f843-170">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="1f843-171">![New user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773633.png "New user")</span><span class="sxs-lookup"><span data-stu-id="1f843-171">![New user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="1f843-172">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="1f843-172">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="1f843-173">Assigning users</span><span class="sxs-lookup"><span data-stu-id="1f843-173">Assigning users</span></span>
<span data-ttu-id="1f843-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="1f843-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-zendesk-perform-the-following-steps"></a><span data-ttu-id="1f843-175">To assign users to Zendesk, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f843-175">To assign users to Zendesk, perform the following steps:</span></span>
1. <span data-ttu-id="1f843-176">In the Azure AD portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="1f843-176">In the Azure AD portal, create a test account.</span></span>

2. <span data-ttu-id="1f843-177">On the \*\*Zendesk \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="1f843-177">On the \*\*Zendesk \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="1f843-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773094.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="1f843-178">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773094.png "Assign users")</span></span>

3. <span data-ttu-id="1f843-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="1f843-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="1f843-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="1f843-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1f843-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1f843-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1f843-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f843-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















