---
title: 'Tutorial: Azure Active Directory integration with Zscaler | Microsoft Docs'
description: Learn how to use Zscaler with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 8c5ba50d9eb26ccbf252be6da7e5ac35adae063c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555144"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="9de95-103">Tutorial: Azure Active Directory integration with Zscaler</span><span class="sxs-lookup"><span data-stu-id="9de95-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>
<span data-ttu-id="9de95-104">The objective of this tutorial is to show the integration of Azure and Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9de95-104">The objective of this tutorial is to show the integration of Azure and Zscaler.</span></span> <span data-ttu-id="9de95-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="9de95-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="9de95-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="9de95-106">A valid Azure subscription</span></span>
* <span data-ttu-id="9de95-107">A tenant in Zscaler</span><span class="sxs-lookup"><span data-stu-id="9de95-107">A tenant in Zscaler</span></span>

<span data-ttu-id="9de95-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9de95-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="9de95-109">Enabling the application integration for Zscaler</span><span class="sxs-lookup"><span data-stu-id="9de95-109">Enabling the application integration for Zscaler</span></span>
2. <span data-ttu-id="9de95-110">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="9de95-110">Configuring single sign-on</span></span>
3. <span data-ttu-id="9de95-111">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="9de95-111">Configuring proxy settings</span></span>
4. <span data-ttu-id="9de95-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="9de95-112">Configuring user provisioning</span></span>
5. <span data-ttu-id="9de95-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="9de95-113">Assigning users</span></span>

<span data-ttu-id="9de95-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769226.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="9de95-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769226.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-zscaler"></a><span data-ttu-id="9de95-115">Enabling the application integration for Zscaler</span><span class="sxs-lookup"><span data-stu-id="9de95-115">Enabling the application integration for Zscaler</span></span>
<span data-ttu-id="9de95-116">The objective of this section is to outline how to enable the application integration for Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9de95-116">The objective of this section is to outline how to enable the application integration for Zscaler.</span></span>

### <a name="to-enable-the-application-integration-for-zscaler-perform-the-following-steps"></a><span data-ttu-id="9de95-117">To enable the application integration for Zscaler, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-117">To enable the application integration for Zscaler, perform the following steps:</span></span>
1. <span data-ttu-id="9de95-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9de95-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="9de95-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="9de95-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="9de95-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9de95-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9de95-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9de95-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="9de95-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="9de95-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="9de95-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9de95-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="9de95-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="9de95-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="9de95-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="9de95-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="9de95-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="9de95-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="9de95-127">In the **search box**, type **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="9de95-127">In the **search box**, type **Zscaler**.</span></span>
   
    <span data-ttu-id="9de95-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769227.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="9de95-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769227.png "Application gallery")</span></span>

7. <span data-ttu-id="9de95-129">In the results pane, select **Zscaler**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="9de95-129">In the results pane, select **Zscaler**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="9de95-130">![Zscaler](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769228.png "Zscaler")</span><span class="sxs-lookup"><span data-stu-id="9de95-130">![Zscaler](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769228.png "Zscaler")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="9de95-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="9de95-131">Configuring single sign-on</span></span>
<span data-ttu-id="9de95-132">The objective of this section is to outline how to enable users to authenticate to Zscaler with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="9de95-132">The objective of this section is to outline how to enable users to authenticate to Zscaler with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="9de95-133">As part of this procedure, you are required to upload a certificate to Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9de95-133">As part of this procedure, you are required to upload a certificate to Zscaler.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="9de95-134">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-134">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="9de95-135">In the Azure classic portal, on the **Zscaler** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="9de95-135">In the Azure classic portal, on the **Zscaler** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="9de95-136">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769229.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9de95-136">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769229.png "Enable single sign-on")</span></span>

2. <span data-ttu-id="9de95-137">On the **How would you like users to sign on to Zscaler** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9de95-137">On the **How would you like users to sign on to Zscaler** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="9de95-138">![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769230.png "Configure single sign on")</span><span class="sxs-lookup"><span data-stu-id="9de95-138">![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769230.png "Configure single sign on")</span></span>

3. <span data-ttu-id="9de95-139">On the **Configure App URL** page, in the **Zscaler Sign In URL** textbox, type your sign in URL you got from Zscaler, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="9de95-139">On the **Configure App URL** page, in the **Zscaler Sign In URL** textbox, type your sign in URL you got from Zscaler, and then click **Next**:</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="9de95-140">Please contact the Zscaler support team if you don’t know what your sign in URL is.</span><span class="sxs-lookup"><span data-stu-id="9de95-140">Please contact the Zscaler support team if you don’t know what your sign in URL is.</span></span>
    > 
    > 
   
    <span data-ttu-id="9de95-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769231.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="9de95-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769231.png "Configure app URL")</span></span>

4. <span data-ttu-id="9de95-142">On the **Configure single sign-on at Zscaler** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-142">On the **Configure single sign-on at Zscaler** page, perform the following steps:</span></span>
   
    <span data-ttu-id="9de95-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769232.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9de95-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769232.png "Configure single sign-on")</span></span>
   
    1. <span data-ttu-id="9de95-144">Click **Download certificate**, and then save the certificate file locally as **c:\\Zscaler.cer**.</span><span class="sxs-lookup"><span data-stu-id="9de95-144">Click **Download certificate**, and then save the certificate file locally as **c:\\Zscaler.cer**.</span></span>
    2. <span data-ttu-id="9de95-145">Copy the **Authentication request URL** into your clipboard.</span><span class="sxs-lookup"><span data-stu-id="9de95-145">Copy the **Authentication request URL** into your clipboard.</span></span>

5. <span data-ttu-id="9de95-146">Login to your Zscaler tenant.</span><span class="sxs-lookup"><span data-stu-id="9de95-146">Login to your Zscaler tenant.</span></span>

6. <span data-ttu-id="9de95-147">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="9de95-147">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="9de95-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769486.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="9de95-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769486.png "Administration")</span></span>

7. <span data-ttu-id="9de95-149">Under **Manage Administrators & Roles**, click **Mange Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="9de95-149">Under **Manage Administrators & Roles**, click **Mange Users & Authentication**.</span></span>
   
    <span data-ttu-id="9de95-150">![Manage Administrators & Roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769487.png "Manage Administrators & Roles")</span><span class="sxs-lookup"><span data-stu-id="9de95-150">![Manage Administrators & Roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769487.png "Manage Administrators & Roles")</span></span>

8. <span data-ttu-id="9de95-151">In the **Choose Authentication Option for your Organization** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-151">In the **Choose Authentication Option for your Organization** section, perform the following steps:</span></span>
   
    <span data-ttu-id="9de95-152">![Choose Authentication Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769488.png "Choose Authentication Options")</span><span class="sxs-lookup"><span data-stu-id="9de95-152">![Choose Authentication Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769488.png "Choose Authentication Options")</span></span>
   
    1. <span data-ttu-id="9de95-153">Select **Authenticate using SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9de95-153">Select **Authenticate using SAML Single Sign-on**.</span></span>
    2. <span data-ttu-id="9de95-154">Click **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="9de95-154">Click **Configure SAML Single Sign-On Parameters**.</span></span>

9. <span data-ttu-id="9de95-155">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**:</span><span class="sxs-lookup"><span data-stu-id="9de95-155">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**:</span></span>
   
    <span data-ttu-id="9de95-156">![Upload certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769489.png "Upload certificate")</span><span class="sxs-lookup"><span data-stu-id="9de95-156">![Upload certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769489.png "Upload certificate")</span></span>
   
    1. <span data-ttu-id="9de95-157">In the **URL of the SAML Portal to which users are sent for authentication** textbox, paste the value of the **Authentication request URL** field from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9de95-157">In the **URL of the SAML Portal to which users are sent for authentication** textbox, paste the value of the **Authentication request URL** field from the Azure classic portal.</span></span>
   
    2. <span data-ttu-id="9de95-158">In the **Attribute containing Login Name** textbox, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="9de95-158">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
   
    3. <span data-ttu-id="9de95-159">In the **Upload SSL Public Certificate** field, upload the certificate you have downloaded from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9de95-159">In the **Upload SSL Public Certificate** field, upload the certificate you have downloaded from the Azure classic portal.</span></span>
   
    4. <span data-ttu-id="9de95-160">Select **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="9de95-160">Select **Enable SAML Auto-Provisioning**.</span></span>

10. <span data-ttu-id="9de95-161">On the **Configure User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-161">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="9de95-162">![Configure User Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769490.png "Configure User Authentication")</span><span class="sxs-lookup"><span data-stu-id="9de95-162">![Configure User Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769490.png "Configure User Authentication")</span></span>
    
    1. <span data-ttu-id="9de95-163">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9de95-163">Click **Save**.</span></span>
    2. <span data-ttu-id="9de95-164">Click **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="9de95-164">Click **Activate Now**.</span></span>

11. <span data-ttu-id="9de95-165">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="9de95-165">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="9de95-166">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769491.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9de95-166">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769491.png "Configure single sign-on")</span></span>


## <a name="configuring-proxy-settings"></a><span data-ttu-id="9de95-167">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="9de95-167">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="9de95-168">To configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9de95-168">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="9de95-169">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9de95-169">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="9de95-170">Select **Internet options** from the **Tools** menu to open the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="9de95-170">Select **Internet options** from the **Tools** menu to open the **Internet Options** dialog.</span></span>
   
    <span data-ttu-id="9de95-171">![Internet Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769492.png "Internet Options")</span><span class="sxs-lookup"><span data-stu-id="9de95-171">![Internet Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769492.png "Internet Options")</span></span>

3. <span data-ttu-id="9de95-172">Click the **Connections** tab.</span><span class="sxs-lookup"><span data-stu-id="9de95-172">Click the **Connections** tab.</span></span>
   
    <span data-ttu-id="9de95-173">![Connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769493.png "Connections")</span><span class="sxs-lookup"><span data-stu-id="9de95-173">![Connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769493.png "Connections")</span></span>

4. <span data-ttu-id="9de95-174">Click **LAN settings** to open the **LAN Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="9de95-174">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="9de95-175">In the Proxy server section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-175">In the Proxy server section, perform the following steps:</span></span>
   
    <span data-ttu-id="9de95-176">![Proxy server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769494.png "Proxy server")</span><span class="sxs-lookup"><span data-stu-id="9de95-176">![Proxy server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769494.png "Proxy server")</span></span>
   
    1. <span data-ttu-id="9de95-177">Select Use a proxy server for your LAN.</span><span class="sxs-lookup"><span data-stu-id="9de95-177">Select Use a proxy server for your LAN.</span></span>

    2. <span data-ttu-id="9de95-178">In the Address textbox, type **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="9de95-178">In the Address textbox, type **gateway.zscalertwo.net**.</span></span>
   
    3. <span data-ttu-id="9de95-179">In the Port textbox, type **80**.</span><span class="sxs-lookup"><span data-stu-id="9de95-179">In the Port textbox, type **80**.</span></span>
   
    4. <span data-ttu-id="9de95-180">Select **Bypass proxy server for local addresses**.</span><span class="sxs-lookup"><span data-stu-id="9de95-180">Select **Bypass proxy server for local addresses**.</span></span>
   
    5. <span data-ttu-id="9de95-181">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="9de95-181">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="9de95-182">Click **OK** to close the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="9de95-182">Click **OK** to close the **Internet Options** dialog.</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="9de95-183">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="9de95-183">Configuring user provisioning</span></span>
<span data-ttu-id="9de95-184">In order to enable Azure AD users to log into Zscaler, they must be provisioned into Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9de95-184">In order to enable Azure AD users to log into Zscaler, they must be provisioned into Zscaler.</span></span>  
<span data-ttu-id="9de95-185">In the case of Zscaler, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="9de95-185">In the case of Zscaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="9de95-186">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-186">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="9de95-187">Log in to your **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="9de95-187">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="9de95-188">Click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="9de95-188">Click **Administration**.</span></span>

    <span data-ttu-id="9de95-189">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="9de95-189">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781035.png "Administration")</span></span>

3. <span data-ttu-id="9de95-190">Click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="9de95-190">Click **User Management**.</span></span>
   
    <span data-ttu-id="9de95-191">![User Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781036.png "User Management")</span><span class="sxs-lookup"><span data-stu-id="9de95-191">![User Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781036.png "User Management")</span></span>

4. <span data-ttu-id="9de95-192">In the **Users** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="9de95-192">In the **Users** tab, click **Add**.</span></span>
   
    <span data-ttu-id="9de95-193">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="9de95-193">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781037.png "Add")</span></span>

5. <span data-ttu-id="9de95-194">In the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-194">In the Add User section, perform the following steps:</span></span>
   
    <span data-ttu-id="9de95-195">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781038.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="9de95-195">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC781038.png "Add User")</span></span>
   
    1. <span data-ttu-id="9de95-196">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="9de95-196">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>
   
    2. <span data-ttu-id="9de95-197">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9de95-197">Click **Save**.</span></span>

## <a name="assigning-users"></a><span data-ttu-id="9de95-198">Assigning users</span><span class="sxs-lookup"><span data-stu-id="9de95-198">Assigning users</span></span>
<span data-ttu-id="9de95-199">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="9de95-199">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-zscaler-perform-the-following-steps"></a><span data-ttu-id="9de95-200">To assign users to Zscaler, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9de95-200">To assign users to Zscaler, perform the following steps:</span></span>

1. <span data-ttu-id="9de95-201">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="9de95-201">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="9de95-202">On the **Zscaler** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="9de95-202">On the **Zscaler** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="9de95-203">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769495.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="9de95-203">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC769495.png "Assign users")</span></span>

3. <span data-ttu-id="9de95-204">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="9de95-204">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="9de95-205">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="9de95-205">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="9de95-206">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9de95-206">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="9de95-207">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9de95-207">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



























