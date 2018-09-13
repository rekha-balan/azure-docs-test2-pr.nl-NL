---
title: 'Tutorial: Azure Active Directory Integration with Cisco Webex | Microsoft Docs'
description: Learn how to use Cisco Webex with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: bb313e1afb2351659c7a44ce47de24527cc9a307
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555102"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="f527f-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f527f-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="f527f-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="f527f-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="f527f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="f527f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="f527f-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f527f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f527f-107">A Cisco Webex tenant</span><span class="sxs-lookup"><span data-stu-id="f527f-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="f527f-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f527f-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="f527f-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f527f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="f527f-110">Enabling the application integration for Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f527f-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="f527f-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="f527f-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="f527f-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="f527f-112">Configuring user provisioning</span></span>
* <span data-ttu-id="f527f-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="f527f-113">Assigning users</span></span>

<span data-ttu-id="f527f-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="f527f-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="f527f-115">Enable the application integration for Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f527f-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="f527f-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="f527f-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="f527f-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f527f-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="f527f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f527f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="f527f-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f527f-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f527f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f527f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f527f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f527f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="f527f-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="f527f-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f527f-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f527f-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="f527f-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="f527f-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f527f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f527f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="f527f-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="f527f-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f527f-127">In the **search box**, type **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="f527f-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="f527f-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="f527f-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="f527f-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f527f-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="f527f-130">![Cisco Webex](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="f527f-130">![Cisco Webex](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f527f-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="f527f-131">Configure single sign-on</span></span>

<span data-ttu-id="f527f-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="f527f-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="f527f-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span><span class="sxs-lookup"><span data-stu-id="f527f-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="f527f-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f527f-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="f527f-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f527f-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="f527f-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="f527f-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="f527f-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f527f-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="f527f-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f527f-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="f527f-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f527f-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="f527f-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f527f-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="f527f-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="f527f-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="f527f-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="f527f-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="f527f-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="f527f-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="f527f-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f527f-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="f527f-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f527f-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="f527f-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f527f-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="f527f-147">In the menu on the top, click **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="f527f-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="f527f-148">![Site Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span><span class="sxs-lookup"><span data-stu-id="f527f-148">![Site Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="f527f-149">In the **Manage Site** section, click **SSO Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f527f-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="f527f-150">![SSO Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="f527f-150">![SSO Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="f527f-151">In the Federated Web SSO Configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f527f-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="f527f-152">![Federated SSO Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="f527f-152">![Federated SSO Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="f527f-153">From the **Federation Protocol** list, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f527f-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="f527f-154">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="f527f-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="f527f-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f527f-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="f527f-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span><span class="sxs-lookup"><span data-stu-id="f527f-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="f527f-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span><span class="sxs-lookup"><span data-stu-id="f527f-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="f527f-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span><span class="sxs-lookup"><span data-stu-id="f527f-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="f527f-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f527f-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="f527f-160">From the **NameID Format** list, select **Email address**.</span><span class="sxs-lookup"><span data-stu-id="f527f-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="f527f-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="f527f-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="f527f-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f527f-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="f527f-163">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="f527f-163">Click **Update**.</span></span>
9. <span data-ttu-id="f527f-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f527f-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="f527f-165">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f527f-165">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="f527f-166">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="f527f-166">Configure user provisioning</span></span>

<span data-ttu-id="f527f-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="f527f-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="f527f-168">In the case of Cisco Webex, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f527f-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="f527f-169">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f527f-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="f527f-170">Log in to your **Cisco Webex** tenant.</span><span class="sxs-lookup"><span data-stu-id="f527f-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="f527f-171">Go to **Manage Users \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="f527f-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="f527f-172">![Add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span><span class="sxs-lookup"><span data-stu-id="f527f-172">![Add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="f527f-173">On the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f527f-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="f527f-174">![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="f527f-174">![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="f527f-175">As **Account Type**, select **Host**.</span><span class="sxs-lookup"><span data-stu-id="f527f-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="f527f-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span><span class="sxs-lookup"><span data-stu-id="f527f-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="f527f-177">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f527f-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="f527f-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="f527f-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="f527f-179">Assign users</span><span class="sxs-lookup"><span data-stu-id="f527f-179">Assign users</span></span>
<span data-ttu-id="f527f-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="f527f-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="f527f-181">**To assign users to Cisco Webex, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f527f-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="f527f-182">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="f527f-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f527f-183">On the **Cisco Webex** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="f527f-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f527f-184">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="f527f-184">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="f527f-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="f527f-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="f527f-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="f527f-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f527f-187">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f527f-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f527f-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f527f-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















