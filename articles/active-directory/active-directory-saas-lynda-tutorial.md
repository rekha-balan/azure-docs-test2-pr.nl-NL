---
title: 'Tutorial: Azure Active Directory integration with Lynda.com | Microsoft Docs'
description: Learn how to use Lynda.com with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/22/2017
ms.author: jeedes
ms.openlocfilehash: a3c89710d28564a193dac86c9cdf3f59f938310f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563131"
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="142a0-103">Tutorial: Azure Active Directory integration with Lynda.com</span><span class="sxs-lookup"><span data-stu-id="142a0-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>
<span data-ttu-id="142a0-104">The objective of this tutorial is to show the integration of Azure and Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="142a0-104">The objective of this tutorial is to show the integration of Azure and Lynda.com.</span></span>  

<span data-ttu-id="142a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="142a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="142a0-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="142a0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="142a0-107">A Lynda.com tenant</span><span class="sxs-lookup"><span data-stu-id="142a0-107">A Lynda.com tenant</span></span>

<span data-ttu-id="142a0-108">After completing this tutorial, the Azure AD users you have assigned to Lynda.com will be able to single sign into the application at your Lynda.com company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="142a0-108">After completing this tutorial, the Azure AD users you have assigned to Lynda.com will be able to single sign into the application at your Lynda.com company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="142a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="142a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="142a0-110">Enabling the application integration for Lynda.com</span><span class="sxs-lookup"><span data-stu-id="142a0-110">Enabling the application integration for Lynda.com</span></span>
2. <span data-ttu-id="142a0-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="142a0-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="142a0-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="142a0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="142a0-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="142a0-113">Assigning users</span></span>

<span data-ttu-id="142a0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC781046.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="142a0-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC781046.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-lyndacom"></a><span data-ttu-id="142a0-115">Enable the application integration for Lynda.com</span><span class="sxs-lookup"><span data-stu-id="142a0-115">Enable the application integration for Lynda.com</span></span>
<span data-ttu-id="142a0-116">The objective of this section is to outline how to enable the application integration for Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="142a0-116">The objective of this section is to outline how to enable the application integration for Lynda.com.</span></span>

<span data-ttu-id="142a0-117">**To enable the application integration for Lynda.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="142a0-117">**To enable the application integration for Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="142a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="142a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="142a0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="142a0-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="142a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="142a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="142a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="142a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="142a0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="142a0-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="142a0-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="142a0-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="142a0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="142a0-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="142a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="142a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="142a0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="142a0-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="142a0-127">In the **search box**, type **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="142a0-127">In the **search box**, type **Lynda.com**.</span></span>
   
   <span data-ttu-id="142a0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777524.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="142a0-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777524.png "Application Gallery")</span></span>
7. <span data-ttu-id="142a0-129">In the results pane, select **Lynda.com**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="142a0-129">In the results pane, select **Lynda.com**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="142a0-130">![Lynda.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777525.png "Lynda.com")</span><span class="sxs-lookup"><span data-stu-id="142a0-130">![Lynda.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777525.png "Lynda.com")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="142a0-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="142a0-131">Configure single sign-on</span></span>

<span data-ttu-id="142a0-132">The objective of this section is to outline how to enable users to authenticate to Lynda.com with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="142a0-132">The objective of this section is to outline how to enable users to authenticate to Lynda.com with their account in Azure AD using federation based on the SAML protocol.</span></span>

>[!IMPORTANT]
><span data-ttu-id="142a0-133">In order to be able to configure single sign-on on your Lynda.com tenant, you need to contact first the Lynda.com technical support to get this feature enabled.</span><span class="sxs-lookup"><span data-stu-id="142a0-133">In order to be able to configure single sign-on on your Lynda.com tenant, you need to contact first the Lynda.com technical support to get this feature enabled.</span></span> 
> 

<span data-ttu-id="142a0-134">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="142a0-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="142a0-135">In the Azure classic portal, on the **Lynda.com** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="142a0-135">In the Azure classic portal, on the **Lynda.com** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="142a0-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777526.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="142a0-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777526.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="142a0-137">On the **How would you like users to sign on to Lynda.com** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="142a0-137">On the **How would you like users to sign on to Lynda.com** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="142a0-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777527.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="142a0-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777527.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="142a0-139">On the **Configure App URL** page, in the **Lynda.com Sign In URL** textbox, type your Lynda.com tenant URL (e.g.: *https://shib.lynda.com/Shibboleth.sso/InCommon?providerId=https://sts.windows-ppe.net/6247032d-9415-403c-b72b-277e3fb6f2c8/&target=https://shib.lynda.com/InCommon*), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="142a0-139">On the **Configure App URL** page, in the **Lynda.com Sign In URL** textbox, type your Lynda.com tenant URL (e.g.: *https://shib.lynda.com/Shibboleth.sso/InCommon?providerId=https://sts.windows-ppe.net/6247032d-9415-403c-b72b-277e3fb6f2c8/&target=https://shib.lynda.com/InCommon*), and then click **Next**.</span></span>
   
   <span data-ttu-id="142a0-140">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC781047.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="142a0-140">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC781047.png "Configure app URL")</span></span>
4. <span data-ttu-id="142a0-141">On the **Configure single sign-on at Lynda.com** page, to download your metadata, click **Download metadata**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="142a0-141">On the **Configure single sign-on at Lynda.com** page, to download your metadata, click **Download metadata**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="142a0-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777529.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="142a0-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777529.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="142a0-143">Send the downloaded metadata file to the Lynda.com support team.</span><span class="sxs-lookup"><span data-stu-id="142a0-143">Send the downloaded metadata file to the Lynda.com support team.</span></span> <span data-ttu-id="142a0-144">The Lynda.com support team does the Single Sign On configuration for you.</span><span class="sxs-lookup"><span data-stu-id="142a0-144">The Lynda.com support team does the Single Sign On configuration for you.</span></span>
6. <span data-ttu-id="142a0-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="142a0-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="142a0-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777530.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="142a0-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777530.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="142a0-147">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="142a0-147">Configure user provisioning</span></span>

<span data-ttu-id="142a0-148">There is no action item for you to configure user provisioning to Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="142a0-148">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="142a0-149">When an assigned user tries to log into Lynda.com using the access panel, Lynda.com checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="142a0-149">When an assigned user tries to log into Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="142a0-150">If there is no user account available yet, it is automatically created by Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="142a0-150">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="142a0-151">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="142a0-151">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="142a0-152">Assign users</span><span class="sxs-lookup"><span data-stu-id="142a0-152">Assign users</span></span>
<span data-ttu-id="142a0-153">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="142a0-153">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="142a0-154">**To assign users to Lynda.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="142a0-154">**To assign users to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="142a0-155">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="142a0-155">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="142a0-156">On the **Lynda.com** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="142a0-156">On the **Lynda.com** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="142a0-157">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777531.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="142a0-157">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC777531.png "Assign users")</span></span>
3. <span data-ttu-id="142a0-158">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="142a0-158">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="142a0-159">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="142a0-159">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lynda-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="142a0-160">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="142a0-160">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="142a0-161">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="142a0-161">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















