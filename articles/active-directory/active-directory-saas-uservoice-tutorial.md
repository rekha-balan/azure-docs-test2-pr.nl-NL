---
title: 'Tutorial: Azure Active Directory Integration with UserVoice | Microsoft Docs'
description: Learn how to use UserVoice with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0f38add4a23532366839c7f81b313c646f69e937
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550699"
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="5635c-103">Tutorial: Azure Active Directory Integration with UserVoice</span><span class="sxs-lookup"><span data-stu-id="5635c-103">Tutorial: Azure Active Directory Integration with UserVoice</span></span>
<span data-ttu-id="5635c-104">The objective of this tutorial is to show the integration of Azure and UserVoice.</span><span class="sxs-lookup"><span data-stu-id="5635c-104">The objective of this tutorial is to show the integration of Azure and UserVoice.</span></span>  
<span data-ttu-id="5635c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="5635c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5635c-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5635c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5635c-107">A UserVoice tenant</span><span class="sxs-lookup"><span data-stu-id="5635c-107">A UserVoice tenant</span></span>

<span data-ttu-id="5635c-108">After completing this tutorial, the Azure AD users you have assigned to UserVoice will be able to single sign into the application at your UserVoice company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5635c-108">After completing this tutorial, the Azure AD users you have assigned to UserVoice will be able to single sign into the application at your UserVoice company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5635c-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5635c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="5635c-110">Enabling the application integration for UserVoice</span><span class="sxs-lookup"><span data-stu-id="5635c-110">Enabling the application integration for UserVoice</span></span>
2. <span data-ttu-id="5635c-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5635c-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="5635c-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5635c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5635c-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5635c-113">Assigning users</span></span>

<span data-ttu-id="5635c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777514.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="5635c-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777514.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-uservoice"></a><span data-ttu-id="5635c-115">Enabling the application integration for UserVoice</span><span class="sxs-lookup"><span data-stu-id="5635c-115">Enabling the application integration for UserVoice</span></span>
<span data-ttu-id="5635c-116">The objective of this section is to outline how to enable the application integration for UserVoice.</span><span class="sxs-lookup"><span data-stu-id="5635c-116">The objective of this section is to outline how to enable the application integration for UserVoice.</span></span>

### <a name="to-enable-the-application-integration-for-uservoice-perform-the-following-steps"></a><span data-ttu-id="5635c-117">To enable the application integration for UserVoice, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5635c-117">To enable the application integration for UserVoice, perform the following steps:</span></span>
1. <span data-ttu-id="5635c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5635c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="5635c-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5635c-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="5635c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5635c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="5635c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5635c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="5635c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="5635c-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="5635c-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5635c-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="5635c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="5635c-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="5635c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5635c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="5635c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="5635c-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="5635c-127">In the **search box**, type **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="5635c-127">In the **search box**, type **UserVoice**.</span></span>
   
    <span data-ttu-id="5635c-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777513.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="5635c-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777513.png "Application gallery")</span></span>

7. <span data-ttu-id="5635c-129">In the results pane, select **UserVoice**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5635c-129">In the results pane, select **UserVoice**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="5635c-130">![UserVoice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777810.png "UserVoice")</span><span class="sxs-lookup"><span data-stu-id="5635c-130">![UserVoice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777810.png "UserVoice")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="5635c-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5635c-131">Configuring single sign-on</span></span>
<span data-ttu-id="5635c-132">The objective of this section is to outline how to enable users to authenticate to UserVoice with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="5635c-132">The objective of this section is to outline how to enable users to authenticate to UserVoice with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="5635c-133">Configuring single sign-on for UserVoice requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="5635c-133">Configuring single sign-on for UserVoice requires you to retrieve a thumbprint value from a certificate.</span></span>  
<span data-ttu-id="5635c-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="5635c-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="5635c-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5635c-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="5635c-136">In the Azure classic portal, on the **UserVoice** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="5635c-136">In the Azure classic portal, on the **UserVoice** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="5635c-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777515.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5635c-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777515.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5635c-138">On the **How would you like users to sign on to UserVoice** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5635c-138">On the **How would you like users to sign on to UserVoice** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5635c-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777516.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5635c-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777516.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="5635c-140">On the **Configure App URL** page, in the **UserVoice Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.UserVoice.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5635c-140">On the **Configure App URL** page, in the **UserVoice Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.UserVoice.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="5635c-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777517.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="5635c-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777517.png "Configure App URL")</span></span>

4. <span data-ttu-id="5635c-142">On the **Configure single sign-on at UserVoice** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\UserVoice.cer**.</span><span class="sxs-lookup"><span data-stu-id="5635c-142">On the **Configure single sign-on at UserVoice** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\UserVoice.cer**.</span></span>
   
    <span data-ttu-id="5635c-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777518.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5635c-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777518.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="5635c-144">In a different web browser window, log into your UserVoice company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5635c-144">In a different web browser window, log into your UserVoice company site as an administrator.</span></span>

6. <span data-ttu-id="5635c-145">In the toolbar on the top, click Settings, and then select Web portal from the menu.</span><span class="sxs-lookup"><span data-stu-id="5635c-145">In the toolbar on the top, click Settings, and then select Web portal from the menu.</span></span>
   
    <span data-ttu-id="5635c-146">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777519.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="5635c-146">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777519.png "Settings")</span></span>

7. <span data-ttu-id="5635c-147">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page</span><span class="sxs-lookup"><span data-stu-id="5635c-147">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page</span></span>
   
    <span data-ttu-id="5635c-148">![Web portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777520.png "Web portal")</span><span class="sxs-lookup"><span data-stu-id="5635c-148">![Web portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777520.png "Web portal")</span></span>

8. <span data-ttu-id="5635c-149">On the **Edit User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5635c-149">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="5635c-150">![Edit user authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777521.png "Edit user authentication")</span><span class="sxs-lookup"><span data-stu-id="5635c-150">![Edit user authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="5635c-151">a.</span><span class="sxs-lookup"><span data-stu-id="5635c-151">a.</span></span> <span data-ttu-id="5635c-152">Click **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="5635c-152">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="5635c-153">b.</span><span class="sxs-lookup"><span data-stu-id="5635c-153">b.</span></span> <span data-ttu-id="5635c-154">In the Azure classic portal, on the **Configure single sign-on at UserVoice** dialog page, copy the **Remote Login URL** value, and then paste it into the **SSO Remote Sign-In** textbox.</span><span class="sxs-lookup"><span data-stu-id="5635c-154">In the Azure classic portal, on the **Configure single sign-on at UserVoice** dialog page, copy the **Remote Login URL** value, and then paste it into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="5635c-155">c.</span><span class="sxs-lookup"><span data-stu-id="5635c-155">c.</span></span> <span data-ttu-id="5635c-156">In the Azure classic portal, on the **Configure single sign-on at UserVoice** dialog page, copy the **Remote Logout URL** value, and then paste it into the **SSO Remote Sign-Out textbox**.</span><span class="sxs-lookup"><span data-stu-id="5635c-156">In the Azure classic portal, on the **Configure single sign-on at UserVoice** dialog page, copy the **Remote Logout URL** value, and then paste it into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="5635c-157">d.</span><span class="sxs-lookup"><span data-stu-id="5635c-157">d.</span></span> <span data-ttu-id="5635c-158">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Current certificate SHA1 fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="5635c-158">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Current certificate SHA1 fingerprint** textbox.</span></span>  
      
    > [!TIP]
    > <span data-ttu-id="5635c-159">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="5635c-159">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span>
    > 
    > 
  
    <span data-ttu-id="5635c-160">e.</span><span class="sxs-lookup"><span data-stu-id="5635c-160">e.</span></span> <span data-ttu-id="5635c-161">Click **Save authentication settings**.</span><span class="sxs-lookup"><span data-stu-id="5635c-161">Click **Save authentication settings**.</span></span>

9. <span data-ttu-id="5635c-162">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5635c-162">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="5635c-163">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777522.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5635c-163">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777522.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="5635c-164">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5635c-164">Configuring user provisioning</span></span>
<span data-ttu-id="5635c-165">In order to enable Azure AD users to log into UserVoice, they must be provisioned into UserVoice.</span><span class="sxs-lookup"><span data-stu-id="5635c-165">In order to enable Azure AD users to log into UserVoice, they must be provisioned into UserVoice.</span></span>  
<span data-ttu-id="5635c-166">In the case of UserVoice, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="5635c-166">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="5635c-167">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5635c-167">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="5635c-168">Log in to your **UserVoice** tenant.</span><span class="sxs-lookup"><span data-stu-id="5635c-168">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="5635c-169">Go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="5635c-169">Go to **Settings**.</span></span>
   
    <span data-ttu-id="5635c-170">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777811.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="5635c-170">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777811.png "Settings")</span></span>

3. <span data-ttu-id="5635c-171">Click **General**.</span><span class="sxs-lookup"><span data-stu-id="5635c-171">Click **General**.</span></span>

4. <span data-ttu-id="5635c-172">Click **Agents and permissions**.</span><span class="sxs-lookup"><span data-stu-id="5635c-172">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="5635c-173">![Agents and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777812.png "Agents and permissions")</span><span class="sxs-lookup"><span data-stu-id="5635c-173">![Agents and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="5635c-174">Click **Add admins**.</span><span class="sxs-lookup"><span data-stu-id="5635c-174">Click **Add admins**.</span></span>
   
    <span data-ttu-id="5635c-175">![Add admins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777813.png "Add admins")</span><span class="sxs-lookup"><span data-stu-id="5635c-175">![Add admins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777813.png "Add admins")</span></span>

6. <span data-ttu-id="5635c-176">On the **Invite admins** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5635c-176">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="5635c-177">![Invite admins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777814.png "Invite admins")</span><span class="sxs-lookup"><span data-stu-id="5635c-177">![Invite admins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="5635c-178">a.</span><span class="sxs-lookup"><span data-stu-id="5635c-178">a.</span></span> <span data-ttu-id="5635c-179">In the Emails texbox, type the email address of the account you want to provision, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="5635c-179">In the Emails texbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="5635c-180">b.</span><span class="sxs-lookup"><span data-stu-id="5635c-180">b.</span></span> <span data-ttu-id="5635c-181">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="5635c-181">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="5635c-182">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="5635c-182">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="5635c-183">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5635c-183">Assigning users</span></span>
<span data-ttu-id="5635c-184">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="5635c-184">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-uservoice-perform-the-following-steps"></a><span data-ttu-id="5635c-185">To assign users to UserVoice, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5635c-185">To assign users to UserVoice, perform the following steps:</span></span>
1. <span data-ttu-id="5635c-186">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="5635c-186">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5635c-187">On the \*\*UserVoice \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="5635c-187">On the \*\*UserVoice \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="5635c-188">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777523.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="5635c-188">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777523.png "Assign users")</span></span>

3. <span data-ttu-id="5635c-189">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="5635c-189">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="5635c-190">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="5635c-190">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5635c-191">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5635c-191">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5635c-192">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5635c-192">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















