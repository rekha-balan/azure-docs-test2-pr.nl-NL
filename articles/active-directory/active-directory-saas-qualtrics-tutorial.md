---
title: 'Tutorial: Azure Active Directory integration with Qualtrics | Microsoft Docs'
description: Learn how to use Qualtrics with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 28e82508628afcdcc7d1eb9d67b75534a503b0ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553817"
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="a89b4-103">Tutorial: Azure Active Directory integration with Qualtrics</span><span class="sxs-lookup"><span data-stu-id="a89b4-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="a89b4-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="a89b4-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="a89b4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a89b4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a89b4-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a89b4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a89b4-107">A Qualtrics single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a89b4-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a89b4-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a89b4-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a89b4-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a89b4-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="a89b4-110">Enabling the application integration for Qualtrics</span><span class="sxs-lookup"><span data-stu-id="a89b4-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="a89b4-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="a89b4-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="a89b4-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a89b4-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="a89b4-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a89b4-113">Assigning users</span></span>

<span data-ttu-id="a89b4-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a89b4-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="a89b4-115">Enabling the application integration for Qualtrics</span><span class="sxs-lookup"><span data-stu-id="a89b4-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="a89b4-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="a89b4-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="a89b4-117">**To enable the application integration for Qualtrics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a89b4-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="a89b4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a89b4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a89b4-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a89b4-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a89b4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a89b4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a89b4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a89b4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a89b4-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a89b4-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a89b4-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a89b4-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a89b4-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a89b4-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a89b4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a89b4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a89b4-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a89b4-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a89b4-127">In the **search box**, type **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="a89b4-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="a89b4-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a89b4-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="a89b4-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a89b4-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a89b4-130">![Qualtrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="a89b4-130">![Qualtrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a89b4-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a89b4-131">Configure single sign-on</span></span>

<span data-ttu-id="a89b4-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a89b4-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="a89b4-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a89b4-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a89b4-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a89b4-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a89b4-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a89b4-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a89b4-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a89b4-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a89b4-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a89b4-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="a89b4-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a89b4-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="a89b4-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a89b4-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="a89b4-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a89b4-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="a89b4-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a89b4-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="a89b4-142">Send the metadata file to the Qualtrics support team.</span><span class="sxs-lookup"><span data-stu-id="a89b4-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="a89b4-143">The SSO configuration has to be performed by the Qualtrics support team.</span><span class="sxs-lookup"><span data-stu-id="a89b4-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="a89b4-144">You will get a notification as soon as the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="a89b4-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="a89b4-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a89b4-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a89b4-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a89b4-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="a89b4-147">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a89b4-147">Configure user provisioning</span></span>

<span data-ttu-id="a89b4-148">There is no action item for you to configure user provisioning to Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="a89b4-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="a89b4-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="a89b4-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="a89b4-150">If there is no user account available yet, it is automatically created by Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="a89b4-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="a89b4-151">Assign users</span><span class="sxs-lookup"><span data-stu-id="a89b4-151">Assign users</span></span>
<span data-ttu-id="a89b4-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a89b4-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a89b4-153">**To assign users to Qualtrics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a89b4-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="a89b4-154">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a89b4-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a89b4-155">On the **Qualtrics** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a89b4-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a89b4-156">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="a89b4-156">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="a89b4-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a89b4-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a89b4-158">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a89b4-158">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a89b4-159">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a89b4-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="a89b4-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a89b4-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















