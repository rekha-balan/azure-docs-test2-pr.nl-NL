---
title: 'Tutorial: Azure Active Directory integration with Igloo Software | Microsoft Docs'
description: Learn how to use Igloo Software with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: b1309afbb7526801a53e0df2a21ecd239d97c125
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553860"
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="07ecb-103">Tutorial: Azure Active Directory integration with Igloo Software</span><span class="sxs-lookup"><span data-stu-id="07ecb-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>
<span data-ttu-id="07ecb-104">The objective of this tutorial is to show the integration of Azure and Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="07ecb-104">The objective of this tutorial is to show the integration of Azure and Igloo Software.</span></span>  

<span data-ttu-id="07ecb-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="07ecb-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="07ecb-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="07ecb-106">A valid Azure subscription</span></span>
* <span data-ttu-id="07ecb-107">An [Igloo Software](http://www.igloosoftware.com/) Single sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="07ecb-107">An [Igloo Software](http://www.igloosoftware.com/) Single sign on enabled subscription</span></span>

<span data-ttu-id="07ecb-108">After completing this tutorial, the Azure AD users you have assigned to Igloo Software will be able to access the application via single sign-on at your Igloo Software company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07ecb-108">After completing this tutorial, the Azure AD users you have assigned to Igloo Software will be able to access the application via single sign-on at your Igloo Software company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="07ecb-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="07ecb-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="07ecb-110">Enabling the application integration for Igloo Software</span><span class="sxs-lookup"><span data-stu-id="07ecb-110">Enabling the application integration for Igloo Software</span></span>
2. <span data-ttu-id="07ecb-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="07ecb-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="07ecb-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="07ecb-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="07ecb-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="07ecb-113">Assigning users</span></span>

<span data-ttu-id="07ecb-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783961.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="07ecb-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783961.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-igloo-software"></a><span data-ttu-id="07ecb-115">Enable the application integration for Igloo Software</span><span class="sxs-lookup"><span data-stu-id="07ecb-115">Enable the application integration for Igloo Software</span></span>
<span data-ttu-id="07ecb-116">The objective of this section is to outline how to enable the application integration for Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="07ecb-116">The objective of this section is to outline how to enable the application integration for Igloo Software.</span></span>

<span data-ttu-id="07ecb-117">**To enable the application integration for Igloo Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="07ecb-117">**To enable the application integration for Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="07ecb-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="07ecb-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="07ecb-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="07ecb-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="07ecb-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="07ecb-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="07ecb-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="07ecb-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="07ecb-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="07ecb-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="07ecb-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="07ecb-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="07ecb-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="07ecb-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="07ecb-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="07ecb-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="07ecb-127">In the **search box**, type **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-127">In the **search box**, type **Igloo Software**.</span></span>
   
   <span data-ttu-id="07ecb-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783962.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="07ecb-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783962.png "Application Gallery")</span></span>
7. <span data-ttu-id="07ecb-129">In the results pane, select **Igloo Software**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="07ecb-129">In the results pane, select **Igloo Software**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="07ecb-130">![Igloo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783963.png "Igloo")</span><span class="sxs-lookup"><span data-stu-id="07ecb-130">![Igloo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783963.png "Igloo")</span></span>
   
## <a name="configure-sso"></a><span data-ttu-id="07ecb-131">Configure SSO</span><span class="sxs-lookup"><span data-stu-id="07ecb-131">Configure SSO</span></span>

<span data-ttu-id="07ecb-132">The objective of this section is to outline how to enable users to authenticate to Igloo Software with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="07ecb-132">The objective of this section is to outline how to enable users to authenticate to Igloo Software with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="07ecb-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span><span class="sxs-lookup"><span data-stu-id="07ecb-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span> <span data-ttu-id="07ecb-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="07ecb-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="07ecb-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="07ecb-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="07ecb-136">In the Azure classic portal, on the **Igloo Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="07ecb-136">In the Azure classic portal, on the **Igloo Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="07ecb-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783964.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="07ecb-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783964.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="07ecb-138">On the **How would you like users to sign on to Igloo Software** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-138">On the **How would you like users to sign on to Igloo Software** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="07ecb-139">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783965.png "Microsoft Azure AD Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="07ecb-139">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783965.png "Microsoft Azure AD Single Sign-On")</span></span>
3. <span data-ttu-id="07ecb-140">On the **Configure App URL** page, in the **Igloo Software Sign In URL** textbox, type your URL using the following pattern "*https://company.igloocommunities.com/?signin*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-140">On the **Configure App URL** page, in the **Igloo Software Sign In URL** textbox, type your URL using the following pattern "*https://company.igloocommunities.com/?signin*", and then click **Next**.</span></span>
   
   <span data-ttu-id="07ecb-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC773625.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="07ecb-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC773625.png "Configure App URL")</span></span>
4. <span data-ttu-id="07ecb-142">On the **Configure single sign-on at Igloo Software** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="07ecb-142">On the **Configure single sign-on at Igloo Software** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="07ecb-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783966.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="07ecb-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783966.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="07ecb-144">In a different web browser window, log into your Igloo Software company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="07ecb-144">In a different web browser window, log into your Igloo Software company site as an administrator.</span></span>
6. <span data-ttu-id="07ecb-145">Go to the **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-145">Go to the **Control Panel**.</span></span>
   
   <span data-ttu-id="07ecb-146">![Control Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC799949.png "Control Panel")</span><span class="sxs-lookup"><span data-stu-id="07ecb-146">![Control Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC799949.png "Control Panel")</span></span>
7. <span data-ttu-id="07ecb-147">In the **Membership** tab, click **Sign In Settings**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-147">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
   <span data-ttu-id="07ecb-148">![Sign in Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783968.png "Sign in Settings")</span><span class="sxs-lookup"><span data-stu-id="07ecb-148">![Sign in Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783968.png "Sign in Settings")</span></span>
8. <span data-ttu-id="07ecb-149">In the SAML Configuration section, click **Configure SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-149">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
   <span data-ttu-id="07ecb-150">![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783969.png "SAML Configuration")</span><span class="sxs-lookup"><span data-stu-id="07ecb-150">![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783969.png "SAML Configuration")</span></span>
9. <span data-ttu-id="07ecb-151">In the **General Configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="07ecb-151">In the **General Configuration** section, perform the following steps:</span></span>
   
   <span data-ttu-id="07ecb-152">![General Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783970.png "General Configuration")</span><span class="sxs-lookup"><span data-stu-id="07ecb-152">![General Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783970.png "General Configuration")</span></span>
   1. <span data-ttu-id="07ecb-153">In the **Connection Name** textbox, type a custom name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="07ecb-153">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   2. <span data-ttu-id="07ecb-154">In the Azure classic portal, on the **Configure single sign-on at Igloo Software** dialogue page, copy the **Remote Login URL** value, and then paste it into the **IdP Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="07ecb-154">In the Azure classic portal, on the **Configure single sign-on at Igloo Software** dialogue page, copy the **Remote Login URL** value, and then paste it into the **IdP Login URL** textbox.</span></span>
   3. <span data-ttu-id="07ecb-155">In the Azure classic portal, on the **Configure single sign-on at Igloo Software** dialogue page, copy the **Remote Logout URL** value, and then paste it into the **IdP Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="07ecb-155">In the Azure classic portal, on the **Configure single sign-on at Igloo Software** dialogue page, copy the **Remote Logout URL** value, and then paste it into the **IdP Logout URL** textbox.</span></span>
   4. <span data-ttu-id="07ecb-156">As **Logout Response and Request HTTP Type**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-156">As **Logout Response and Request HTTP Type**, select **POST**.</span></span>
   5. <span data-ttu-id="07ecb-157">Create a text file from the downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="07ecb-157">Create a text file from the downloaded certificate.</span></span>    
   
       >[!TIP]
       ><span data-ttu-id="07ecb-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="07ecb-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
       > 
   6. <span data-ttu-id="07ecb-159">Remove the first line and the last line from the text file version of your certificate, copy the remaining certificate text, and then paste it into the **Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="07ecb-159">Remove the first line and the last line from the text file version of your certificate, copy the remaining certificate text, and then paste it into the **Public Certificate** textbox.</span></span>
10. <span data-ttu-id="07ecb-160">In the **Response and Authentication Configuration**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="07ecb-160">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="07ecb-161">![Response and Authentication Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span><span class="sxs-lookup"><span data-stu-id="07ecb-161">![Response and Authentication Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  1. <span data-ttu-id="07ecb-162">As **Identity Provider**, select **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-162">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
  2. <span data-ttu-id="07ecb-163">As **Identifier Type**, select **Email Address**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-163">As **Identifier Type**, select **Email Address**.</span></span>
  3. <span data-ttu-id="07ecb-164">In the **Email Attribute** textbox, type **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-164">In the **Email Attribute** textbox, type **emailaddress**.</span></span>
  4. <span data-ttu-id="07ecb-165">In the **First Name Attribute** textbox, type **givenname**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-165">In the **First Name Attribute** textbox, type **givenname**.</span></span>
  5. <span data-ttu-id="07ecb-166">In the **Last Name Attribute** textbox, type **surname**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-166">In the **Last Name Attribute** textbox, type **surname**.</span></span>
11. <span data-ttu-id="07ecb-167">Preform the following steps to complete the configuration:</span><span class="sxs-lookup"><span data-stu-id="07ecb-167">Preform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="07ecb-168">![User creation on Sign in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span><span class="sxs-lookup"><span data-stu-id="07ecb-168">![User creation on Sign in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span>   
  1. <span data-ttu-id="07ecb-169">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-169">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>
  2. <span data-ttu-id="07ecb-170">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-170">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>
  3. <span data-ttu-id="07ecb-171">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-171">Click **Save**.</span></span>
12. <span data-ttu-id="07ecb-172">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="07ecb-172">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="07ecb-173">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783973.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="07ecb-173">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783973.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="07ecb-174">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="07ecb-174">Configure user provisioning</span></span>

<span data-ttu-id="07ecb-175">There is no action item for you to configure user provisioning to Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="07ecb-175">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="07ecb-176">When an assigned user tries to log into Igloo Software using the access panel, Igloo Software checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="07ecb-176">When an assigned user tries to log into Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="07ecb-177">If there is no user account available yet, it is automatically created by Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="07ecb-177">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

## <a name="assign-users"></a><span data-ttu-id="07ecb-178">Assign users</span><span class="sxs-lookup"><span data-stu-id="07ecb-178">Assign users</span></span>
<span data-ttu-id="07ecb-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="07ecb-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="07ecb-180">**To assign users to Igloo Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="07ecb-180">**To assign users to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="07ecb-181">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="07ecb-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="07ecb-182">On the **Igloo Software** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="07ecb-182">On the **Igloo Software** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="07ecb-183">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783974.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="07ecb-183">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC783974.png "Assign Users")</span></span>
3. <span data-ttu-id="07ecb-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="07ecb-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="07ecb-185">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="07ecb-185">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-igloo-software-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="07ecb-186">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="07ecb-186">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="07ecb-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07ecb-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















