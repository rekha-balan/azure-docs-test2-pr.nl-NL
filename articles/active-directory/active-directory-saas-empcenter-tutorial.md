---
title: 'Tutorial: Azure Active Directory integration with EmpCenter | Microsoft Docs'
description: Learn how to use EmpCenter with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: a4c6e4177d8c4e1b577cdd7ac4c1499a7048f2ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550712"
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="5c822-103">Tutorial: Azure Active Directory integration with EmpCenter</span><span class="sxs-lookup"><span data-stu-id="5c822-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>
<span data-ttu-id="5c822-104">The objective of this tutorial is to show the integration of Azure and EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="5c822-104">The objective of this tutorial is to show the integration of Azure and EmpCenter.</span></span>  
<span data-ttu-id="5c822-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="5c822-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5c822-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5c822-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5c822-107">An EmpCenter single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5c822-107">An EmpCenter single sign-on enabled subscription</span></span>

<span data-ttu-id="5c822-108">After completing this tutorial, the Azure AD users you have assigned to EmpCenter will be able to single sign into the application at your EmpCenter company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c822-108">After completing this tutorial, the Azure AD users you have assigned to EmpCenter will be able to single sign into the application at your EmpCenter company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5c822-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5c822-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="5c822-110">Enabling the application integration for EmpCenter</span><span class="sxs-lookup"><span data-stu-id="5c822-110">Enabling the application integration for EmpCenter</span></span>
2. <span data-ttu-id="5c822-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c822-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="5c822-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5c822-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5c822-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5c822-113">Assigning users</span></span>

<span data-ttu-id="5c822-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802916.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="5c822-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802916.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-empcenter"></a><span data-ttu-id="5c822-115">Enabling the application integration for EmpCenter</span><span class="sxs-lookup"><span data-stu-id="5c822-115">Enabling the application integration for EmpCenter</span></span>
<span data-ttu-id="5c822-116">The objective of this section is to outline how to enable the application integration for EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="5c822-116">The objective of this section is to outline how to enable the application integration for EmpCenter.</span></span>

### <a name="to-enable-the-application-integration-for-empcenter-perform-the-following-steps"></a><span data-ttu-id="5c822-117">To enable the application integration for EmpCenter, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c822-117">To enable the application integration for EmpCenter, perform the following steps:</span></span>
1. <span data-ttu-id="5c822-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c822-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5c822-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5c822-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5c822-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5c822-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5c822-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5c822-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5c822-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="5c822-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5c822-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5c822-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5c822-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="5c822-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5c822-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5c822-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5c822-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="5c822-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5c822-127">In the **search box**, type **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="5c822-127">In the **search box**, type **EmpCenter**.</span></span>
   
   <span data-ttu-id="5c822-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802917.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="5c822-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802917.png "Application Gallery")</span></span>
7. <span data-ttu-id="5c822-129">In the results pane, select **EmpCenter**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5c822-129">In the results pane, select **EmpCenter**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5c822-130">![EmpCentral](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802918.png "EmpCentral")</span><span class="sxs-lookup"><span data-stu-id="5c822-130">![EmpCentral](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802918.png "EmpCentral")</span></span>
   

## <a name="configuring-single-sign-on"></a><span data-ttu-id="5c822-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c822-131">Configuring single sign-on</span></span>

<span data-ttu-id="5c822-132">The objective of this section is to outline how to enable users to authenticate to EmpCenter with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="5c822-132">The objective of this section is to outline how to enable users to authenticate to EmpCenter with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="5c822-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c822-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="5c822-134">In the Azure classic portal, on the **EmpCenter** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="5c822-134">In the Azure classic portal, on the **EmpCenter** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="5c822-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802919.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5c822-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802919.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="5c822-136">On the **How would you like users to sign on to EmpCenter** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c822-136">On the **How would you like users to sign on to EmpCenter** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5c822-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802920.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5c822-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802920.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="5c822-138">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c822-138">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="5c822-139">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802921.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="5c822-139">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802921.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="5c822-140">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your EmpCenter application (e.g.: *https://partner-authenticati.empcenter.com/workforce/SSO.do*).</span><span class="sxs-lookup"><span data-stu-id="5c822-140">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your EmpCenter application (e.g.: *https://partner-authenticati.empcenter.com/workforce/SSO.do*).</span></span>
   2. <span data-ttu-id="5c822-141">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="5c822-141">Click **Next**</span></span>
4. <span data-ttu-id="5c822-142">On the **Configure single sign-on at EmpCenter** page, to download your metadata, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5c822-142">On the **Configure single sign-on at EmpCenter** page, to download your metadata, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="5c822-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802922.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5c822-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802922.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="5c822-144">Send the downloaded metadata file to your EmpCenter support team.</span><span class="sxs-lookup"><span data-stu-id="5c822-144">Send the downloaded metadata file to your EmpCenter support team.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5c822-145">Your EmpCenter support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="5c822-145">Your EmpCenter support team has to do the actual SSO configuration.</span></span>
   > <span data-ttu-id="5c822-146">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="5c822-146">You will get a notification when SSO has been enabled for your subscription.</span></span>
   > 
   > 
6. <span data-ttu-id="5c822-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5c822-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5c822-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802923.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5c822-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802923.png "Configure Single Sign-On")</span></span>
   
## <a name="configuring-user-provisioning"></a><span data-ttu-id="5c822-149">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5c822-149">Configuring user provisioning</span></span>

<span data-ttu-id="5c822-150">In order to enable Azure AD users to log into EmpCenter, they must be provisioned into EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="5c822-150">In order to enable Azure AD users to log into EmpCenter, they must be provisioned into EmpCenter.</span></span>  
<span data-ttu-id="5c822-151">In the case of EmpCenter, the user accounts need to be created by your EmpCenter support team.</span><span class="sxs-lookup"><span data-stu-id="5c822-151">In the case of EmpCenter, the user accounts need to be created by your EmpCenter support team.</span></span>

> [!NOTE]
> <span data-ttu-id="5c822-152">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="5c822-152">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="5c822-153">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5c822-153">Assigning users</span></span>
<span data-ttu-id="5c822-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="5c822-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-empcenter-perform-the-following-steps"></a><span data-ttu-id="5c822-155">To assign users to EmpCenter, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c822-155">To assign users to EmpCenter, perform the following steps:</span></span>
1. <span data-ttu-id="5c822-156">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="5c822-156">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5c822-157">On the \*\*EmpCenter \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="5c822-157">On the \*\*EmpCenter \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5c822-158">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802924.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="5c822-158">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC802924.png "Assign Users")</span></span>
3. <span data-ttu-id="5c822-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="5c822-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5c822-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="5c822-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-empcenter-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5c822-161">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5c822-161">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5c822-162">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c822-162">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















