---
title: 'Tutorial: Azure Active Directory integration with Zoho Mail | Microsoft Docs'
description: Learn how to use Zoho Mail with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 93517c52c805240722f04feb0dd43e41116d521b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555631"
---
# <a name="tutorial-azure-active-directory-integration-with-zoho-mail"></a><span data-ttu-id="481d0-103">Tutorial: Azure Active Directory integration with Zoho Mail</span><span class="sxs-lookup"><span data-stu-id="481d0-103">Tutorial: Azure Active Directory integration with Zoho Mail</span></span>
<span data-ttu-id="481d0-104">The objective of this tutorial is to show the integration of Azure and Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="481d0-104">The objective of this tutorial is to show the integration of Azure and Zoho Mail.</span></span>  
<span data-ttu-id="481d0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="481d0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="481d0-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="481d0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="481d0-107">A Zoho Mail tenant</span><span class="sxs-lookup"><span data-stu-id="481d0-107">A Zoho Mail tenant</span></span>

<span data-ttu-id="481d0-108">After completing this tutorial, the Azure AD users you have assigned to Zoho Mail will be able to single sign into the application at your Zoho Mail company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="481d0-108">After completing this tutorial, the Azure AD users you have assigned to Zoho Mail will be able to single sign into the application at your Zoho Mail company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="481d0-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="481d0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="481d0-110">Enabling the application integration for Zoho Mail</span><span class="sxs-lookup"><span data-stu-id="481d0-110">Enabling the application integration for Zoho Mail</span></span>
2. <span data-ttu-id="481d0-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="481d0-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="481d0-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="481d0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="481d0-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="481d0-113">Assigning users</span></span>

<span data-ttu-id="481d0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789600.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="481d0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789600.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-zoho-mail"></a><span data-ttu-id="481d0-115">Enabling the application integration for Zoho Mail</span><span class="sxs-lookup"><span data-stu-id="481d0-115">Enabling the application integration for Zoho Mail</span></span>
<span data-ttu-id="481d0-116">The objective of this section is to outline how to enable the application integration for Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="481d0-116">The objective of this section is to outline how to enable the application integration for Zoho Mail.</span></span>

### <a name="to-enable-the-application-integration-for-zoho-mail-perform-the-following-steps"></a><span data-ttu-id="481d0-117">To enable the application integration for Zoho Mail, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-117">To enable the application integration for Zoho Mail, perform the following steps:</span></span>
1. <span data-ttu-id="481d0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="481d0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="481d0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="481d0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="481d0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="481d0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="481d0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="481d0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="481d0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="481d0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="481d0-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="481d0-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="481d0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="481d0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="481d0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="481d0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="481d0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="481d0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="481d0-127">In the **search box**, type **Zoho Mail**.</span><span class="sxs-lookup"><span data-stu-id="481d0-127">In the **search box**, type **Zoho Mail**.</span></span>
   
    <span data-ttu-id="481d0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789601.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="481d0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789601.png "Application Gallery")</span></span>

7. <span data-ttu-id="481d0-129">In the results pane, select **Zoho Mail**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="481d0-129">In the results pane, select **Zoho Mail**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="481d0-130">![Zoho Mail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789602.png "Zoho Mail")</span><span class="sxs-lookup"><span data-stu-id="481d0-130">![Zoho Mail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789602.png "Zoho Mail")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="481d0-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="481d0-131">Configuring single sign-on</span></span>
<span data-ttu-id="481d0-132">The objective of this section is to outline how to enable users to authenticate to Zoho Mail with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="481d0-132">The objective of this section is to outline how to enable users to authenticate to Zoho Mail with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="481d0-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="481d0-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  
<span data-ttu-id="481d0-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="481d0-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="481d0-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="481d0-136">In the Azure classic portal, on the **Zoho Mail** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="481d0-136">In the Azure classic portal, on the **Zoho Mail** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="481d0-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789603.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="481d0-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789603.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="481d0-138">On the **How would you like users to sign on to Zoho Mail** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="481d0-138">On the **How would you like users to sign on to Zoho Mail** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="481d0-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789604.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="481d0-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789604.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="481d0-140">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-140">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="481d0-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789605.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="481d0-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789605.png "Configure App URL")</span></span>
   
    <span data-ttu-id="481d0-142">a.</span><span class="sxs-lookup"><span data-stu-id="481d0-142">a.</span></span> <span data-ttu-id="481d0-143">In the **Zoho Mail Sign On URL** textbox, type your URL using the following pattern: `http://<company name>.ZohoMail.com`</span><span class="sxs-lookup"><span data-stu-id="481d0-143">In the **Zoho Mail Sign On URL** textbox, type your URL using the following pattern: `http://<company name>.ZohoMail.com`</span></span>
   
    <span data-ttu-id="481d0-144">b.</span><span class="sxs-lookup"><span data-stu-id="481d0-144">b.</span></span> <span data-ttu-id="481d0-145">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="481d0-145">Click **Next**.</span></span>

4. <span data-ttu-id="481d0-146">On the **Configure single sign-on at Zoho Mail** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="481d0-146">On the **Configure single sign-on at Zoho Mail** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="481d0-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789606.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="481d0-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789606.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="481d0-148">In a different web browser window, log into your Zoho Mail company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="481d0-148">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

6. <span data-ttu-id="481d0-149">Go to the **Control panel**.</span><span class="sxs-lookup"><span data-stu-id="481d0-149">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="481d0-150">![Control Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789607.png "Control Panel")</span><span class="sxs-lookup"><span data-stu-id="481d0-150">![Control Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789607.png "Control Panel")</span></span>

7. <span data-ttu-id="481d0-151">Click the **SAML Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="481d0-151">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="481d0-152">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789608.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="481d0-152">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789608.png "SAML Authentication")</span></span>

8. <span data-ttu-id="481d0-153">In the **SAML Authentication Details** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-153">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="481d0-154">![SAML Authentication Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789609.png "SAML Authentication Details")</span><span class="sxs-lookup"><span data-stu-id="481d0-154">![SAML Authentication Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="481d0-155">a.</span><span class="sxs-lookup"><span data-stu-id="481d0-155">a.</span></span> <span data-ttu-id="481d0-156">In the Azure classic portal, on the **Configure single sign-on at Zoho Mail** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="481d0-156">In the Azure classic portal, on the **Configure single sign-on at Zoho Mail** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="481d0-157">b.</span><span class="sxs-lookup"><span data-stu-id="481d0-157">b.</span></span> <span data-ttu-id="481d0-158">In the Azure classic portal, on the **Configure single sign-on at Zoho Mail** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="481d0-158">In the Azure classic portal, on the **Configure single sign-on at Zoho Mail** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="481d0-159">c.</span><span class="sxs-lookup"><span data-stu-id="481d0-159">c.</span></span> <span data-ttu-id="481d0-160">In the Azure classic portal, on the **Configure single sign-on at Zoho Mail** dialog page, copy the **Change Password URL** value, and then paste it into the **Change Password URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="481d0-160">In the Azure classic portal, on the **Configure single sign-on at Zoho Mail** dialog page, copy the **Change Password URL** value, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="481d0-161">d.</span><span class="sxs-lookup"><span data-stu-id="481d0-161">d.</span></span> <span data-ttu-id="481d0-162">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="481d0-162">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
    > [!TIP]
    > <span data-ttu-id="481d0-163">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="481d0-163">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    > 
    > 
   
    <span data-ttu-id="481d0-164">e.</span><span class="sxs-lookup"><span data-stu-id="481d0-164">e.</span></span> <span data-ttu-id="481d0-165">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span><span class="sxs-lookup"><span data-stu-id="481d0-165">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="481d0-166">f.</span><span class="sxs-lookup"><span data-stu-id="481d0-166">f.</span></span> <span data-ttu-id="481d0-167">As **Algorithm**, select **RSA**.</span><span class="sxs-lookup"><span data-stu-id="481d0-167">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="481d0-168">g.</span><span class="sxs-lookup"><span data-stu-id="481d0-168">g.</span></span> <span data-ttu-id="481d0-169">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="481d0-169">Click **OK**.</span></span>

9. <span data-ttu-id="481d0-170">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="481d0-170">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="481d0-171">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789610.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="481d0-171">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789610.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="481d0-172">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="481d0-172">Configuring user provisioning</span></span>
<span data-ttu-id="481d0-173">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="481d0-173">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span>  
<span data-ttu-id="481d0-174">In the case of Zoho Mail, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="481d0-174">In the case of Zoho Mail, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="481d0-175">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-175">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="481d0-176">Log in to your **Zoho Mail** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="481d0-176">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="481d0-177">Go to **Control Panel \> Mail & Docs**.</span><span class="sxs-lookup"><span data-stu-id="481d0-177">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="481d0-178">Go to **User Details \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="481d0-178">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="481d0-179">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789611.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="481d0-179">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789611.png "Add User")</span></span>

4. <span data-ttu-id="481d0-180">On the **Add users** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-180">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="481d0-181">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789612.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="481d0-181">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789612.png "Add User")</span></span>
   
    <span data-ttu-id="481d0-182">a.</span><span class="sxs-lookup"><span data-stu-id="481d0-182">a.</span></span> <span data-ttu-id="481d0-183">Type the **First Name**, **Last Name**, **Email ID**, **Password** of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="481d0-183">Type the **First Name**, **Last Name**, **Email ID**, **Password** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="481d0-184">b.</span><span class="sxs-lookup"><span data-stu-id="481d0-184">b.</span></span> <span data-ttu-id="481d0-185">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="481d0-185">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="481d0-186">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="481d0-186">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>
    > 
    > 

> [!NOTE]
> <span data-ttu-id="481d0-187">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="481d0-187">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="481d0-188">Assigning users</span><span class="sxs-lookup"><span data-stu-id="481d0-188">Assigning users</span></span>
<span data-ttu-id="481d0-189">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="481d0-189">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-zoho-mail-perform-the-following-steps"></a><span data-ttu-id="481d0-190">To assign users to Zoho Mail, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="481d0-190">To assign users to Zoho Mail, perform the following steps:</span></span>
1. <span data-ttu-id="481d0-191">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="481d0-191">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="481d0-192">On the \*\*Zoho Mail \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="481d0-192">On the \*\*Zoho Mail \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="481d0-193">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789613.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="481d0-193">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC789613.png "Assign Users")</span></span>

3. <span data-ttu-id="481d0-194">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="481d0-194">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="481d0-195">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="481d0-195">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zoho-mail-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="481d0-196">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="481d0-196">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="481d0-197">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="481d0-197">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















