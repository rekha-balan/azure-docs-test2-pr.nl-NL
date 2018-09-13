---
title: 'Tutorial: Azure Active Directory integration with Gigya | Microsoft Docs'
description: Learn how to use Gigya with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4bfa9e834c3b9354adf7b889ef3e6e49250a6e9e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661574"
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="76bd7-103">Tutorial: Azure Active Directory integration with Gigya</span><span class="sxs-lookup"><span data-stu-id="76bd7-103">Tutorial: Azure Active Directory integration with Gigya</span></span>
<span data-ttu-id="76bd7-104">The objective of this tutorial is to show the integration of Azure and Gigya.</span><span class="sxs-lookup"><span data-stu-id="76bd7-104">The objective of this tutorial is to show the integration of Azure and Gigya.</span></span>  
<span data-ttu-id="76bd7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="76bd7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="76bd7-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="76bd7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="76bd7-107">A Gigya single sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="76bd7-107">A Gigya single sign on enabled subscription</span></span>

<span data-ttu-id="76bd7-108">After completing this tutorial, the Azure AD users you have assigned to Gigya will be able to single sign into the application at your Gigya company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76bd7-108">After completing this tutorial, the Azure AD users you have assigned to Gigya will be able to single sign into the application at your Gigya company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="76bd7-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="76bd7-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="76bd7-110">Enabling the application integration for Gigya</span><span class="sxs-lookup"><span data-stu-id="76bd7-110">Enabling the application integration for Gigya</span></span>
2. <span data-ttu-id="76bd7-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="76bd7-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="76bd7-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="76bd7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="76bd7-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="76bd7-113">Assigning users</span></span>

<span data-ttu-id="76bd7-114">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789512.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="76bd7-114">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789512.png "Configure Single Sign-On")</span></span>

## <a name="enabling-the-application-integration-for-gigya"></a><span data-ttu-id="76bd7-115">Enabling the application integration for Gigya</span><span class="sxs-lookup"><span data-stu-id="76bd7-115">Enabling the application integration for Gigya</span></span>
<span data-ttu-id="76bd7-116">The objective of this section is to outline how to enable the application integration for Gigya.</span><span class="sxs-lookup"><span data-stu-id="76bd7-116">The objective of this section is to outline how to enable the application integration for Gigya.</span></span>

### <a name="to-enable-the-application-integration-for-gigya-perform-the-following-steps"></a><span data-ttu-id="76bd7-117">To enable the application integration for Gigya, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76bd7-117">To enable the application integration for Gigya, perform the following steps:</span></span>
1. <span data-ttu-id="76bd7-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="76bd7-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="76bd7-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="76bd7-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="76bd7-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="76bd7-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="76bd7-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="76bd7-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="76bd7-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="76bd7-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="76bd7-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="76bd7-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="76bd7-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="76bd7-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="76bd7-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="76bd7-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="76bd7-127">In the **search box**, type **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-127">In the **search box**, type **Gigya**.</span></span>
   
    <span data-ttu-id="76bd7-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789513.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="76bd7-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789513.png "Application Gallery")</span></span>

7. <span data-ttu-id="76bd7-129">In the results pane, select **Gigya**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="76bd7-129">In the results pane, select **Gigya**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="76bd7-130">![Gigya](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789527.png "Gigya")</span><span class="sxs-lookup"><span data-stu-id="76bd7-130">![Gigya](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789527.png "Gigya")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="76bd7-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="76bd7-131">Configuring single sign-on</span></span>

<span data-ttu-id="76bd7-132">The objective of this section is to outline how to enable users to authenticate to Gigya with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="76bd7-132">The objective of this section is to outline how to enable users to authenticate to Gigya with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="76bd7-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="76bd7-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  
<span data-ttu-id="76bd7-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="76bd7-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="76bd7-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76bd7-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="76bd7-136">In the Azure classic portal, on the **Gigya** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="76bd7-136">In the Azure classic portal, on the **Gigya** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="76bd7-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789528.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="76bd7-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789528.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="76bd7-138">On the **How would you like users to sign on to Gigya** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-138">On the **How would you like users to sign on to Gigya** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="76bd7-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789529.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="76bd7-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789529.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="76bd7-140">On the **Configure App URL** page, in the **Gigya Sign On URL** textbox, type your URL using the following pattern "*http://company.gigya.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-140">On the **Configure App URL** page, in the **Gigya Sign On URL** textbox, type your URL using the following pattern "*http://company.gigya.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="76bd7-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789530.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="76bd7-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789530.png "Configure App URL")</span></span>

4. <span data-ttu-id="76bd7-142">On the **Configure single sign-on at Gigya** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="76bd7-142">On the **Configure single sign-on at Gigya** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="76bd7-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789531.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="76bd7-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789531.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="76bd7-144">In a different web browser window, log into your Gigya company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="76bd7-144">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

6. <span data-ttu-id="76bd7-145">Go to **Settings \> SAML Login**, and then click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="76bd7-145">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="76bd7-146">![SAML Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789532.png "SAML Login")</span><span class="sxs-lookup"><span data-stu-id="76bd7-146">![SAML Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789532.png "SAML Login")</span></span>

7. <span data-ttu-id="76bd7-147">In the **SAML Login** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76bd7-147">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="76bd7-148">![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789533.png "SAML Configuration")</span><span class="sxs-lookup"><span data-stu-id="76bd7-148">![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="76bd7-149">a.</span><span class="sxs-lookup"><span data-stu-id="76bd7-149">a.</span></span> <span data-ttu-id="76bd7-150">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="76bd7-150">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="76bd7-151">b.</span><span class="sxs-lookup"><span data-stu-id="76bd7-151">b.</span></span> <span data-ttu-id="76bd7-152">In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="76bd7-152">In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="76bd7-153">c.</span><span class="sxs-lookup"><span data-stu-id="76bd7-153">c.</span></span> <span data-ttu-id="76bd7-154">In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign-On Service URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="76bd7-154">In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign-On Service URL** textbox.</span></span>
   
    <span data-ttu-id="76bd7-155">d.</span><span class="sxs-lookup"><span data-stu-id="76bd7-155">d.</span></span> <span data-ttu-id="76bd7-156">In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Name Identifier Format** value, and then paste it into the **Name ID Format** textbox.</span><span class="sxs-lookup"><span data-stu-id="76bd7-156">In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Name Identifier Format** value, and then paste it into the **Name ID Format** textbox.</span></span>
   
    <span data-ttu-id="76bd7-157">e.</span><span class="sxs-lookup"><span data-stu-id="76bd7-157">e.</span></span> <span data-ttu-id="76bd7-158">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="76bd7-158">Create a **base-64 encoded** file from your downloaded certificate.</span></span>
      
    > [!TIP]
    > <span data-ttu-id="76bd7-159">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="76bd7-159">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    > 
    > 
   
    <span data-ttu-id="76bd7-160">f.</span><span class="sxs-lookup"><span data-stu-id="76bd7-160">f.</span></span> <span data-ttu-id="76bd7-161">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="76bd7-161">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="76bd7-162">g.</span><span class="sxs-lookup"><span data-stu-id="76bd7-162">g.</span></span> <span data-ttu-id="76bd7-163">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-163">Click **Save Settings**.</span></span>

8. <span data-ttu-id="76bd7-164">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="76bd7-164">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="76bd7-165">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789534.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="76bd7-165">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789534.png "Configure Single Sign-On")</span></span>
   
## <a name="configuring-user-provisioning"></a><span data-ttu-id="76bd7-166">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="76bd7-166">Configuring user provisioning</span></span>

<span data-ttu-id="76bd7-167">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span><span class="sxs-lookup"><span data-stu-id="76bd7-167">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="76bd7-168">In the case of Gigya, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="76bd7-168">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="76bd7-169">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76bd7-169">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="76bd7-170">Log in to your **Gigya** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="76bd7-170">Log in to your **Gigya** company site as an administrator.</span></span>
2. <span data-ttu-id="76bd7-171">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-171">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="76bd7-172">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789535.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="76bd7-172">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789535.png "Manage Users")</span></span>

3. <span data-ttu-id="76bd7-173">On the Invite Users dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76bd7-173">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="76bd7-174">![Invite Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789536.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="76bd7-174">![Invite Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="76bd7-175">a.</span><span class="sxs-lookup"><span data-stu-id="76bd7-175">a.</span></span> <span data-ttu-id="76bd7-176">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="76bd7-176">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="76bd7-177">b.</span><span class="sxs-lookup"><span data-stu-id="76bd7-177">b.</span></span> <span data-ttu-id="76bd7-178">Click **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-178">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="76bd7-179">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="76bd7-179">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    > 

 

## <a name="assigning-users"></a><span data-ttu-id="76bd7-180">Assigning users</span><span class="sxs-lookup"><span data-stu-id="76bd7-180">Assigning users</span></span>
<span data-ttu-id="76bd7-181">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="76bd7-181">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-gigya-perform-the-following-steps"></a><span data-ttu-id="76bd7-182">To assign users to Gigya, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76bd7-182">To assign users to Gigya, perform the following steps:</span></span>
1. <span data-ttu-id="76bd7-183">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="76bd7-183">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="76bd7-184">On the \*\*Gigya \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="76bd7-184">On the \*\*Gigya \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="76bd7-185">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789537.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="76bd7-185">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC789537.png "Assign Users")</span></span>

3. <span data-ttu-id="76bd7-186">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="76bd7-186">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="76bd7-187">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="76bd7-187">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gigya-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="76bd7-188">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="76bd7-188">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="76bd7-189">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76bd7-189">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















