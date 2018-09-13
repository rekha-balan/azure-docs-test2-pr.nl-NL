---
title: 'Tutorial: Azure Active Directory integration with Cornerstone OnDemand | Microsoft Docs'
description: Learn how to use Cornerstone OnDemand with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: decffd3bf15037c437463937d044e9d6d4150f2d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555675"
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="19029-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="19029-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>
<span data-ttu-id="19029-104">The objective of this tutorial is to show the integration of Azure and Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="19029-104">The objective of this tutorial is to show the integration of Azure and Cornerstone OnDemand.</span></span>

<span data-ttu-id="19029-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="19029-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="19029-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="19029-106">A valid Azure subscription</span></span>
* <span data-ttu-id="19029-107">A Cornerstone OnDemand tenant</span><span class="sxs-lookup"><span data-stu-id="19029-107">A Cornerstone OnDemand tenant</span></span>

<span data-ttu-id="19029-108">After completing this tutorial, the Azure AD users you have assigned to Cornerstone OnDemand will be able to single sign into the application at your Cornerstone OnDemand company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19029-108">After completing this tutorial, the Azure AD users you have assigned to Cornerstone OnDemand will be able to single sign into the application at your Cornerstone OnDemand company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="19029-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19029-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="19029-110">Enabling the application integration for Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="19029-110">Enabling the application integration for Cornerstone OnDemand</span></span>
* <span data-ttu-id="19029-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="19029-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="19029-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="19029-112">Configuring user provisioning</span></span>
* <span data-ttu-id="19029-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="19029-113">Assigning users</span></span>

<span data-ttu-id="19029-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781593.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="19029-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781593.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cornerstone-ondemand"></a><span data-ttu-id="19029-115">Enable the application integration for Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="19029-115">Enable the application integration for Cornerstone OnDemand</span></span>
<span data-ttu-id="19029-116">The objective of this section is to outline how to enable the application integration for Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="19029-116">The objective of this section is to outline how to enable the application integration for Cornerstone OnDemand.</span></span>

<span data-ttu-id="19029-117">**To enable the application integration for Cornerstone OnDemand, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19029-117">**To enable the application integration for Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="19029-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19029-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="19029-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="19029-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="19029-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19029-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="19029-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19029-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="19029-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="19029-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="19029-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19029-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="19029-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="19029-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="19029-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="19029-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="19029-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="19029-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="19029-127">In the **search box**, type **cornerstone ondemand**.</span><span class="sxs-lookup"><span data-stu-id="19029-127">In the **search box**, type **cornerstone ondemand**.</span></span>
   
   <span data-ttu-id="19029-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781594.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="19029-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781594.png "Application Gallery")</span></span>
7. <span data-ttu-id="19029-129">In the results pane, select **Cornerstone OnDemand**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="19029-129">In the results pane, select **Cornerstone OnDemand**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="19029-130">![Cornerstone OnDemand](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781595.png "Cornerstone OnDemand")</span><span class="sxs-lookup"><span data-stu-id="19029-130">![Cornerstone OnDemand](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781595.png "Cornerstone OnDemand")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="19029-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="19029-131">Configure single sign-on</span></span>

<span data-ttu-id="19029-132">The objective of this section is to outline how to enable users to authenticate to Cornerstone OnDemand with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="19029-132">The objective of this section is to outline how to enable users to authenticate to Cornerstone OnDemand with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="19029-133">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19029-133">**To configure SSO, perform the following steps:**</span></span>
1. <span data-ttu-id="19029-134">In the Azure classic portal, on the **Cornerstone OnDemand** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="19029-134">In the Azure classic portal, on the **Cornerstone OnDemand** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="19029-135">![Enable Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781596.png "Enable Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19029-135">![Enable Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781596.png "Enable Single Sign-On")</span></span>
2. <span data-ttu-id="19029-136">On the **How would you like users to sign on to Cornerstone OnDemand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19029-136">On the **How would you like users to sign on to Cornerstone OnDemand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="19029-137">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781597.png "Microsoft Azure AD Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19029-137">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781597.png "Microsoft Azure AD Single Sign-On")</span></span>
3. <span data-ttu-id="19029-138">On the **Configure App URL** page, in the **Cornerstone OnDemand Sign In URL** textbox, type your URL using the following pattern "*http://company.csod.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19029-138">On the **Configure App URL** page, in the **Cornerstone OnDemand Sign In URL** textbox, type your URL using the following pattern "*http://company.csod.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="19029-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781598.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="19029-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781598.png "Configure App URL")</span></span>
4. <span data-ttu-id="19029-140">On the **Configure single sign-on at Cornerstone OnDemand** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="19029-140">On the **Configure single sign-on at Cornerstone OnDemand** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="19029-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781599.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19029-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781599.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="19029-142">Send the following items to the Cornerstone OnDemand support team:</span><span class="sxs-lookup"><span data-stu-id="19029-142">Send the following items to the Cornerstone OnDemand support team:</span></span>  
   1. <span data-ttu-id="19029-143">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="19029-143">The downloaded certificate</span></span>
   2. <span data-ttu-id="19029-144">The **Remote Login URL** value</span><span class="sxs-lookup"><span data-stu-id="19029-144">The **Remote Login URL** value</span></span>
   3. <span data-ttu-id="19029-145">The **Remote Logout URL** value.</span><span class="sxs-lookup"><span data-stu-id="19029-145">The **Remote Logout URL** value.</span></span>

   >[!NOTE]
   ><span data-ttu-id="19029-146">Single Sign-On needs to be configured by the Cornerstone OnDemand support team.</span><span class="sxs-lookup"><span data-stu-id="19029-146">Single Sign-On needs to be configured by the Cornerstone OnDemand support team.</span></span> <span data-ttu-id="19029-147">You will get a notification from the support team when the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="19029-147">You will get a notification from the support team when the configuration has been completed.</span></span>
   > 
6. <span data-ttu-id="19029-148">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="19029-148">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
  <span data-ttu-id="19029-149">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781600.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19029-149">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781600.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="19029-150">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="19029-150">Configure user provisioning</span></span>

<span data-ttu-id="19029-151">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="19029-151">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="19029-152">In the case of Cornerstone OnDemand, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="19029-152">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="19029-153">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19029-153">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="19029-154">Send the information (e.g.: Name, Emial) about the Azure AD user you want to provision to the Cornerstone OnDemand support team.</span><span class="sxs-lookup"><span data-stu-id="19029-154">Send the information (e.g.: Name, Emial) about the Azure AD user you want to provision to the Cornerstone OnDemand support team.</span></span>

>[!NOTE]
><span data-ttu-id="19029-155">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="19029-155">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="19029-156">Assign users</span><span class="sxs-lookup"><span data-stu-id="19029-156">Assign users</span></span>
<span data-ttu-id="19029-157">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="19029-157">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="19029-158">**To assign users to Cornerstone OnDemand, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19029-158">**To assign users to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="19029-159">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="19029-159">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="19029-160">On the \*\*Cornerstone OnDemand \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="19029-160">On the \*\*Cornerstone OnDemand \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="19029-161">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC775564.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="19029-161">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC775564.png "Assign users")</span></span>
3. <span data-ttu-id="19029-162">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="19029-162">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="19029-163">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781601.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="19029-163">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cornerstone-ondemand-tutorial/IC781601.png "Assign Users")</span></span>

<span data-ttu-id="19029-164">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="19029-164">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="19029-165">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19029-165">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















