---
title: 'Tutorial: Azure Active Directory integration with Huddle | Microsoft Docs'
description: Learn how to use Huddle with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 5cfdc39fd15ab230006d849245fb17cfffec70c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661167"
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="a6936-103">Tutorial: Azure Active Directory integration with Huddle</span><span class="sxs-lookup"><span data-stu-id="a6936-103">Tutorial: Azure Active Directory integration with Huddle</span></span>
<span data-ttu-id="a6936-104">The objective of this tutorial is to show the integration of Azure and Huddle.</span><span class="sxs-lookup"><span data-stu-id="a6936-104">The objective of this tutorial is to show the integration of Azure and Huddle.</span></span>  
<span data-ttu-id="a6936-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a6936-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a6936-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a6936-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a6936-107">A Huddle single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a6936-107">A Huddle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a6936-108">After completing this tutorial, the Azure AD users you have assigned to Huddle will be able to single sign into the application at your Huddle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a6936-108">After completing this tutorial, the Azure AD users you have assigned to Huddle will be able to single sign into the application at your Huddle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a6936-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a6936-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="a6936-110">Enabling the application integration for Huddle</span><span class="sxs-lookup"><span data-stu-id="a6936-110">Enabling the application integration for Huddle</span></span>
* <span data-ttu-id="a6936-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="a6936-111">Configuring single sign-on</span></span>
* <span data-ttu-id="a6936-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a6936-112">Configuring user provisioning</span></span>
* <span data-ttu-id="a6936-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a6936-113">Assigning users</span></span>

<span data-ttu-id="a6936-114">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787830.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a6936-114">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787830.png "Configure Single Sign-On")</span></span>

## <a name="enable-the-application-integration-for-huddle"></a><span data-ttu-id="a6936-115">Enable the application integration for Huddle</span><span class="sxs-lookup"><span data-stu-id="a6936-115">Enable the application integration for Huddle</span></span>
<span data-ttu-id="a6936-116">The objective of this section is to outline how to enable the application integration for Huddle.</span><span class="sxs-lookup"><span data-stu-id="a6936-116">The objective of this section is to outline how to enable the application integration for Huddle.</span></span>

<span data-ttu-id="a6936-117">**To enable the application integration for Huddle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6936-117">**To enable the application integration for Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="a6936-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6936-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a6936-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a6936-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a6936-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a6936-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a6936-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a6936-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a6936-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a6936-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a6936-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a6936-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a6936-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a6936-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a6936-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a6936-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a6936-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a6936-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a6936-127">In the **search box**, type **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="a6936-127">In the **search box**, type **Huddle**.</span></span>
   
   <span data-ttu-id="a6936-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787831.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a6936-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787831.png "Application Gallery")</span></span>
7. <span data-ttu-id="a6936-129">In the results pane, select **Huddle**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a6936-129">In the results pane, select **Huddle**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a6936-130">![Huddle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787832.png "Huddle")</span><span class="sxs-lookup"><span data-stu-id="a6936-130">![Huddle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787832.png "Huddle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a6936-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a6936-131">Configure single sign-on</span></span>

<span data-ttu-id="a6936-132">The objective of this section is to outline how to enable users to authenticate to Huddle with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a6936-132">The objective of this section is to outline how to enable users to authenticate to Huddle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="a6936-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6936-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a6936-134">In the Azure classic portal, on the **Huddle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a6936-134">In the Azure classic portal, on the **Huddle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a6936-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787833.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a6936-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787833.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a6936-136">On the **How would you like users to sign on to Huddle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a6936-136">On the **How would you like users to sign on to Huddle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a6936-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787834.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a6936-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787834.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="a6936-138">On the **Configure App URL** page, in the **Huddle Sign On URL** textbox, type the URL of your Huddle tenant using the following pattern "*http://company.huddle.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a6936-138">On the **Configure App URL** page, in the **Huddle Sign On URL** textbox, type the URL of your Huddle tenant using the following pattern "*http://company.huddle.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="a6936-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787835.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a6936-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787835.png "Configure App URL")</span></span>
4. <span data-ttu-id="a6936-140">On the **Configure single sign-on at Huddle** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a6936-140">On the **Configure single sign-on at Huddle** page, perform the following steps:</span></span>
   
   <span data-ttu-id="a6936-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787836.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a6936-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787836.png "Configure Single Sign-On")</span></span>
   
   1. <span data-ttu-id="a6936-142">Click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a6936-142">Click **Download certificate**, and then save the certificate file on your computer.</span></span>
   2. <span data-ttu-id="a6936-143">Copy the **Issuer URL** value, the **SAML SSO URL** value and the downloaded certificate, and then send them to the Huddle support team.</span><span class="sxs-lookup"><span data-stu-id="a6936-143">Copy the **Issuer URL** value, the **SAML SSO URL** value and the downloaded certificate, and then send them to the Huddle support team.</span></span>  
   
    >[!NOTE]
    ><span data-ttu-id="a6936-144">Single sign-on needs to be enabled by the Huddle support team.</span><span class="sxs-lookup"><span data-stu-id="a6936-144">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="a6936-145">You will get a notification when the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="a6936-145">You will get a notification when the configuration has been completed.</span></span> 
    > 
5. <span data-ttu-id="a6936-146">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a6936-146">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a6936-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787837.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a6936-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787837.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="a6936-148">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a6936-148">Configure user provisioning</span></span>

<span data-ttu-id="a6936-149">In order to enable Azure AD users to log into Huddle, they must be provisioned into Huddle.</span><span class="sxs-lookup"><span data-stu-id="a6936-149">In order to enable Azure AD users to log into Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="a6936-150">In the case of Huddle, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a6936-150">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="a6936-151">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6936-151">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a6936-152">Log in to your **Huddle** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="a6936-152">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="a6936-153">Click **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="a6936-153">Click **Workspace**.</span></span>
3. <span data-ttu-id="a6936-154">Click **People \> Invite People**.</span><span class="sxs-lookup"><span data-stu-id="a6936-154">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="a6936-155">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span><span class="sxs-lookup"><span data-stu-id="a6936-155">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>
4. <span data-ttu-id="a6936-156">In the **Create a new invitation** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a6936-156">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a6936-157">![New Invitation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span><span class="sxs-lookup"><span data-stu-id="a6936-157">![New Invitation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   1. <span data-ttu-id="a6936-158">In the **Choose a team to invite people to join** list, select **team**.</span><span class="sxs-lookup"><span data-stu-id="a6936-158">In the **Choose a team to invite people to join** list, select **team**.</span></span>
   2. <span data-ttu-id="a6936-159">Type the **Email Address** of a valid AAD account you want to provision into the related textbox.</span><span class="sxs-lookup"><span data-stu-id="a6936-159">Type the **Email Address** of a valid AAD account you want to provision into the related textbox.</span></span>
   3. <span data-ttu-id="a6936-160">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="a6936-160">Click **Invite**.</span></span>   
   
    >[!NOTE]
    ><span data-ttu-id="a6936-161">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="a6936-161">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="a6936-162">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a6936-162">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="a6936-163">Assign users</span><span class="sxs-lookup"><span data-stu-id="a6936-163">Assign users</span></span>
<span data-ttu-id="a6936-164">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a6936-164">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a6936-165">**To assign users to Huddle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6936-165">**To assign users to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="a6936-166">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a6936-166">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a6936-167">On the **Huddle** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a6936-167">On the **Huddle** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a6936-168">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787840.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="a6936-168">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC787840.png "Assign Users")</span></span>
3. <span data-ttu-id="a6936-169">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a6936-169">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a6936-170">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a6936-170">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-huddle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a6936-171">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a6936-171">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a6936-172">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a6936-172">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















