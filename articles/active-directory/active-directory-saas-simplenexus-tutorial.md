---
title: 'Tutorial: Azure Active Directory integration with SimpleNexus | Microsoft Docs'
description: Learn how to use SimpleNexus with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: fbab7e283d862865aed0c14c3c0298ec28a182a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550926"
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="24241-103">Tutorial: Azure Active Directory integration with SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="24241-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>
<span data-ttu-id="24241-104">The objective of this tutorial is to show the integration of Azure and SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="24241-104">The objective of this tutorial is to show the integration of Azure and SimpleNexus.</span></span>  

<span data-ttu-id="24241-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="24241-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="24241-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="24241-106">A valid Azure subscription</span></span>
* <span data-ttu-id="24241-107">A SimpleNexus single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="24241-107">A SimpleNexus single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="24241-108">After completing this tutorial, the Azure AD users you have assigned to SimpleNexus will be able to single sign into the application at your SimpleNexus company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24241-108">After completing this tutorial, the Azure AD users you have assigned to SimpleNexus will be able to single sign into the application at your SimpleNexus company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="24241-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="24241-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="24241-110">Enabling the application integration for SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="24241-110">Enabling the application integration for SimpleNexus</span></span>
2. <span data-ttu-id="24241-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="24241-111">Configuring single sign-on (SSO)</span></span> 
3. <span data-ttu-id="24241-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="24241-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="24241-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="24241-113">Assigning users</span></span>

<span data-ttu-id="24241-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785893.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="24241-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785893.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-simplenexus"></a><span data-ttu-id="24241-115">Enabling the application integration for SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="24241-115">Enabling the application integration for SimpleNexus</span></span>
<span data-ttu-id="24241-116">The objective of this section is to outline how to enable the application integration for SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="24241-116">The objective of this section is to outline how to enable the application integration for SimpleNexus.</span></span>

<span data-ttu-id="24241-117">**To enable the application integration for SimpleNexus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24241-117">**To enable the application integration for SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="24241-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24241-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="24241-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="24241-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="24241-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="24241-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="24241-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="24241-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="24241-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="24241-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="24241-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="24241-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="24241-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="24241-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="24241-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="24241-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="24241-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="24241-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="24241-127">In the **search box**, type **simple nexus**.</span><span class="sxs-lookup"><span data-stu-id="24241-127">In the **search box**, type **simple nexus**.</span></span>
   
    <span data-ttu-id="24241-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785894.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="24241-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785894.png "Application Gallery")</span></span>

7. <span data-ttu-id="24241-129">In the results pane, select **SimpleNexus**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="24241-129">In the results pane, select **SimpleNexus**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="24241-130">![Simple Nexus](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC809578.png "Simple Nexus")</span><span class="sxs-lookup"><span data-stu-id="24241-130">![Simple Nexus](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC809578.png "Simple Nexus")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="24241-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="24241-131">Configure single sign-on</span></span>

<span data-ttu-id="24241-132">The objective of this section is to outline how to enable users to authenticate to SimpleNexus with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="24241-132">The objective of this section is to outline how to enable users to authenticate to SimpleNexus with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="24241-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24241-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="24241-134">In the Azure classic portal, on the **SimpleNexus** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="24241-134">In the Azure classic portal, on the **SimpleNexus** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="24241-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785896.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="24241-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785896.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="24241-136">On the **How would you like users to sign on to SimpleNexus** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24241-136">On the **How would you like users to sign on to SimpleNexus** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="24241-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785897.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="24241-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785897.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="24241-138">On the **Configure App URL** page, in the **SimpleNexus Sign In URL** textbox, type your URL using the following pattern "*https://simplenexus.com/CompanyName\_login*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24241-138">On the **Configure App URL** page, in the **SimpleNexus Sign In URL** textbox, type your URL using the following pattern "*https://simplenexus.com/CompanyName\_login*", and then click **Next**.</span></span>
   
    <span data-ttu-id="24241-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC786904.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="24241-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC786904.png "Configure App URL")</span></span>

4. <span data-ttu-id="24241-140">On the **Configure single sign-on at SimpleNexus** page, click **Download metadata**, and then forward the metadata file to the SimpleNexus support team.</span><span class="sxs-lookup"><span data-stu-id="24241-140">On the **Configure single sign-on at SimpleNexus** page, click **Download metadata**, and then forward the metadata file to the SimpleNexus support team.</span></span>
   
    <span data-ttu-id="24241-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785899.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="24241-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785899.png "Configure Single Sign-On")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="24241-142">Single sign-on needs to be enabled by the SimpleNexus support team.</span><span class="sxs-lookup"><span data-stu-id="24241-142">Single sign-on needs to be enabled by the SimpleNexus support team.</span></span> 
    > 

5. <span data-ttu-id="24241-143">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="24241-143">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="24241-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785900.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="24241-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785900.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="24241-145">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="24241-145">Configure user provisioning</span></span>

<span data-ttu-id="24241-146">In order to enable Azure AD users to log into SimpleNexus, they must be provisioned into SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="24241-146">In order to enable Azure AD users to log into SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="24241-147">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="24241-147">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="24241-148">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="24241-148">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="24241-149">Assign users</span><span class="sxs-lookup"><span data-stu-id="24241-149">Assign users</span></span>
<span data-ttu-id="24241-150">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="24241-150">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="24241-151">**To assign users to SimpleNexus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24241-151">**To assign users to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="24241-152">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="24241-152">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="24241-153">On the **SimpleNexus** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="24241-153">On the **SimpleNexus** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="24241-154">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785901.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="24241-154">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC785901.png "Assign Users")</span></span>

3. <span data-ttu-id="24241-155">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="24241-155">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="24241-156">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="24241-156">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-simplenexus-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="24241-157">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="24241-157">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="24241-158">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24241-158">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















