---
title: 'Tutorial: Azure Active Directory integration with Projectplace | Microsoft Docs'
description: Learn how to use Projectplace with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 6b3c3b2d3c5cd142ce5251500d8036efd4c7c6dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550585"
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="601da-103">Tutorial: Azure Active Directory integration with Projectplace</span><span class="sxs-lookup"><span data-stu-id="601da-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>
<span data-ttu-id="601da-104">The objective of this tutorial is to show the integration of Azure and Projectplace.</span><span class="sxs-lookup"><span data-stu-id="601da-104">The objective of this tutorial is to show the integration of Azure and Projectplace.</span></span> <span data-ttu-id="601da-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="601da-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="601da-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="601da-106">A valid Azure subscription</span></span>
* <span data-ttu-id="601da-107">A Projectplace single sign-on enabled (SSO) subscription</span><span class="sxs-lookup"><span data-stu-id="601da-107">A Projectplace single sign-on enabled (SSO) subscription</span></span>

<span data-ttu-id="601da-108">After completing this tutorial, the Azure AD users you have assigned to Projectplace will be able to single sign into the application at your Projectplace company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="601da-108">After completing this tutorial, the Azure AD users you have assigned to Projectplace will be able to single sign into the application at your Projectplace company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="601da-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="601da-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="601da-110">Enabling the application integration for Projectplace</span><span class="sxs-lookup"><span data-stu-id="601da-110">Enabling the application integration for Projectplace</span></span>
2. <span data-ttu-id="601da-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="601da-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="601da-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="601da-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="601da-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="601da-113">Assigning users</span></span>

<span data-ttu-id="601da-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790217.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="601da-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790217.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-projectplace"></a><span data-ttu-id="601da-115">Enabling the application integration for Projectplace</span><span class="sxs-lookup"><span data-stu-id="601da-115">Enabling the application integration for Projectplace</span></span>
<span data-ttu-id="601da-116">The objective of this section is to outline how to enable the application integration for Projectplace.</span><span class="sxs-lookup"><span data-stu-id="601da-116">The objective of this section is to outline how to enable the application integration for Projectplace.</span></span>

<span data-ttu-id="601da-117">**To enable the application integration for Projectplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="601da-117">**To enable the application integration for Projectplace, perform the following steps:**</span></span>
1. <span data-ttu-id="601da-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="601da-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="601da-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="601da-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="601da-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="601da-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="601da-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="601da-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="601da-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="601da-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="601da-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="601da-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="601da-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="601da-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="601da-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="601da-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="601da-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="601da-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="601da-127">In the **search box**, type **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="601da-127">In the **search box**, type **Projectplace**.</span></span>
   
   <span data-ttu-id="601da-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790218.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="601da-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790218.png "Application Gallery")</span></span>
7. <span data-ttu-id="601da-129">In the results pane, select **Projectplace**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="601da-129">In the results pane, select **Projectplace**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="601da-130">![ProjectPlace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790219.png "ProjectPlace")</span><span class="sxs-lookup"><span data-stu-id="601da-130">![ProjectPlace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790219.png "ProjectPlace")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="601da-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="601da-131">Configure single sign-on</span></span>

<span data-ttu-id="601da-132">The objective of this section is to outline how to enable users to authenticate to Projectplace with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="601da-132">The objective of this section is to outline how to enable users to authenticate to Projectplace with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="601da-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="601da-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="601da-134">In the Azure classic portal, on the **Projectplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="601da-134">In the Azure classic portal, on the **Projectplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="601da-135">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790220.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="601da-135">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790220.png "Configure Single SignOn")</span></span>
2. <span data-ttu-id="601da-136">On the **How would you like users to sign on to Projectplace** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="601da-136">On the **How would you like users to sign on to Projectplace** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="601da-137">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790221.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="601da-137">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790221.png "Configure Single SignOn")</span></span>
3. <span data-ttu-id="601da-138">On the **Configure App URL** page, in the **Projectplace Sign On URL** textbox, type your ProjectPlace tenant URL (e.g.: "*http://company.projectplace.com*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="601da-138">On the **Configure App URL** page, in the **Projectplace Sign On URL** textbox, type your ProjectPlace tenant URL (e.g.: "*http://company.projectplace.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="601da-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790222.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="601da-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790222.png "Configure App URL")</span></span>
4. <span data-ttu-id="601da-140">On the **Configure single sign-on at Projectplace** page, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="601da-140">On the **Configure single sign-on at Projectplace** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="601da-141">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790223.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="601da-141">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790223.png "Configure Single SignOn")</span></span>
5. <span data-ttu-id="601da-142">Send the metadata file to the Projectplace support team.</span><span class="sxs-lookup"><span data-stu-id="601da-142">Send the metadata file to the Projectplace support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="601da-143">The single sign-on configuration has to be performed by the Projectplace support team.</span><span class="sxs-lookup"><span data-stu-id="601da-143">The single sign-on configuration has to be performed by the Projectplace support team.</span></span> <span data-ttu-id="601da-144">You will get a notification as soon as the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="601da-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="601da-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="601da-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="601da-146">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790227.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="601da-146">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790227.png "Configure Single SignOn")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="601da-147">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="601da-147">Configure user provisioning</span></span>

<span data-ttu-id="601da-148">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span><span class="sxs-lookup"><span data-stu-id="601da-148">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="601da-149">In the case of Projectplace, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="601da-149">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="601da-150">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="601da-150">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="601da-151">Log in to your **Projectplace** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="601da-151">Log in to your **Projectplace** company site as an administrator.</span></span>
2. <span data-ttu-id="601da-152">Go to **People**, and then click **Members**.</span><span class="sxs-lookup"><span data-stu-id="601da-152">Go to **People**, and then click **Members**.</span></span>
   
   <span data-ttu-id="601da-153">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790228.png "People")</span><span class="sxs-lookup"><span data-stu-id="601da-153">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790228.png "People")</span></span>
3. <span data-ttu-id="601da-154">Click **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="601da-154">Click **Add Member**.</span></span>
   
   <span data-ttu-id="601da-155">![Add Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790232.png "Add Members")</span><span class="sxs-lookup"><span data-stu-id="601da-155">![Add Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790232.png "Add Members")</span></span>
4. <span data-ttu-id="601da-156">In the **Add Member** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="601da-156">In the **Add Member** section, perform the following steps:</span></span>
   
   <span data-ttu-id="601da-157">![New Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790233.png "New Members")</span><span class="sxs-lookup"><span data-stu-id="601da-157">![New Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790233.png "New Members")</span></span>
   
   1. <span data-ttu-id="601da-158">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="601da-158">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="601da-159">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="601da-159">Click **Send**.</span></span>

<span data-ttu-id="601da-160">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span><span class="sxs-lookup"><span data-stu-id="601da-160">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>


>[!NOTE]
><span data-ttu-id="601da-161">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="601da-161">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="601da-162">Assign users</span><span class="sxs-lookup"><span data-stu-id="601da-162">Assign users</span></span>
<span data-ttu-id="601da-163">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="601da-163">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="601da-164">**To assign users to Projectplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="601da-164">**To assign users to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="601da-165">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="601da-165">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="601da-166">On the **Projectplace** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="601da-166">On the **Projectplace** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="601da-167">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790234.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="601da-167">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC790234.png "Assign Users")</span></span>
3. <span data-ttu-id="601da-168">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="601da-168">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="601da-169">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="601da-169">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-projectplace-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="601da-170">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="601da-170">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="601da-171">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="601da-171">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















