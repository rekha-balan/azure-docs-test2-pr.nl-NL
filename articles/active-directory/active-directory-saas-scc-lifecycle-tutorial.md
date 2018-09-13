---
title: 'Tutorial: Azure Active Directory integration with SCC LifeCycle | Microsoft Docs'
description: Learn how to use SCC LifeCycle with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: d6926dcefed606480121420c3eab4df80967bab0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549375"
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="55838-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="55838-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="55838-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="55838-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="55838-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="55838-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="55838-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="55838-106">A valid Azure subscription</span></span>
* <span data-ttu-id="55838-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="55838-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="55838-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55838-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="55838-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="55838-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="55838-110">Enabling the application integration for SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="55838-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="55838-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="55838-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="55838-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="55838-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="55838-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="55838-113">Assigning users</span></span>

<span data-ttu-id="55838-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="55838-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="55838-115">Enable the application integration for SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="55838-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="55838-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="55838-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="55838-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55838-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="55838-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55838-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="55838-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="55838-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="55838-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="55838-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="55838-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="55838-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="55838-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="55838-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="55838-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="55838-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="55838-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="55838-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="55838-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="55838-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="55838-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="55838-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="55838-127">In the **search box**, type **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="55838-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="55838-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="55838-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="55838-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="55838-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="55838-130">![SCC LifeCycle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="55838-130">![SCC LifeCycle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="55838-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="55838-131">Configure single sign-on</span></span>

<span data-ttu-id="55838-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="55838-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="55838-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55838-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="55838-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="55838-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="55838-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="55838-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="55838-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55838-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="55838-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="55838-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="55838-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55838-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="55838-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="55838-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="55838-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="55838-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="55838-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="55838-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="55838-142">Forward that Metadata file to SCC LifeCycle Support team.</span><span class="sxs-lookup"><span data-stu-id="55838-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="55838-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span><span class="sxs-lookup"><span data-stu-id="55838-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="55838-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="55838-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="55838-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="55838-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="55838-146">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="55838-146">Configure user provisioning</span></span>

<span data-ttu-id="55838-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="55838-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="55838-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="55838-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="55838-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span><span class="sxs-lookup"><span data-stu-id="55838-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="55838-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="55838-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="55838-151">Assign users</span><span class="sxs-lookup"><span data-stu-id="55838-151">Assign users</span></span>
<span data-ttu-id="55838-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="55838-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="55838-153">**To assign users to SCC LifeCycle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55838-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="55838-154">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="55838-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="55838-155">On the \*\*SCC LifeCycle \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="55838-155">On the \*\*SCC LifeCycle \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="55838-156">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="55838-156">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="55838-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="55838-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="55838-158">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="55838-158">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="55838-159">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="55838-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="55838-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55838-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















