---
title: 'Tutorial: Azure Active Directory integration with IdeaScale | Microsoft Docs'
description: Learn how to use IdeaScale with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 3bc8061397256c51b51f8bf816a27eec8d33d7fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550454"
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="7a0b2-103">Tutorial: Azure Active Directory integration with IdeaScale</span><span class="sxs-lookup"><span data-stu-id="7a0b2-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>
<span data-ttu-id="7a0b2-104">The objective of this tutorial is to show the integration of Azure and IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-104">The objective of this tutorial is to show the integration of Azure and IdeaScale.</span></span>  
<span data-ttu-id="7a0b2-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="7a0b2-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="7a0b2-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7a0b2-106">A valid Azure subscription</span></span>
* <span data-ttu-id="7a0b2-107">A IdeaScale single sign-on (SSO)enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7a0b2-107">A IdeaScale single sign-on (SSO)enabled subscription</span></span>

<span data-ttu-id="7a0b2-108">After completing this tutorial, the Azure AD users you have assigned to IdeaScale will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7a0b2-108">After completing this tutorial, the Azure AD users you have assigned to IdeaScale will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="7a0b2-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a0b2-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

*  <span data-ttu-id="7a0b2-110">Enabling the application integration for IdeaScale</span><span class="sxs-lookup"><span data-stu-id="7a0b2-110">Enabling the application integration for IdeaScale</span></span>
*  <span data-ttu-id="7a0b2-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a0b2-111">Configuring single sign-on</span></span>
*  <span data-ttu-id="7a0b2-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="7a0b2-112">Configuring user provisioning</span></span>
*  <span data-ttu-id="7a0b2-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="7a0b2-113">Assigning users</span></span>

<span data-ttu-id="7a0b2-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790838.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790838.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-ideascale"></a><span data-ttu-id="7a0b2-115">Enable the application integration for IdeaScale</span><span class="sxs-lookup"><span data-stu-id="7a0b2-115">Enable the application integration for IdeaScale</span></span>
<span data-ttu-id="7a0b2-116">The objective of this section is to outline how to enable the application integration for IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-116">The objective of this section is to outline how to enable the application integration for IdeaScale.</span></span>

<span data-ttu-id="7a0b2-117">**To enable the application integration for IdeaScale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a0b2-117">**To enable the application integration for IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="7a0b2-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="7a0b2-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="7a0b2-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7a0b2-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="7a0b2-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="7a0b2-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="7a0b2-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="7a0b2-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="7a0b2-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="7a0b2-127">In the **search box**, type **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-127">In the **search box**, type **IdeaScale**.</span></span>
   
   <span data-ttu-id="7a0b2-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790841.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790841.png "Application Gallery")</span></span>
7. <span data-ttu-id="7a0b2-129">In the results pane, select **IdeaScale**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-129">In the results pane, select **IdeaScale**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="7a0b2-130">![IdeaScale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790842.png "IdeaScale")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-130">![IdeaScale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790842.png "IdeaScale")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="7a0b2-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a0b2-131">Configure single sign-on</span></span>

<span data-ttu-id="7a0b2-132">The objective of this section is to outline how to enable users to authenticate to IdeaScale with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-132">The objective of this section is to outline how to enable users to authenticate to IdeaScale with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="7a0b2-133">Configuring single sign-on for IdeaScale requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-133">Configuring single sign-on for IdeaScale requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="7a0b2-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="7a0b2-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="7a0b2-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a0b2-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="7a0b2-136">In the Azure classic portal, on the **IdeaScale** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-136">In the Azure classic portal, on the **IdeaScale** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="7a0b2-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790843.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790843.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="7a0b2-138">On the **How would you like users to sign on to IdeaScale** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-138">On the **How would you like users to sign on to IdeaScale** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="7a0b2-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790844.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790844.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="7a0b2-140">On the **Configure App URL** page, in the **IdeaScale Sign On URL** textbox, type the URL used by your users to sign on to your IdeaScale application (e.g.: "*https://company.IdeaScale.com*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-140">On the **Configure App URL** page, in the **IdeaScale Sign On URL** textbox, type the URL used by your users to sign on to your IdeaScale application (e.g.: "*https://company.IdeaScale.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="7a0b2-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790845.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790845.png "Configure App URL")</span></span>
4. <span data-ttu-id="7a0b2-142">On the **Configure single sign-on at IdeaScale** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-142">On the **Configure single sign-on at IdeaScale** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="7a0b2-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790846.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790846.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="7a0b2-144">In a different web browser window, log into your IdeaScale company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-144">In a different web browser window, log into your IdeaScale company site as an administrator.</span></span>
6. <span data-ttu-id="7a0b2-145">Go to **Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-145">Go to **Community Settings**.</span></span>
   
   <span data-ttu-id="7a0b2-146">![Community Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-146">![Community Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790847.png "Community Settings")</span></span>
7. <span data-ttu-id="7a0b2-147">Go to **Security \> Single Signon Settings**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-147">Go to **Security \> Single Signon Settings**.</span></span>
   
   <span data-ttu-id="7a0b2-148">![Single Signon Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790848.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-148">![Single Signon Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790848.png "Single Signon Settings")</span></span>
8. <span data-ttu-id="7a0b2-149">As **Single-Signon Type**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-149">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
   <span data-ttu-id="7a0b2-150">![Single Signon Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790849.png "Single Signon Type")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-150">![Single Signon Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790849.png "Single Signon Type")</span></span>
9. <span data-ttu-id="7a0b2-151">On the **Single Signon Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a0b2-151">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="7a0b2-152">![Single Signon Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790850.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-152">![Single Signon Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790850.png "Single Signon Settings")</span></span>
   
   1. <span data-ttu-id="7a0b2-153">In the Azure classic portal, on the **Configure single sign-on at IdeaScale** dialog page, copy the **Entity ID** value, and then paste it into the **SAML IdP Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-153">In the Azure classic portal, on the **Configure single sign-on at IdeaScale** dialog page, copy the **Entity ID** value, and then paste it into the **SAML IdP Entity ID** textbox.</span></span>
   2. <span data-ttu-id="7a0b2-154">Copy the content of your downloaded metadata file, and then paste it into the **SAML IdP Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-154">Copy the content of your downloaded metadata file, and then paste it into the **SAML IdP Metadata** textbox.</span></span>
   3. <span data-ttu-id="7a0b2-155">In the Azure classic portal, on the **Configure single sign-on at IdeaScale** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout Success URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-155">In the Azure classic portal, on the **Configure single sign-on at IdeaScale** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout Success URL** textbox.</span></span>
   4. <span data-ttu-id="7a0b2-156">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-156">Click **Save Changes**.</span></span>
10. <span data-ttu-id="7a0b2-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="7a0b2-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790851.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790851.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="7a0b2-159">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="7a0b2-159">Configure user provisioning</span></span>

<span data-ttu-id="7a0b2-160">In order to enable Azure AD users to log into IdeaScale, they must be provisioned into IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-160">In order to enable Azure AD users to log into IdeaScale, they must be provisioned into IdeaScale.</span></span> <span data-ttu-id="7a0b2-161">In the case of IdeaScale, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-161">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="7a0b2-162">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a0b2-162">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7a0b2-163">Log in to your **IdeaScale** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-163">Log in to your **IdeaScale** company site as administrator.</span></span>
2. <span data-ttu-id="7a0b2-164">Go to **Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-164">Go to **Community Settings**.</span></span>
   
   <span data-ttu-id="7a0b2-165">![Community Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-165">![Community Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790847.png "Community Settings")</span></span>
3. <span data-ttu-id="7a0b2-166">Go to **Basic Settings \> Member Management**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-166">Go to **Basic Settings \> Member Management**.</span></span>
4. <span data-ttu-id="7a0b2-167">Click **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-167">Click **Add Member**.</span></span>
   
   <span data-ttu-id="7a0b2-168">![Member Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790852.png "Member Management")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-168">![Member Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790852.png "Member Management")</span></span>
5. <span data-ttu-id="7a0b2-169">In the Add New Member section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a0b2-169">In the Add New Member section, perform the following steps:</span></span>
   
   <span data-ttu-id="7a0b2-170">![Add New Member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790853.png "Add New Member")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-170">![Add New Member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790853.png "Add New Member")</span></span>
   
   1. <span data-ttu-id="7a0b2-171">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-171">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   2. <span data-ttu-id="7a0b2-172">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-172">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="7a0b2-173">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-173">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span>
    >  

>[!NOTE]
><span data-ttu-id="7a0b2-174">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-174">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="7a0b2-175">Assign users</span><span class="sxs-lookup"><span data-stu-id="7a0b2-175">Assign users</span></span>
<span data-ttu-id="7a0b2-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-176">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="7a0b2-177">**To assign users to IdeaScale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a0b2-177">**To assign users to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="7a0b2-178">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-178">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="7a0b2-179">On the **IdeaScale** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-179">On the **IdeaScale** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="7a0b2-180">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790854.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-180">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC790854.png "Assign Users")</span></span>
3. <span data-ttu-id="7a0b2-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-181">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="7a0b2-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="7a0b2-182">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ideascale-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="7a0b2-183">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7a0b2-183">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7a0b2-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7a0b2-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















