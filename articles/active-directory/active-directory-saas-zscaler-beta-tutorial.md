---
title: 'Tutorial: Azure Active Directory Integration with Zscaler Beta | Microsoft Docs'
description: Learn how to use Zscaler Beta with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 1566ae026b303ffff66a232828d0bcb1299fdaed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553737"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="822d2-103">Tutorial: Azure Active Directory Integration with Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="822d2-103">Tutorial: Azure Active Directory Integration with Zscaler Beta</span></span>
<span data-ttu-id="822d2-104">The objective of this tutorial is to show the integration of Azure and ZScaler Beta.</span><span class="sxs-lookup"><span data-stu-id="822d2-104">The objective of this tutorial is to show the integration of Azure and ZScaler Beta.</span></span>  
<span data-ttu-id="822d2-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="822d2-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="822d2-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="822d2-106">A valid Azure subscription</span></span>
* <span data-ttu-id="822d2-107">A ZScaler Beta single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="822d2-107">A ZScaler Beta single sign-on enabled subscription</span></span>

<span data-ttu-id="822d2-108">After completing this tutorial, the Azure AD users you have assigned to ZScaler Beta will be able to single sign into the application at your ZScaler Beta company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="822d2-108">After completing this tutorial, the Azure AD users you have assigned to ZScaler Beta will be able to single sign into the application at your ZScaler Beta company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="822d2-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="822d2-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="822d2-110">Enabling the application integration for ZScaler Beta</span><span class="sxs-lookup"><span data-stu-id="822d2-110">Enabling the application integration for ZScaler Beta</span></span>
2. <span data-ttu-id="822d2-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="822d2-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="822d2-112">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="822d2-112">Configuring proxy settings</span></span>
4. <span data-ttu-id="822d2-113">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="822d2-113">Configuring user provisioning</span></span>
5. <span data-ttu-id="822d2-114">Assigning users</span><span class="sxs-lookup"><span data-stu-id="822d2-114">Assigning users</span></span>

<span data-ttu-id="822d2-115">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800223.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="822d2-115">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800223.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-zscaler-beta"></a><span data-ttu-id="822d2-116">Enabling the application integration for ZScaler Beta</span><span class="sxs-lookup"><span data-stu-id="822d2-116">Enabling the application integration for ZScaler Beta</span></span>
<span data-ttu-id="822d2-117">The objective of this section is to outline how to enable the application integration for ZScaler Beta.</span><span class="sxs-lookup"><span data-stu-id="822d2-117">The objective of this section is to outline how to enable the application integration for ZScaler Beta.</span></span>

### <a name="to-enable-the-application-integration-for-zscaler-beta-perform-the-following-steps"></a><span data-ttu-id="822d2-118">To enable the application integration for ZScaler Beta, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-118">To enable the application integration for ZScaler Beta, perform the following steps:</span></span>
1. <span data-ttu-id="822d2-119">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="822d2-119">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="822d2-120">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="822d2-120">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="822d2-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="822d2-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="822d2-122">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="822d2-122">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="822d2-123">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="822d2-123">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="822d2-124">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="822d2-124">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="822d2-125">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="822d2-125">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="822d2-126">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="822d2-126">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="822d2-127">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="822d2-127">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="822d2-128">In the **search box**, type **ZScaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="822d2-128">In the **search box**, type **ZScaler Beta**.</span></span>
   
   <span data-ttu-id="822d2-129">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800224.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="822d2-129">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800224.png "Application Gallery")</span></span>
7. <span data-ttu-id="822d2-130">In the results pane, select **ZScaler Beta**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="822d2-130">In the results pane, select **ZScaler Beta**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="822d2-131">![ZScaler One](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800216.png "ZScaler One")</span><span class="sxs-lookup"><span data-stu-id="822d2-131">![ZScaler One](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800216.png "ZScaler One")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="822d2-132">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="822d2-132">Configuring single sign-on</span></span>
<span data-ttu-id="822d2-133">The objective of this section is to outline how to enable users to authenticate to ZScaler Beta with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="822d2-133">The objective of this section is to outline how to enable users to authenticate to ZScaler Beta with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="822d2-134">As part of this procedure, you are required to upload a base-64 encoded certificate to your ZScaler Beta tenant.</span><span class="sxs-lookup"><span data-stu-id="822d2-134">As part of this procedure, you are required to upload a base-64 encoded certificate to your ZScaler Beta tenant.</span></span>  
<span data-ttu-id="822d2-135">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="822d2-135">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="822d2-136">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-136">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="822d2-137">In the Azure classic portal, on the **ZScaler Beta** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="822d2-137">In the Azure classic portal, on the **ZScaler Beta** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="822d2-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800225.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="822d2-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800225.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="822d2-139">On the **How would you like users to sign on to ZScaler Beta** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="822d2-139">On the **How would you like users to sign on to ZScaler Beta** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="822d2-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800226.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="822d2-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800226.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="822d2-141">On the **Configure App URL** page, in the **ZScaler Beta Sign On URL** textbox, type the URL used by your users to sign-on to your ZScaler Beta application, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="822d2-141">On the **Configure App URL** page, in the **ZScaler Beta Sign On URL** textbox, type the URL used by your users to sign-on to your ZScaler Beta application, and then click **Next**.</span></span>
   
   <span data-ttu-id="822d2-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800227.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="822d2-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800227.png "Configure App URL")</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="822d2-143">You can get the actual value for your environment from your ZScaler Beta support team if you need it.</span><span class="sxs-lookup"><span data-stu-id="822d2-143">You can get the actual value for your environment from your ZScaler Beta support team if you need it.</span></span>
   > 
   > 
4. <span data-ttu-id="822d2-144">On the **Configure single sign-on at ZScaler Beta** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="822d2-144">On the **Configure single sign-on at ZScaler Beta** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="822d2-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800228.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="822d2-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800228.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="822d2-146">In a different web browser window, log into your ZScaler Beta company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="822d2-146">In a different web browser window, log into your ZScaler Beta company site as an administrator.</span></span>
6. <span data-ttu-id="822d2-147">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="822d2-147">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="822d2-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="822d2-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800206.png "Administration")</span></span>
7. <span data-ttu-id="822d2-149">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="822d2-149">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>
   
   <span data-ttu-id="822d2-150">![Manage Users & Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800207.png "Manage Users & Authentication")</span><span class="sxs-lookup"><span data-stu-id="822d2-150">![Manage Users & Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800207.png "Manage Users & Authentication")</span></span>
8. <span data-ttu-id="822d2-151">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-151">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>
   
   <span data-ttu-id="822d2-152">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="822d2-152">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800208.png "Authentication")</span></span>
   
   1. <span data-ttu-id="822d2-153">Select **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="822d2-153">Select **Authenticate using SAML Single Sign-On**.</span></span>
   2. <span data-ttu-id="822d2-154">Click **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="822d2-154">Click **Configure SAML Single Sign-On Parameters**.</span></span>
9. <span data-ttu-id="822d2-155">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**:</span><span class="sxs-lookup"><span data-stu-id="822d2-155">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**:</span></span>
   
   <span data-ttu-id="822d2-156">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="822d2-156">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800209.png "Single Sign-On")</span></span>
   
   1. <span data-ttu-id="822d2-157">In the Azure classic portal, on the **Configure single sign-on at ZScaler Beta** dialog page, copy the **Authentication Request URL** value, and then paste it into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span><span class="sxs-lookup"><span data-stu-id="822d2-157">In the Azure classic portal, on the **Configure single sign-on at ZScaler Beta** dialog page, copy the **Authentication Request URL** value, and then paste it into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
   2. <span data-ttu-id="822d2-158">In the **Attribute containing Login Name** textbox, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="822d2-158">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
   3. <span data-ttu-id="822d2-159">To upload your downloaded certificate, click **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="822d2-159">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
   4. <span data-ttu-id="822d2-160">Select **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="822d2-160">Select **Enable SAML Auto-Provisioning**.</span></span>
10. <span data-ttu-id="822d2-161">On the **Configure User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-161">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="822d2-162">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="822d2-162">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800210.png "Administration")</span></span>
    
    1. <span data-ttu-id="822d2-163">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="822d2-163">Click **Save**.</span></span>
    2. <span data-ttu-id="822d2-164">Click **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="822d2-164">Click **Activate Now**.</span></span>
11. <span data-ttu-id="822d2-165">In the Azure classic portal, on the **Configure single sign-on at ZScaler Beta** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="822d2-165">In the Azure classic portal, on the **Configure single sign-on at ZScaler Beta** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="822d2-166">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800229.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="822d2-166">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800229.png "Configure Single Sign-On")</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="822d2-167">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="822d2-167">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="822d2-168">To configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="822d2-168">To configure the proxy settings in Internet Explorer</span></span>
1. <span data-ttu-id="822d2-169">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="822d2-169">Start **Internet Explorer**.</span></span>
2. <span data-ttu-id="822d2-170">Select **Internet options** from the **Tools** menu to open the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="822d2-170">Select **Internet options** from the **Tools** menu to open the **Internet Options** dialog.</span></span>
   
   <span data-ttu-id="822d2-171">![Internet Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC769492.png "Internet Options")</span><span class="sxs-lookup"><span data-stu-id="822d2-171">![Internet Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC769492.png "Internet Options")</span></span>
3. <span data-ttu-id="822d2-172">Click the **Connections** tab.</span><span class="sxs-lookup"><span data-stu-id="822d2-172">Click the **Connections** tab.</span></span>
   
   <span data-ttu-id="822d2-173">![Connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC769493.png "Connections")</span><span class="sxs-lookup"><span data-stu-id="822d2-173">![Connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC769493.png "Connections")</span></span>
4. <span data-ttu-id="822d2-174">Click **LAN settings** to open the **LAN Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="822d2-174">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>
5. <span data-ttu-id="822d2-175">In the Proxy server section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-175">In the Proxy server section, perform the following steps:</span></span>
   
   <span data-ttu-id="822d2-176">![Proxy server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC769494.png "Proxy server")</span><span class="sxs-lookup"><span data-stu-id="822d2-176">![Proxy server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC769494.png "Proxy server")</span></span>
   
   1. <span data-ttu-id="822d2-177">Select Use a proxy server for your LAN.</span><span class="sxs-lookup"><span data-stu-id="822d2-177">Select Use a proxy server for your LAN.</span></span>
   2. <span data-ttu-id="822d2-178">In the Address textbox, type **gateway.zscalerBeta.net**.</span><span class="sxs-lookup"><span data-stu-id="822d2-178">In the Address textbox, type **gateway.zscalerBeta.net**.</span></span>
   3. <span data-ttu-id="822d2-179">In the Port textbox, type **80**.</span><span class="sxs-lookup"><span data-stu-id="822d2-179">In the Port textbox, type **80**.</span></span>
   4. <span data-ttu-id="822d2-180">Select **Bypass proxy server for local addresses**.</span><span class="sxs-lookup"><span data-stu-id="822d2-180">Select **Bypass proxy server for local addresses**.</span></span>
   5. <span data-ttu-id="822d2-181">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="822d2-181">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>
6. <span data-ttu-id="822d2-182">Click **OK** to close the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="822d2-182">Click **OK** to close the **Internet Options** dialog.</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="822d2-183">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="822d2-183">Configuring user provisioning</span></span>
<span data-ttu-id="822d2-184">In order to enable Azure AD users to log into ZScaler Beta, they must be provisioned to ZScaler Beta.</span><span class="sxs-lookup"><span data-stu-id="822d2-184">In order to enable Azure AD users to log into ZScaler Beta, they must be provisioned to ZScaler Beta.</span></span>  
<span data-ttu-id="822d2-185">In the case of ZScaler Beta, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="822d2-185">In the case of ZScaler Beta, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="822d2-186">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-186">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="822d2-187">Log in to your **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="822d2-187">Log in to your **Zscaler** tenant.</span></span>
2. <span data-ttu-id="822d2-188">Click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="822d2-188">Click **Administration**.</span></span>
   
   <span data-ttu-id="822d2-189">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="822d2-189">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781035.png "Administration")</span></span>
3. <span data-ttu-id="822d2-190">Click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="822d2-190">Click **User Management**.</span></span>
   
   <span data-ttu-id="822d2-191">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="822d2-191">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781037.png "Add")</span></span>
4. <span data-ttu-id="822d2-192">In the **Users** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="822d2-192">In the **Users** tab, click **Add**.</span></span>
   
   <span data-ttu-id="822d2-193">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="822d2-193">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781037.png "Add")</span></span>
5. <span data-ttu-id="822d2-194">In the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-194">In the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="822d2-195">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781038.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="822d2-195">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC781038.png "Add User")</span></span>
   
   1. <span data-ttu-id="822d2-196">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="822d2-196">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>
   2. <span data-ttu-id="822d2-197">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="822d2-197">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="822d2-198">You can use any other ZScaler Beta user account creation tools or APIs provided by ZScaler Beta to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="822d2-198">You can use any other ZScaler Beta user account creation tools or APIs provided by ZScaler Beta to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="822d2-199">Assigning users</span><span class="sxs-lookup"><span data-stu-id="822d2-199">Assigning users</span></span>
<span data-ttu-id="822d2-200">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="822d2-200">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-zscaler-beta-perform-the-following-steps"></a><span data-ttu-id="822d2-201">To assign users to ZScaler Beta, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="822d2-201">To assign users to ZScaler Beta, perform the following steps:</span></span>
1. <span data-ttu-id="822d2-202">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="822d2-202">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="822d2-203">On the **ZScaler Beta** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="822d2-203">On the **ZScaler Beta** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="822d2-204">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800230.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="822d2-204">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC800230.png "Assign Users")</span></span>
3. <span data-ttu-id="822d2-205">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="822d2-205">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="822d2-206">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="822d2-206">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscaler-beta-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="822d2-207">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="822d2-207">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="822d2-208">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="822d2-208">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



























