---
title: 'Tutorial: Azure Active Directory integration with Jitbit Helpdesk | Microsoft Docs'
description: Learn how to use Jitbit Helpdesk with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 1b5f9614709eb8dbee00adfeba5332096461f4a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564487"
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="3c9db-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="3c9db-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>
<span data-ttu-id="3c9db-104">The objective of this tutorial is to show the integration of Azure and Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3c9db-104">The objective of this tutorial is to show the integration of Azure and Jitbit Helpdesk.</span></span>  

<span data-ttu-id="3c9db-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="3c9db-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="3c9db-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="3c9db-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3c9db-107">A Jitbit Helpdesk tenant</span><span class="sxs-lookup"><span data-stu-id="3c9db-107">A Jitbit Helpdesk tenant</span></span>

<span data-ttu-id="3c9db-108">After completing this tutorial, the Azure AD users you have assigned to Jitbit Helpdesk will be able to single sign into the application at your Jitbit Helpdesk company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c9db-108">After completing this tutorial, the Azure AD users you have assigned to Jitbit Helpdesk will be able to single sign into the application at your Jitbit Helpdesk company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="3c9db-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3c9db-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="3c9db-110">Enabling the application integration for Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="3c9db-110">Enabling the application integration for Jitbit Helpdesk</span></span>
* <span data-ttu-id="3c9db-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="3c9db-111">Configuring single sign-on</span></span>
* <span data-ttu-id="3c9db-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="3c9db-112">Configuring user provisioning</span></span>
* <span data-ttu-id="3c9db-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="3c9db-113">Assigning users</span></span>

<span data-ttu-id="3c9db-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777676.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="3c9db-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777676.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-jitbit-helpdesk"></a><span data-ttu-id="3c9db-115">Enabling the application integration for Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="3c9db-115">Enabling the application integration for Jitbit Helpdesk</span></span>
<span data-ttu-id="3c9db-116">The objective of this section is to outline how to enable the application integration for Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3c9db-116">The objective of this section is to outline how to enable the application integration for Jitbit Helpdesk.</span></span>

### <a name="to-enable-the-application-integration-for-jitbit-helpdesk-perform-the-following-steps"></a><span data-ttu-id="3c9db-117">To enable the application integration for Jitbit Helpdesk, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3c9db-117">To enable the application integration for Jitbit Helpdesk, perform the following steps:</span></span>
1. <span data-ttu-id="3c9db-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3c9db-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3c9db-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3c9db-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3c9db-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3c9db-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3c9db-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="3c9db-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="3c9db-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3c9db-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3c9db-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="3c9db-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="3c9db-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3c9db-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="3c9db-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="3c9db-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3c9db-127">In the **search box**, type **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-127">In the **search box**, type **Jitbit Helpdesk**.</span></span>
   
   <span data-ttu-id="3c9db-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777677.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="3c9db-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777677.png "Application Gallery")</span></span>
7. <span data-ttu-id="3c9db-129">In the results pane, select **Jitbit Helpdesk**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3c9db-129">In the results pane, select **Jitbit Helpdesk**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="3c9db-130">![JitBit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC781008.png "JitBit")</span><span class="sxs-lookup"><span data-stu-id="3c9db-130">![JitBit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC781008.png "JitBit")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="3c9db-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="3c9db-131">Configure single sign-on</span></span>

<span data-ttu-id="3c9db-132">The objective of this section is to outline how to enable users to authenticate to Jitbit Helpdesk with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="3c9db-132">The objective of this section is to outline how to enable users to authenticate to Jitbit Helpdesk with their account in Azure AD using federation based on the SAML protocol.</span></span> <span data-ttu-id="3c9db-133">.</span><span class="sxs-lookup"><span data-stu-id="3c9db-133">.</span></span>  

<span data-ttu-id="3c9db-134">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="3c9db-134">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="3c9db-135">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="3c9db-135">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

>[!IMPORTANT]
><span data-ttu-id="3c9db-136">In order to be able to configure single sign-on on your Jitbit Helpdesk tenant, you need to contact first the Jitbit Helpdesk technical support to get this feature enabled.</span><span class="sxs-lookup"><span data-stu-id="3c9db-136">In order to be able to configure single sign-on on your Jitbit Helpdesk tenant, you need to contact first the Jitbit Helpdesk technical support to get this feature enabled.</span></span> 
> 

<span data-ttu-id="3c9db-137">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3c9db-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="3c9db-138">In the Azure classic portal, on the **Jitbit Helpdesk** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="3c9db-138">In the Azure classic portal, on the **Jitbit Helpdesk** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="3c9db-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777678.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3c9db-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777678.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="3c9db-140">On the **How would you like users to sign on to Jitbit Helpdesk** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-140">On the **How would you like users to sign on to Jitbit Helpdesk** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3c9db-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777679.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3c9db-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777679.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="3c9db-142">On the **Configure App URL** page, in the **Jitbit Helpdesk Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Jitbit.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-142">On the **Configure App URL** page, in the **Jitbit Helpdesk Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Jitbit.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="3c9db-143">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777528.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="3c9db-143">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777528.png "Configure app URL")</span></span>
4. <span data-ttu-id="3c9db-144">On the **Configure single sign-on at Jitbit Helpdesk** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Jitbit Helpdesk.cer**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-144">On the **Configure single sign-on at Jitbit Helpdesk** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Jitbit Helpdesk.cer**.</span></span>
   
   <span data-ttu-id="3c9db-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777680.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3c9db-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777680.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="3c9db-146">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3c9db-146">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>
6. <span data-ttu-id="3c9db-147">In the toolbar on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-147">In the toolbar on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="3c9db-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777681.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="3c9db-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777681.png "Administration")</span></span>
7. <span data-ttu-id="3c9db-149">Click **General settings**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-149">Click **General settings**.</span></span>
   
   <span data-ttu-id="3c9db-150">![Users, companies and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777682.png "Users, companies and permissions")</span><span class="sxs-lookup"><span data-stu-id="3c9db-150">![Users, companies and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777682.png "Users, companies and permissions")</span></span>
8. <span data-ttu-id="3c9db-151">In the **Authentication settings** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3c9db-151">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="3c9db-152">![Authentication settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777683.png "Authentication settings")</span><span class="sxs-lookup"><span data-stu-id="3c9db-152">![Authentication settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777683.png "Authentication settings")</span></span>
   
   1. <span data-ttu-id="3c9db-153">Select **Enable SAML 2.0 single sign on** sign-in using Single Sign-On (SSO) with **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-153">Select **Enable SAML 2.0 single sign on** sign-in using Single Sign-On (SSO) with **OneLogin**.</span></span>
   2. <span data-ttu-id="3c9db-154">In the Azure classic portal, on the **Configure single sign-on at Jitbit Helpdesk** dialogue page, copy the **Service Provider (SP) initiated endpoint** value, and then paste it into the **EndPoint URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3c9db-154">In the Azure classic portal, on the **Configure single sign-on at Jitbit Helpdesk** dialogue page, copy the **Service Provider (SP) initiated endpoint** value, and then paste it into the **EndPoint URL** textbox.</span></span>
   3. <span data-ttu-id="3c9db-155">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="3c9db-155">Create a **base-64 encoded** file from your downloaded certificate.</span></span> 
      >[!TIP]
      ><span data-ttu-id="3c9db-156">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="3c9db-156">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span> 
      > 
   4. <span data-ttu-id="3c9db-157">Open your base-64 encoded certificate, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="3c9db-157">Open your base-64 encoded certificate, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   5. <span data-ttu-id="3c9db-158">Click **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-158">Click **Save changes**.</span></span>
9. <span data-ttu-id="3c9db-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="3c9db-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3c9db-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777684.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3c9db-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777684.png "Configure single sign-on")</span></span>
   
## <a name="configuring-user-provisioning"></a><span data-ttu-id="3c9db-161">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="3c9db-161">Configuring user provisioning</span></span>

<span data-ttu-id="3c9db-162">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3c9db-162">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="3c9db-163">In the case of Jitbit Helpdesk, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3c9db-163">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="3c9db-164">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3c9db-164">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="3c9db-165">Log in to your **Jitbit Helpdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="3c9db-165">Log in to your **Jitbit Helpdesk** tenant.</span></span>
2. <span data-ttu-id="3c9db-166">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-166">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="3c9db-167">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777681.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="3c9db-167">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777681.png "Administration")</span></span>
3. <span data-ttu-id="3c9db-168">Click **Users, companies and permissions**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-168">Click **Users, companies and permissions**.</span></span>
   
   <span data-ttu-id="3c9db-169">![Users, companies and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777682.png "Users, companies and permissions")</span><span class="sxs-lookup"><span data-stu-id="3c9db-169">![Users, companies and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777682.png "Users, companies and permissions")</span></span>
4. <span data-ttu-id="3c9db-170">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-170">Click **Add user**.</span></span>
   
   <span data-ttu-id="3c9db-171">![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777685.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="3c9db-171">![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777685.png "Add user")</span></span>
5. <span data-ttu-id="3c9db-172">In the Create section, type the data of the Azure AD account you want to provision into the following textboxes: **Username**, **Email**, **First Name**, **Last Name**</span><span class="sxs-lookup"><span data-stu-id="3c9db-172">In the Create section, type the data of the Azure AD account you want to provision into the following textboxes: **Username**, **Email**, **First Name**, **Last Name**</span></span>
   
   <span data-ttu-id="3c9db-173">![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777686.png "Create")</span><span class="sxs-lookup"><span data-stu-id="3c9db-173">![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777686.png "Create")</span></span>
6. <span data-ttu-id="3c9db-174">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-174">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="3c9db-175">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="3c9db-175">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision AAD user accounts.</span></span>
> 

## <a name="assign-users"></a><span data-ttu-id="3c9db-176">Assign users</span><span class="sxs-lookup"><span data-stu-id="3c9db-176">Assign users</span></span>
<span data-ttu-id="3c9db-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="3c9db-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="3c9db-178">**To assign users to Jitbit Helpdesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3c9db-178">**To assign users to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="3c9db-179">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="3c9db-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3c9db-180">On the **Jitbit Helpdesk** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="3c9db-180">On the **Jitbit Helpdesk** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3c9db-181">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777687.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="3c9db-181">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC777687.png "Assign users")</span></span>
3. <span data-ttu-id="3c9db-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="3c9db-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="3c9db-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="3c9db-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jitbit-helpdesk-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3c9db-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3c9db-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3c9db-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c9db-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















