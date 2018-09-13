---
title: 'Tutorial: Azure Active Directory integration with Thoughtworks Mingle | Microsoft Docs'
description: Learn how to use Thoughtworks Mingle with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: db1540ec6c0aabd628e7975bc8f9ec95a1705a39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662427"
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="b9efc-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b9efc-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>
<span data-ttu-id="b9efc-104">The objective of this tutorial is to show the integration of Azure and Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="b9efc-104">The objective of this tutorial is to show the integration of Azure and Thoughtworks Mingle.</span></span>  

<span data-ttu-id="b9efc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="b9efc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b9efc-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b9efc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b9efc-107">A Thoughtworks Mingle tenant</span><span class="sxs-lookup"><span data-stu-id="b9efc-107">A Thoughtworks Mingle tenant</span></span>

<span data-ttu-id="b9efc-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9efc-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="b9efc-109">Enabling the application integration for Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b9efc-109">Enabling the application integration for Thoughtworks Mingle</span></span>
2. <span data-ttu-id="b9efc-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="b9efc-110">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="b9efc-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="b9efc-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="b9efc-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="b9efc-112">Assigning users</span></span>

<span data-ttu-id="b9efc-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785150.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="b9efc-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785150.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-thoughtworks-mingle"></a><span data-ttu-id="b9efc-114">Enable the application integration for Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b9efc-114">Enable the application integration for Thoughtworks Mingle</span></span>
<span data-ttu-id="b9efc-115">The objective of this section is to outline how to enable the application integration for Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="b9efc-115">The objective of this section is to outline how to enable the application integration for Thoughtworks Mingle.</span></span>

<span data-ttu-id="b9efc-116">**To enable the application integration for Thoughtworks Mingle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9efc-116">**To enable the application integration for Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="b9efc-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="b9efc-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b9efc-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="b9efc-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b9efc-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b9efc-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b9efc-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="b9efc-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="b9efc-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="b9efc-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b9efc-122">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="b9efc-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="b9efc-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="b9efc-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="b9efc-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="b9efc-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="b9efc-126">In the **search box**, type **thoughtworks mingle**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-126">In the **search box**, type **thoughtworks mingle**.</span></span>
   
    <span data-ttu-id="b9efc-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785151.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="b9efc-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785151.png "Application Gallery")</span></span>

7. <span data-ttu-id="b9efc-128">In the results pane, select **Thoughtworks Mingle**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b9efc-128">In the results pane, select **Thoughtworks Mingle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="b9efc-129">![Thoughtworks Mingle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785152.png "Thoughtworks Mingle")</span><span class="sxs-lookup"><span data-stu-id="b9efc-129">![Thoughtworks Mingle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785152.png "Thoughtworks Mingle")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="b9efc-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9efc-130">Configure single sign-on</span></span>
<span data-ttu-id="b9efc-131">The objective of this section is to outline how to enable users to authenticate to Thoughtworks Mingle with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="b9efc-131">The objective of this section is to outline how to enable users to authenticate to Thoughtworks Mingle with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="b9efc-132">As part of this procedure, you are required to upload a certificate to Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="b9efc-132">As part of this procedure, you are required to upload a certificate to Thoughtworks Mingle.</span></span>

<span data-ttu-id="b9efc-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9efc-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="b9efc-134">In the Azure classic portal, on the \*\*Thoughtworks Mingle \*\*application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9efc-134">In the Azure classic portal, on the \*\*Thoughtworks Mingle \*\*application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b9efc-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785153.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="b9efc-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785153.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="b9efc-136">On the **How would you like users to sign on to Thoughtworks Mingle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-136">On the **How would you like users to sign on to Thoughtworks Mingle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="b9efc-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785154.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="b9efc-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785154.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="b9efc-138">On the **Configure App URL** page, in the **Thoughtworks Mingle Tenant URL** textbox, type your URL using the following pattern "*http://company.mingle.thoughtworks.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-138">On the **Configure App URL** page, in the **Thoughtworks Mingle Tenant URL** textbox, type your URL using the following pattern "*http://company.mingle.thoughtworks.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="b9efc-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785155.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="b9efc-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785155.png "Configure App URL")</span></span>

4. <span data-ttu-id="b9efc-140">On the **Configure single sign-on at Thoughtworks Mingle** page, click Download metadata, and then save it on your computer.</span><span class="sxs-lookup"><span data-stu-id="b9efc-140">On the **Configure single sign-on at Thoughtworks Mingle** page, click Download metadata, and then save it on your computer.</span></span>
   
    <span data-ttu-id="b9efc-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785156.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="b9efc-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785156.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="b9efc-142">Log in to your **Thoughtworks Mingle** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="b9efc-142">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

6. <span data-ttu-id="b9efc-143">Click the **Admin** tab, and then, click **SSO Config**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-143">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="b9efc-144">![SSO Config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785157.png "SSO Config")</span><span class="sxs-lookup"><span data-stu-id="b9efc-144">![SSO Config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785157.png "SSO Config")</span></span>

7. <span data-ttu-id="b9efc-145">In the **SSO Config** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9efc-145">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b9efc-146">![SSO Config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785158.png "SSO Config")</span><span class="sxs-lookup"><span data-stu-id="b9efc-146">![SSO Config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785158.png "SSO Config")</span></span>   
 1. <span data-ttu-id="b9efc-147">To upload the metadata file, click **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-147">To upload the metadata file, click **Choose file**.</span></span> 
 2. <span data-ttu-id="b9efc-148">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-148">Click **Save Changes**.</span></span>

8. <span data-ttu-id="b9efc-149">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9efc-149">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b9efc-150">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785159.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="b9efc-150">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785159.png "Configure single sign-on")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="b9efc-151">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="b9efc-151">Configure user provisioning</span></span>
<span data-ttu-id="b9efc-152">For AAD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span><span class="sxs-lookup"><span data-stu-id="b9efc-152">For AAD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span>  

* <span data-ttu-id="b9efc-153">In the case of Thoughtworks Mingle, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="b9efc-153">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="b9efc-154">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9efc-154">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b9efc-155">Log in to your Thoughtworks Mingle company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="b9efc-155">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="b9efc-156">Click **Profile**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-156">Click **Profile**.</span></span>
   
    <span data-ttu-id="b9efc-157">![Your First Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785160.png "Your First Project")</span><span class="sxs-lookup"><span data-stu-id="b9efc-157">![Your First Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785160.png "Your First Project")</span></span>

3. <span data-ttu-id="b9efc-158">Click the **Admin** tab, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-158">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="b9efc-159">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785161.png "Users")</span><span class="sxs-lookup"><span data-stu-id="b9efc-159">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785161.png "Users")</span></span>

4. <span data-ttu-id="b9efc-160">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-160">Click **New User**.</span></span>
   
    <span data-ttu-id="b9efc-161">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785162.png "New User")</span><span class="sxs-lookup"><span data-stu-id="b9efc-161">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785162.png "New User")</span></span>

5. <span data-ttu-id="b9efc-162">On the **New User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9efc-162">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="b9efc-163">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785163.png "New User")</span><span class="sxs-lookup"><span data-stu-id="b9efc-163">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785163.png "New User")</span></span>   
  1. <span data-ttu-id="b9efc-164">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="b9efc-164">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid AAD account you want to provision into the related textboxes.</span></span> 
  2. <span data-ttu-id="b9efc-165">As **User type**, select **Full user**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-165">As **User type**, select **Full user**.</span></span>
  3. <span data-ttu-id="b9efc-166">Click **Create This Profile**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-166">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="b9efc-167">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="b9efc-167">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="b9efc-168">Assign users</span><span class="sxs-lookup"><span data-stu-id="b9efc-168">Assign users</span></span>
<span data-ttu-id="b9efc-169">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="b9efc-169">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="b9efc-170">**To assign users to Thoughtworks Mingle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9efc-170">**To assign users to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="b9efc-171">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="b9efc-171">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="b9efc-172">On the **Thoughtworks Mingle** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="b9efc-172">On the **Thoughtworks Mingle** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="b9efc-173">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785164.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="b9efc-173">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC785164.png "Assign Users")</span></span>

3. <span data-ttu-id="b9efc-174">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="b9efc-174">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="b9efc-175">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="b9efc-175">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thoughtworks-mingle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b9efc-176">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b9efc-176">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b9efc-177">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9efc-177">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















