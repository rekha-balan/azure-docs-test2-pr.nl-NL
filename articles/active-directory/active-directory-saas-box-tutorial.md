---
title: 'Tutorial: Azure Active Directory integration with Box | Microsoft Docs'
description: Learn how to use Box with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: e2dc79f5adb8ce6cd1c6b155ce766e6d53ba01c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552934"
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="55ab1-103">Tutorial: Azure Active Directory integration with Box</span><span class="sxs-lookup"><span data-stu-id="55ab1-103">Tutorial: Azure Active Directory integration with Box</span></span>
<span data-ttu-id="55ab1-104">The objective of this tutorial is to show the integration of Azure and Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-104">The objective of this tutorial is to show the integration of Azure and Box.</span></span>  

<span data-ttu-id="55ab1-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="55ab1-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="55ab1-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="55ab1-106">A valid Azure subscription</span></span>
* <span data-ttu-id="55ab1-107">A test tenant in Box</span><span class="sxs-lookup"><span data-stu-id="55ab1-107">A test tenant in Box</span></span>

<span data-ttu-id="55ab1-108">After completing this tutorial, the Azure AD users you have assigned to Box will be able to single sign into the application at your Box company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55ab1-108">After completing this tutorial, the Azure AD users you have assigned to Box will be able to single sign into the application at your Box company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="55ab1-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="55ab1-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="55ab1-110">Enabling the application integration for Box</span><span class="sxs-lookup"><span data-stu-id="55ab1-110">Enabling the application integration for Box</span></span>
* <span data-ttu-id="55ab1-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="55ab1-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="55ab1-112">Configuring user and group provisioning</span><span class="sxs-lookup"><span data-stu-id="55ab1-112">Configuring user and group provisioning</span></span>
* <span data-ttu-id="55ab1-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="55ab1-113">Assigning users</span></span>

<span data-ttu-id="55ab1-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769537.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="55ab1-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769537.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-box"></a><span data-ttu-id="55ab1-115">Enable the application integration for Box</span><span class="sxs-lookup"><span data-stu-id="55ab1-115">Enable the application integration for Box</span></span>
<span data-ttu-id="55ab1-116">The objective of this section is to outline how to enable the application integration for Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-116">The objective of this section is to outline how to enable the application integration for Box.</span></span>

<span data-ttu-id="55ab1-117">**To enable the application integration for Box, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55ab1-117">**To enable the application integration for Box, perform the following steps:**</span></span>

1. <span data-ttu-id="55ab1-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="55ab1-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="55ab1-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="55ab1-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="55ab1-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="55ab1-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="55ab1-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="55ab1-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="55ab1-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="55ab1-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="55ab1-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="55ab1-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="55ab1-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="55ab1-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="55ab1-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="55ab1-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="55ab1-127">In the **search box**, type **Box**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-127">In the **search box**, type **Box**.</span></span>
   
   <span data-ttu-id="55ab1-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC701023.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="55ab1-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC701023.png "Application gallery")</span></span>
7. <span data-ttu-id="55ab1-129">In the results pane, select **box**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="55ab1-129">In the results pane, select **box**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="55ab1-130">![Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC701024.png "Box")</span><span class="sxs-lookup"><span data-stu-id="55ab1-130">![Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC701024.png "Box")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="55ab1-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="55ab1-131">Configure single sign-on</span></span>
<span data-ttu-id="55ab1-132">The objective of this section is to outline how to enable users to authenticate to Box with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="55ab1-132">The objective of this section is to outline how to enable users to authenticate to Box with their account in Azure AD using federation based on the SAML protocol.</span></span> 

<span data-ttu-id="55ab1-133">As part of this procedure, you are required to upload metadata to Box.com.</span><span class="sxs-lookup"><span data-stu-id="55ab1-133">As part of this procedure, you are required to upload metadata to Box.com.</span></span>

<span data-ttu-id="55ab1-134">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55ab1-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="55ab1-135">In the Azure classic portal, on the **Box** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="55ab1-135">In the Azure classic portal, on the **Box** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="55ab1-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769538.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="55ab1-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769538.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="55ab1-137">On the **How would you like users to sign on to Box** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-137">On the **How would you like users to sign on to Box** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="55ab1-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769539.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="55ab1-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769539.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="55ab1-139">On the **Configure App URL** page, in the **Box Tenant URL** textbox, type your Box tenant URL (e.g.: https://<mydomainname>.box.com), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-139">On the **Configure App URL** page, in the **Box Tenant URL** textbox, type your Box tenant URL (e.g.: https://<mydomainname>.box.com), and then click **Next**.</span></span>
   
  <span data-ttu-id="55ab1-140">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC669826.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="55ab1-140">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC669826.png "Configure app URL")</span></span>
4. <span data-ttu-id="55ab1-141">On the **Configure single sign-on at Box** page, to download your metadata, click **Download metadata**, and then the data file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="55ab1-141">On the **Configure single sign-on at Box** page, to download your metadata, click **Download metadata**, and then the data file locally on your computer.</span></span>
   
  <span data-ttu-id="55ab1-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC669824.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="55ab1-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC669824.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="55ab1-143">Forward that metadata file to Box support team.</span><span class="sxs-lookup"><span data-stu-id="55ab1-143">Forward that metadata file to Box support team.</span></span> <span data-ttu-id="55ab1-144">The support team needs configures single sign-on for you.</span><span class="sxs-lookup"><span data-stu-id="55ab1-144">The support team needs configures single sign-on for you.</span></span>
6. <span data-ttu-id="55ab1-145">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="55ab1-145">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
  <span data-ttu-id="55ab1-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769540.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="55ab1-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769540.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="55ab1-147">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="55ab1-147">Configure user provisioning</span></span>

<span data-ttu-id="55ab1-148">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-148">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

<span data-ttu-id="55ab1-149">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55ab1-149">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="55ab1-150">In the Azure classic portal, on the **Box** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="55ab1-150">In the Azure classic portal, on the **Box** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span> 
   
    <span data-ttu-id="55ab1-151">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769541.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="55ab1-151">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769541.png "Enable automatic user provisioning")</span></span>
2. <span data-ttu-id="55ab1-152">On the **Enable user provisioning to Box** dialog page, click **Enable user provisioning**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-152">On the **Enable user provisioning to Box** dialog page, click **Enable user provisioning**.</span></span> 
   
    <span data-ttu-id="55ab1-153">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769544.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="55ab1-153">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769544.png "Enable automatic user provisioning")</span></span>
3. <span data-ttu-id="55ab1-154">On the **Log in to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-154">On the **Log in to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="55ab1-155">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769546.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="55ab1-155">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>
4. <span data-ttu-id="55ab1-156">Click **Grant access to Box** to authorize this operation and to return to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="55ab1-156">Click **Grant access to Box** to authorize this operation and to return to the Azure classic portal.</span></span> 
   
    <span data-ttu-id="55ab1-157">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769549.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="55ab1-157">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>
5. <span data-ttu-id="55ab1-158">On the **Provisioning Options** page, the **Object types to provision** checkboxes allow you to select whether or not group objects are provisioned to Box in addition to user objects.</span><span class="sxs-lookup"><span data-stu-id="55ab1-158">On the **Provisioning Options** page, the **Object types to provision** checkboxes allow you to select whether or not group objects are provisioned to Box in addition to user objects.</span></span>  <span data-ttu-id="55ab1-159">See "Assigning users and groups section" below for more information.</span><span class="sxs-lookup"><span data-stu-id="55ab1-159">See "Assigning users and groups section" below for more information.</span></span>
6. <span data-ttu-id="55ab1-160">To finish the configuration, click the Complete button.</span><span class="sxs-lookup"><span data-stu-id="55ab1-160">To finish the configuration, click the Complete button.</span></span> 
   
    <span data-ttu-id="55ab1-161">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769551.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="55ab1-161">![Enable automatic user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769551.png "Enable automatic user provisioning")</span></span>

## <a name="assign-a-test-user"></a><span data-ttu-id="55ab1-162">Assign a test user</span><span class="sxs-lookup"><span data-stu-id="55ab1-162">Assign a test user</span></span>
<span data-ttu-id="55ab1-163">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="55ab1-163">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="55ab1-164">**To assign users to Box, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55ab1-164">**To assign users to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="55ab1-165">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="55ab1-165">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="55ab1-166">On the \*\*Box \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-166">On the \*\*Box \*\*application integration page, click **Assign users**.</span></span> 
   
    <span data-ttu-id="55ab1-167">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769552.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="55ab1-167">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769552.png "Assign users")</span></span>
3. <span data-ttu-id="55ab1-168">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="55ab1-168">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span> 
   
   <span data-ttu-id="55ab1-169">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="55ab1-169">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="55ab1-170">You should now wait for 10 minutes and verify that the account has been synchronized to Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-170">You should now wait for 10 minutes and verify that the account has been synchronized to Box.</span></span>

<span data-ttu-id="55ab1-171">As a first verification step, you can check the provisioning status, by clicking Dashboard in the D on the Box application integration page on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="55ab1-171">As a first verification step, you can check the provisioning status, by clicking Dashboard in the D on the Box application integration page on the Azure classic portal.</span></span>

<span data-ttu-id="55ab1-172">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769553.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="55ab1-172">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769553.png "Dashboard")</span></span>

<span data-ttu-id="55ab1-173">A successfully completed user provisioning cycle is indicated by a related status:</span><span class="sxs-lookup"><span data-stu-id="55ab1-173">A successfully completed user provisioning cycle is indicated by a related status:</span></span>

<span data-ttu-id="55ab1-174">![Integration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769555.png "Integration status")</span><span class="sxs-lookup"><span data-stu-id="55ab1-174">![Integration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769555.png "Integration status")</span></span>

<span data-ttu-id="55ab1-175">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="55ab1-175">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="55ab1-176">![Integration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769556.png "Integration status")</span><span class="sxs-lookup"><span data-stu-id="55ab1-176">![Integration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-box-tutorial/IC769556.png "Integration status")</span></span>

## <a name="assign-users-and-groups"></a><span data-ttu-id="55ab1-177">Assign users and groups</span><span class="sxs-lookup"><span data-stu-id="55ab1-177">Assign users and groups</span></span>
<span data-ttu-id="55ab1-178">The **Box > Users and Groups** tab in the Azure classic portal allows you to specify which users and groups should be granted access to Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-178">The **Box > Users and Groups** tab in the Azure classic portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="55ab1-179">Assignment of a user or group causes the following things to occur:</span><span class="sxs-lookup"><span data-stu-id="55ab1-179">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="55ab1-180">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-180">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="55ab1-181">If a user is not assigned, then Azure AD will not permit them to sign in to Box and will return an error on the Azure AD sign-in page.</span><span class="sxs-lookup"><span data-stu-id="55ab1-181">If a user is not assigned, then Azure AD will not permit them to sign in to Box and will return an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="55ab1-182">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="55ab1-182">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="55ab1-183">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span><span class="sxs-lookup"><span data-stu-id="55ab1-183">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="55ab1-184">If only user objects were configured to be provisioned, then all directly-assigned users are placed in the provisioning queue, and all users that are members of any assigned groups will be placed in the provisioning queue.</span><span class="sxs-lookup"><span data-stu-id="55ab1-184">If only user objects were configured to be provisioned, then all directly-assigned users are placed in the provisioning queue, and all users that are members of any assigned groups will be placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="55ab1-185">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, as well as all users that are members of those groups.</span><span class="sxs-lookup"><span data-stu-id="55ab1-185">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, as well as all users that are members of those groups.</span></span> <span data-ttu-id="55ab1-186">The group and user memberships are preserved upon being written to Box.</span><span class="sxs-lookup"><span data-stu-id="55ab1-186">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="55ab1-187">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span><span class="sxs-lookup"><span data-stu-id="55ab1-187">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span> <span data-ttu-id="55ab1-188">See the resources below for more information.</span><span class="sxs-lookup"><span data-stu-id="55ab1-188">See the resources below for more information.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55ab1-189">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="55ab1-189">Additional Resources</span></span>
* [<span data-ttu-id="55ab1-190">Customizing claims issued in the SAML token</span><span class="sxs-lookup"><span data-stu-id="55ab1-190">Customizing claims issued in the SAML token</span></span>](active-directory-saml-claims-customization.md)
* [<span data-ttu-id="55ab1-191">Provisioning: Customize Attribute Mappings</span><span class="sxs-lookup"><span data-stu-id="55ab1-191">Provisioning: Customize Attribute Mappings</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="55ab1-192">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55ab1-192">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55ab1-193">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55ab1-193">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)























