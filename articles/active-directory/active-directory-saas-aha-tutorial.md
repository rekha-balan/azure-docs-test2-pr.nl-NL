---
title: 'Tutorial: Azure Active Directory integration with Aha! | Microsoft Docs'
description: Learn how to use Aha! with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 5077fcbb2c8bc09d3d493b252cc0d0ee47ef1e39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540666"
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="f9274-105">Tutorial: Azure Active Directory integration with Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-105">Tutorial: Azure Active Directory integration with Aha!</span></span>
<span data-ttu-id="f9274-106">The objective of this tutorial is to show the integration of Azure and Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-106">The objective of this tutorial is to show the integration of Azure and Aha!</span></span>  
<span data-ttu-id="f9274-107">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="f9274-107">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="f9274-108">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f9274-108">A valid Azure subscription</span></span>
* <span data-ttu-id="f9274-109">An Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-109">An Aha!</span></span> <span data-ttu-id="f9274-110">single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f9274-110">single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="f9274-111">After completing this tutorial, the Azure AD users you have assigned to Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-111">After completing this tutorial, the Azure AD users you have assigned to Aha!</span></span> <span data-ttu-id="f9274-112">will be able to single sign into the application at your Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-112">will be able to single sign into the application at your Aha!</span></span> <span data-ttu-id="f9274-113">company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9274-113">company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="f9274-114">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f9274-114">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="f9274-115">Enabling the application integration for Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-115">Enabling the application integration for Aha!</span></span>
* <span data-ttu-id="f9274-116">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="f9274-116">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="f9274-117">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="f9274-117">Configuring user provisioning</span></span>
* <span data-ttu-id="f9274-118">Assigning users</span><span class="sxs-lookup"><span data-stu-id="f9274-118">Assigning users</span></span>

<span data-ttu-id="f9274-119">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798944.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="f9274-119">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798944.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-aha"></a><span data-ttu-id="f9274-120">Enable the application integration for Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-120">Enable the application integration for Aha!</span></span>
<span data-ttu-id="f9274-121">The objective of this section is to outline how to enable the application integration for Aha!.</span><span class="sxs-lookup"><span data-stu-id="f9274-121">The objective of this section is to outline how to enable the application integration for Aha!.</span></span>

<span data-ttu-id="f9274-122">**To enable the application integration for Aha!, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9274-122">**To enable the application integration for Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="f9274-123">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9274-123">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="f9274-124">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f9274-124">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f9274-125">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f9274-125">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f9274-126">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f9274-126">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="f9274-127">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="f9274-127">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f9274-128">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f9274-128">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="f9274-129">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="f9274-129">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f9274-130">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f9274-130">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="f9274-131">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="f9274-131">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f9274-132">In the **search box**, type **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="f9274-132">In the **search box**, type **Aha!**.</span></span>
   
   <span data-ttu-id="f9274-133">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798945.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="f9274-133">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798945.png "Application Gallery")</span></span>
7. <span data-ttu-id="f9274-134">In the results pane, select **Aha!**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f9274-134">In the results pane, select **Aha!**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="f9274-135">![Aha!](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC802746.png "Aha!")</span><span class="sxs-lookup"><span data-stu-id="f9274-135">![Aha!](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC802746.png "Aha!")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f9274-136">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="f9274-136">Configure single sign-on</span></span>

<span data-ttu-id="f9274-137">The objective of this section is to outline how to enable users to authenticate to Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-137">The objective of this section is to outline how to enable users to authenticate to Aha!</span></span> <span data-ttu-id="f9274-138">with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="f9274-138">with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="f9274-139">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9274-139">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="f9274-140">In the Azure classic portal, on the **Aha!**</span><span class="sxs-lookup"><span data-stu-id="f9274-140">In the Azure classic portal, on the **Aha!**</span></span> <span data-ttu-id="f9274-141">application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="f9274-141">application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="f9274-142">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798946.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f9274-142">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798946.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="f9274-143">On the **How would you like users to sign on to Aha!**</span><span class="sxs-lookup"><span data-stu-id="f9274-143">On the **How would you like users to sign on to Aha!**</span></span> <span data-ttu-id="f9274-144">page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9274-144">page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="f9274-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798947.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f9274-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798947.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="f9274-146">On the **Configure App URL** page, in the **Aha! Sign On URL** textbox, type the URL used by your users to sign-on to your Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-146">On the **Configure App URL** page, in the **Aha! Sign On URL** textbox, type the URL used by your users to sign-on to your Aha!</span></span> <span data-ttu-id="f9274-147">Application (e.g.: "*https://company.aha.io/session/new*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9274-147">Application (e.g.: "*https://company.aha.io/session/new*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="f9274-148">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798948.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="f9274-148">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798948.png "Configure App URL")</span></span>
4. <span data-ttu-id="f9274-149">On the **Configure single sign-on at Aha!**</span><span class="sxs-lookup"><span data-stu-id="f9274-149">On the **Configure single sign-on at Aha!**</span></span> <span data-ttu-id="f9274-150">page, to download your metadata file, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="f9274-150">page, to download your metadata file, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="f9274-151">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798949.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f9274-151">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798949.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="f9274-152">In a different web browser window, log into your Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-152">In a different web browser window, log into your Aha!</span></span> <span data-ttu-id="f9274-153">company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f9274-153">company site as an administrator.</span></span>
6. <span data-ttu-id="f9274-154">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f9274-154">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="f9274-155">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="f9274-155">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>
7. <span data-ttu-id="f9274-156">Click **Account**.</span><span class="sxs-lookup"><span data-stu-id="f9274-156">Click **Account**.</span></span>
   
   <span data-ttu-id="f9274-157">![Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span><span class="sxs-lookup"><span data-stu-id="f9274-157">![Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>
8. <span data-ttu-id="f9274-158">Click **Security and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f9274-158">Click **Security and single sign-on**.</span></span>
   
   <span data-ttu-id="f9274-159">![Security and single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f9274-159">![Security and single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>
9. <span data-ttu-id="f9274-160">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="f9274-160">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
   <span data-ttu-id="f9274-161">![Security and single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span><span class="sxs-lookup"><span data-stu-id="f9274-161">![Security and single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>
10. <span data-ttu-id="f9274-162">On the **Single Sign-On** configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f9274-162">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
   <span data-ttu-id="f9274-163">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f9274-163">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>    
    1. <span data-ttu-id="f9274-164">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="f9274-164">In the **Name** textbox, type a name for your configuration.</span></span>
    2. <span data-ttu-id="f9274-165">For **Configure using**, select **Metadata File**.</span><span class="sxs-lookup"><span data-stu-id="f9274-165">For **Configure using**, select **Metadata File**.</span></span>
    3. <span data-ttu-id="f9274-166">To upload your downloaded metadata file, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="f9274-166">To upload your downloaded metadata file, click **Browse**.</span></span>
    4. <span data-ttu-id="f9274-167">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="f9274-167">Click **Update**.</span></span>
11. <span data-ttu-id="f9274-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="f9274-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="f9274-169">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798955.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f9274-169">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798955.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="f9274-170">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="f9274-170">Configure user provisioning</span></span>

<span data-ttu-id="f9274-171">In order to enable Azure AD users to log into Aha!, they must be provisioned into Aha!.</span><span class="sxs-lookup"><span data-stu-id="f9274-171">In order to enable Azure AD users to log into Aha!, they must be provisioned into Aha!.</span></span>  

* <span data-ttu-id="f9274-172">In the case of Aha!, provisioning is an automated task.</span><span class="sxs-lookup"><span data-stu-id="f9274-172">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="f9274-173">There is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="f9274-173">There is no action item for you.</span></span>

<span data-ttu-id="f9274-174">Users are automatically created if necessary during the first single sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="f9274-174">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="f9274-175">You can use any other Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-175">You can use any other Aha!</span></span> <span data-ttu-id="f9274-176">user account creation tools or APIs provided by Aha!</span><span class="sxs-lookup"><span data-stu-id="f9274-176">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="f9274-177">to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="f9274-177">to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="f9274-178">Assign users</span><span class="sxs-lookup"><span data-stu-id="f9274-178">Assign users</span></span>
<span data-ttu-id="f9274-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="f9274-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="f9274-180">**To assign users to Aha!, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9274-180">**To assign users to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="f9274-181">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="f9274-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f9274-182">On the **Aha!**</span><span class="sxs-lookup"><span data-stu-id="f9274-182">On the **Aha!**</span></span> <span data-ttu-id="f9274-183">application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="f9274-183">application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f9274-184">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798956.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="f9274-184">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC798956.png "Assign Users")</span></span>
3. <span data-ttu-id="f9274-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="f9274-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="f9274-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="f9274-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aha-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f9274-187">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f9274-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f9274-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9274-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















