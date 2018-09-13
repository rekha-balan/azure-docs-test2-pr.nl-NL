---
title: 'Tutorial: Azure Active Directory integration with Clever | Microsoft Docs'
description: Learn how to use Clever with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 67baf0699a872dd9c057b4ee915462a2c75de361
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549379"
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="5dc5a-103">Tutorial: Azure Active Directory integration with Clever</span><span class="sxs-lookup"><span data-stu-id="5dc5a-103">Tutorial: Azure Active Directory integration with Clever</span></span>
<span data-ttu-id="5dc5a-104">The objective of this tutorial is to show the integration of Azure and Clever.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-104">The objective of this tutorial is to show the integration of Azure and Clever.</span></span> <span data-ttu-id="5dc5a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="5dc5a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5dc5a-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5dc5a-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5dc5a-107">A Clever tenant</span><span class="sxs-lookup"><span data-stu-id="5dc5a-107">A Clever tenant</span></span>

<span data-ttu-id="5dc5a-108">After completing this tutorial, the Azure AD users you have assigned to Clever will be able to single sign into the application at your Clever company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5dc5a-108">After completing this tutorial, the Azure AD users you have assigned to Clever will be able to single sign into the application at your Clever company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5dc5a-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5dc5a-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="5dc5a-110">Enabling the application integration for Clever</span><span class="sxs-lookup"><span data-stu-id="5dc5a-110">Enabling the application integration for Clever</span></span>
* <span data-ttu-id="5dc5a-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="5dc5a-111">Configuring single sign-on</span></span>
* <span data-ttu-id="5dc5a-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5dc5a-112">Configuring user provisioning</span></span>
* <span data-ttu-id="5dc5a-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5dc5a-113">Assigning users</span></span>

<span data-ttu-id="5dc5a-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798977.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798977.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-clever"></a><span data-ttu-id="5dc5a-115">Enable the application integration for Clever</span><span class="sxs-lookup"><span data-stu-id="5dc5a-115">Enable the application integration for Clever</span></span>
<span data-ttu-id="5dc5a-116">The objective of this section is to outline how to enable the application integration for Clever.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-116">The objective of this section is to outline how to enable the application integration for Clever.</span></span>

<span data-ttu-id="5dc5a-117">**To enable the application integration for Clever, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5dc5a-117">**To enable the application integration for Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="5dc5a-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5dc5a-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5dc5a-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5dc5a-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5dc5a-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5dc5a-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5dc5a-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5dc5a-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5dc5a-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5dc5a-127">In the **search box**, type **Clever**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-127">In the **search box**, type **Clever**.</span></span>
   
   <span data-ttu-id="5dc5a-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798978.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798978.png "Application Gallery")</span></span>
7. <span data-ttu-id="5dc5a-129">In the results pane, select **Clever**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-129">In the results pane, select **Clever**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5dc5a-130">![Clever](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798979.png "Clever")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-130">![Clever](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798979.png "Clever")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5dc5a-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="5dc5a-131">Configure single sign-on</span></span>

<span data-ttu-id="5dc5a-132">The objective of this section is to outline how to enable users to authenticate to Clever with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-132">The objective of this section is to outline how to enable users to authenticate to Clever with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="5dc5a-133">Your Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-133">Your Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>  

<span data-ttu-id="5dc5a-134">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="5dc5a-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798980.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798980.png "Attributes")</span></span>

<span data-ttu-id="5dc5a-136">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5dc5a-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="5dc5a-137">In the Azure classic portal, on the **Clever** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-137">In the Azure classic portal, on the **Clever** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5dc5a-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC784682.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC784682.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="5dc5a-139">On the **How would you like users to sign on to Clever** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-139">On the **How would you like users to sign on to Clever** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5dc5a-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798981.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798981.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="5dc5a-141">On the **Configure App URL** page, in the **Clever Sign On URL** textbox, type the URL used by your users to sign-on to your Clever application (e.g.: *https://clever.com/in/azsandbox*), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-141">On the **Configure App URL** page, in the **Clever Sign On URL** textbox, type the URL used by your users to sign-on to your Clever application (e.g.: *https://clever.com/in/azsandbox*), and then click **Next**.</span></span>
   
   <span data-ttu-id="5dc5a-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798982.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798982.png "Configure App URL")</span></span>
4. <span data-ttu-id="5dc5a-143">On the **Configure single sign-on at Clever** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-143">On the **Configure single sign-on at Clever** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="5dc5a-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798983.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798983.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="5dc5a-145">In a different web browser window, log into your Clever company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-145">In a different web browser window, log into your Clever company site as an administrator.</span></span>
6. <span data-ttu-id="5dc5a-146">In the toolbar, click **Instant Login**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-146">In the toolbar, click **Instant Login**.</span></span>
   
   <span data-ttu-id="5dc5a-147">![Instant Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798984.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-147">![Instant Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798984.png "Instant Login")</span></span>
7. <span data-ttu-id="5dc5a-148">On the **Instant Login** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5dc5a-148">On the **Instant Login** page, perform the following steps:</span></span>
   
   <span data-ttu-id="5dc5a-149">![Instant Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798985.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-149">![Instant Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798985.png "Instant Login")</span></span>
   
   1. <span data-ttu-id="5dc5a-150">Type the **Login URL**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-150">Type the **Login URL**.</span></span>  
   
      >[!NOTE]
      ><span data-ttu-id="5dc5a-151">The **Login URL** is a custom value.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-151">The **Login URL** is a custom value.</span></span> <span data-ttu-id="5dc5a-152">You can get the actual value from your Clever support team.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-152">You can get the actual value from your Clever support team.</span></span>
      > 
   2. <span data-ttu-id="5dc5a-153">As **Identity System**, select **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-153">As **Identity System**, select **ADFS**.</span></span>
   3. <span data-ttu-id="5dc5a-154">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-154">Click **Save**.</span></span>
8. <span data-ttu-id="5dc5a-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5dc5a-156">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798986.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-156">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798986.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="5dc5a-157">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-157">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="5dc5a-158">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC795920.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-158">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC795920.png "Attributes")</span></span>
10. <span data-ttu-id="5dc5a-159">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5dc5a-159">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="5dc5a-160">![saml token attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC795921.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-160">![saml token attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC795921.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="5dc5a-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="5dc5a-161">Attribute Name</span></span> | <span data-ttu-id="5dc5a-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="5dc5a-162">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5dc5a-163">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="5dc5a-163">clever.student.credentials.district\_username</span></span> |<span data-ttu-id="5dc5a-164">User.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="5dc5a-164">User.userprincipalname</span></span> |
    
    1. <span data-ttu-id="5dc5a-165">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-165">For each data row in the table above, click **add user attribute**.</span></span>
    2. <span data-ttu-id="5dc5a-166">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-166">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    3. <span data-ttu-id="5dc5a-167">In the **Attribute Value** textbox, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-167">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    4. <span data-ttu-id="5dc5a-168">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-168">Click **Complete**.</span></span>
11. <span data-ttu-id="5dc5a-169">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-169">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="5dc5a-170">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="5dc5a-170">Configure user provisioning</span></span>
<span data-ttu-id="5dc5a-171">In order to enable Azure AD users to log into Clever, they must be provisioned into Clever.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-171">In order to enable Azure AD users to log into Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="5dc5a-172">In the case of Clever, provisioning is a manual task that needs to be performed by your Clever support team.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-172">In the case of Clever, provisioning is a manual task that needs to be performed by your Clever support team.</span></span>

>[!NOTE]
><span data-ttu-id="5dc5a-173">You can use any other Clever user account creation tools or APIs provided by Clever to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-173">You can use any other Clever user account creation tools or APIs provided by Clever to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="5dc5a-174">Assign users</span><span class="sxs-lookup"><span data-stu-id="5dc5a-174">Assign users</span></span>
<span data-ttu-id="5dc5a-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="5dc5a-176">**To assign users to Clever, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5dc5a-176">**To assign users to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="5dc5a-177">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-177">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5dc5a-178">On the **Clever** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-178">On the **Clever** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5dc5a-179">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798987.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-179">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC798987.png "Assign Users")</span></span>
3. <span data-ttu-id="5dc5a-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5dc5a-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="5dc5a-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clever-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5dc5a-182">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5dc5a-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5dc5a-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5dc5a-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















