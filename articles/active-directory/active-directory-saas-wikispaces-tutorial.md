---
title: 'Tutorial: Azure Active Directory integration with Wikispaces | Microsoft Docs'
description: Learn how to use Wikispaces with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 46fa12366c86f523896f7c224524d24a169d267c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662666"
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="7e947-103">Tutorial: Azure Active Directory integration with Wikispaces</span><span class="sxs-lookup"><span data-stu-id="7e947-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>
<span data-ttu-id="7e947-104">The objective of this tutorial is to show the integration of Azure and Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="7e947-104">The objective of this tutorial is to show the integration of Azure and Wikispaces.</span></span>  
<span data-ttu-id="7e947-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="7e947-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="7e947-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7e947-106">A valid Azure subscription</span></span>
* <span data-ttu-id="7e947-107">A Wikispaces single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7e947-107">A Wikispaces single sign-on enabled subscription</span></span>

<span data-ttu-id="7e947-108">After completing this tutorial, the Azure AD users you have assigned to Wikispaces will be able to single sign into the application at your Wikispaces company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e947-108">After completing this tutorial, the Azure AD users you have assigned to Wikispaces will be able to single sign into the application at your Wikispaces company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="7e947-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7e947-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="7e947-110">Enabling the application integration for Wikispaces</span><span class="sxs-lookup"><span data-stu-id="7e947-110">Enabling the application integration for Wikispaces</span></span>
2. <span data-ttu-id="7e947-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e947-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="7e947-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="7e947-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="7e947-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="7e947-113">Assigning users</span></span>

<span data-ttu-id="7e947-114">![Sceanrio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787182.png "Sceanrio")</span><span class="sxs-lookup"><span data-stu-id="7e947-114">![Sceanrio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787182.png "Sceanrio")</span></span>

## <a name="enabling-the-application-integration-for-wikispaces"></a><span data-ttu-id="7e947-115">Enabling the application integration for Wikispaces</span><span class="sxs-lookup"><span data-stu-id="7e947-115">Enabling the application integration for Wikispaces</span></span>
<span data-ttu-id="7e947-116">The objective of this section is to outline how to enable the application integration for Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="7e947-116">The objective of this section is to outline how to enable the application integration for Wikispaces.</span></span>

### <a name="to-enable-the-application-integration-for-wikispaces-perform-the-following-steps"></a><span data-ttu-id="7e947-117">To enable the application integration for Wikispaces, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e947-117">To enable the application integration for Wikispaces, perform the following steps:</span></span>
1. <span data-ttu-id="7e947-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e947-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="7e947-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7e947-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="7e947-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7e947-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7e947-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7e947-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="7e947-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="7e947-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="7e947-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7e947-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="7e947-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="7e947-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="7e947-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7e947-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="7e947-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="7e947-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="7e947-127">In the **search box**, type **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="7e947-127">In the **search box**, type **Wikispaces**.</span></span>
   
    <span data-ttu-id="7e947-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787186.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="7e947-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787186.png "Application Gallery")</span></span>

7. <span data-ttu-id="7e947-129">In the results pane, select **Wikispaces**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7e947-129">In the results pane, select **Wikispaces**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="7e947-130">![Wikispaces](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787187.png "Wikispaces")</span><span class="sxs-lookup"><span data-stu-id="7e947-130">![Wikispaces](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787187.png "Wikispaces")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="7e947-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e947-131">Configuring single sign-on</span></span>
<span data-ttu-id="7e947-132">The objective of this section is to outline how to enable users to authenticate to Wikispaces with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="7e947-132">The objective of this section is to outline how to enable users to authenticate to Wikispaces with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="7e947-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e947-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="7e947-134">In the Azure classic portal, on the **Wikispaces** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="7e947-134">In the Azure classic portal, on the **Wikispaces** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="7e947-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787188.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e947-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787188.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="7e947-136">On the **How would you like users to sign on to Wikispaces** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e947-136">On the **How would you like users to sign on to Wikispaces** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="7e947-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787189.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e947-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787189.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="7e947-138">On the **Configure App URL** page, in the **Wikispaces Sign On URL** textbox, type your URL using the following pattern "*http://company.wikispaces.net*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e947-138">On the **Configure App URL** page, in the **Wikispaces Sign On URL** textbox, type your URL using the following pattern "*http://company.wikispaces.net*", and then click **Next**.</span></span>
   
    <span data-ttu-id="7e947-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787190.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="7e947-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787190.png "Configure App URL")</span></span>

4. <span data-ttu-id="7e947-140">On the **Configure single sign-on at Wikispaces** page, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7e947-140">On the **Configure single sign-on at Wikispaces** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="7e947-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787191.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e947-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787191.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="7e947-142">Send the metadatafile to the Wikispaces support team.</span><span class="sxs-lookup"><span data-stu-id="7e947-142">Send the metadatafile to the Wikispaces support team.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="7e947-143">The single sign-on configuration has to be performed by the Wikispaces support team.</span><span class="sxs-lookup"><span data-stu-id="7e947-143">The single sign-on configuration has to be performed by the Wikispaces support team.</span></span> <span data-ttu-id="7e947-144">You will get a notification as soon as the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="7e947-144">You will get a notification as soon as the configuration has been completed.</span></span>
    > 
    > 

6. <span data-ttu-id="7e947-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7e947-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="7e947-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787192.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7e947-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787192.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="7e947-147">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="7e947-147">Configuring user provisioning</span></span>
<span data-ttu-id="7e947-148">In order to enable Azure AD users to log into Wikispaces, they must be provisioned into Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="7e947-148">In order to enable Azure AD users to log into Wikispaces, they must be provisioned into Wikispaces.</span></span>  
<span data-ttu-id="7e947-149">In the case of Wikispaces, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7e947-149">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="7e947-150">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e947-150">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="7e947-151">Log in to your **Wikispaces** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7e947-151">Log in to your **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="7e947-152">Go to **Members**.</span><span class="sxs-lookup"><span data-stu-id="7e947-152">Go to **Members**.</span></span>
   
    <span data-ttu-id="7e947-153">![Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787193.png "Members")</span><span class="sxs-lookup"><span data-stu-id="7e947-153">![Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787193.png "Members")</span></span>

3. <span data-ttu-id="7e947-154">Click the **Invite People**.</span><span class="sxs-lookup"><span data-stu-id="7e947-154">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="7e947-155">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787194.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="7e947-155">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787194.png "Invite People")</span></span>

4. <span data-ttu-id="7e947-156">In the **Invite People** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e947-156">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="7e947-157">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787208.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="7e947-157">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787208.png "Invite People")</span></span>
   
    <span data-ttu-id="7e947-158">a.</span><span class="sxs-lookup"><span data-stu-id="7e947-158">a.</span></span> <span data-ttu-id="7e947-159">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="7e947-159">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="7e947-160">b.</span><span class="sxs-lookup"><span data-stu-id="7e947-160">b.</span></span> <span data-ttu-id="7e947-161">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="7e947-161">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="7e947-162">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="7e947-162">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

> [!NOTE]
> <span data-ttu-id="7e947-163">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7e947-163">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="7e947-164">Assigning users</span><span class="sxs-lookup"><span data-stu-id="7e947-164">Assigning users</span></span>
<span data-ttu-id="7e947-165">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="7e947-165">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-wikispaces-perform-the-following-steps"></a><span data-ttu-id="7e947-166">To assign users to Wikispaces, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e947-166">To assign users to Wikispaces, perform the following steps:</span></span>
1. <span data-ttu-id="7e947-167">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="7e947-167">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="7e947-168">On the \*\*Wikispaces \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="7e947-168">On the \*\*Wikispaces \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="7e947-169">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787195.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="7e947-169">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC787195.png "Assign Users")</span></span>

3. <span data-ttu-id="7e947-170">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="7e947-170">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="7e947-171">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="7e947-171">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wikispaces-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="7e947-172">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7e947-172">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7e947-173">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e947-173">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















