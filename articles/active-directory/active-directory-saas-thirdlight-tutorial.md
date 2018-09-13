---
title: 'Tutorial: Azure Active Directory Integration with Thirdlight | Microsoft Docs'
description: Learn how to use Thirdlight with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/07/2017
ms.author: jeedes
ms.openlocfilehash: 4c47af02143e1c12b7f06933a1c776228c81db19
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550611"
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="0f9b7-103">Tutorial: Azure Active Directory Integration with Thirdlight</span><span class="sxs-lookup"><span data-stu-id="0f9b7-103">Tutorial: Azure Active Directory Integration with Thirdlight</span></span>
<span data-ttu-id="0f9b7-104">The objective of this tutorial is to show the integration of Azure and Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-104">The objective of this tutorial is to show the integration of Azure and Thirdlight.</span></span>  

<span data-ttu-id="0f9b7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="0f9b7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="0f9b7-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0f9b7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="0f9b7-107">A Thirdlight single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0f9b7-107">A Thirdlight single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="0f9b7-108">After completing this tutorial, the Azure AD users you have assigned to Thirdlight will be able to sign into the application using SSO at your Thirdlight company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0f9b7-108">After completing this tutorial, the Azure AD users you have assigned to Thirdlight will be able to sign into the application using SSO at your Thirdlight company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="0f9b7-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0f9b7-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="0f9b7-110">Enabling the application integration for Thirdlight</span><span class="sxs-lookup"><span data-stu-id="0f9b7-110">Enabling the application integration for Thirdlight</span></span>
2. <span data-ttu-id="0f9b7-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="0f9b7-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="0f9b7-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="0f9b7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="0f9b7-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="0f9b7-113">Assigning users</span></span>

<span data-ttu-id="0f9b7-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805836.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805836.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-thirdlight"></a><span data-ttu-id="0f9b7-115">Enable the application integration for Thirdlight</span><span class="sxs-lookup"><span data-stu-id="0f9b7-115">Enable the application integration for Thirdlight</span></span>
<span data-ttu-id="0f9b7-116">The objective of this section is to outline how to enable the application integration for Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-116">The objective of this section is to outline how to enable the application integration for Thirdlight.</span></span>

<span data-ttu-id="0f9b7-117">**To enable the application integration for Thirdlight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0f9b7-117">**To enable the application integration for Thirdlight, perform the following steps:**</span></span>

1. <span data-ttu-id="0f9b7-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="0f9b7-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="0f9b7-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="0f9b7-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="0f9b7-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="0f9b7-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="0f9b7-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="0f9b7-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="0f9b7-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="0f9b7-127">In the **search box**, type **Thirdlight**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-127">In the **search box**, type **Thirdlight**.</span></span>
   
    <span data-ttu-id="0f9b7-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805837.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805837.png "Application Gallery")</span></span>

7. <span data-ttu-id="0f9b7-129">In the results pane, select **Thirdlight**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-129">In the results pane, select **Thirdlight**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="0f9b7-130">![ThirdLight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805838.png "ThirdLight")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-130">![ThirdLight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805838.png "ThirdLight")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="0f9b7-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="0f9b7-131">Configure single sign-on</span></span>
<span data-ttu-id="0f9b7-132">The objective of this section is to outline how to enable users to authenticate to Thirdlight with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-132">The objective of this section is to outline how to enable users to authenticate to Thirdlight with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="0f9b7-133">Configuring SSO for Thirdlight requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-133">Configuring SSO for Thirdlight requires you to retrieve a thumbprint value from a certificate.</span></span>

<span data-ttu-id="0f9b7-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="0f9b7-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="0f9b7-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0f9b7-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="0f9b7-136">In the Azure classic portal, on the **Thirdlight** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-136">In the Azure classic portal, on the **Thirdlight** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="0f9b7-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805839.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805839.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="0f9b7-138">On the **How would you like users to sign on to Thirdlight** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-138">On the **How would you like users to sign on to Thirdlight** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="0f9b7-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805840.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805840.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="0f9b7-140">On the **Configure App URL** page, in the **Thirdlight Sign In URL** textbox, type your URL used by your users to sign on to your Thirdlight application (e.g.: "*http://azuresso2.thirdlight.com/*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-140">On the **Configure App URL** page, in the **Thirdlight Sign In URL** textbox, type your URL used by your users to sign on to your Thirdlight application (e.g.: "*http://azuresso2.thirdlight.com/*"), and then click **Next**.</span></span>
   
    <span data-ttu-id="0f9b7-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805841.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805841.png "Configure App URL")</span></span>

4. <span data-ttu-id="0f9b7-142">On the **Configure single sign-on at Thirdlight** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-142">On the **Configure single sign-on at Thirdlight** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    <span data-ttu-id="0f9b7-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805842.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805842.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="0f9b7-144">In a different web browser window, log into your Thirdlight company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-144">In a different web browser window, log into your Thirdlight company site as an administrator.</span></span>

6. <span data-ttu-id="0f9b7-145">Go to **Configuration \> System Administration**, and then click **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-145">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="0f9b7-146">![System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805843.png "System Administration")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-146">![System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805843.png "System Administration")</span></span>

7. <span data-ttu-id="0f9b7-147">In the SAML2 configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0f9b7-147">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="0f9b7-148">![SAML Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805844.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-148">![SAML Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805844.png "SAML Single Sign-On")</span></span>   
 1. <span data-ttu-id="0f9b7-149">Select **Enable SAML2 Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-149">Select **Enable SAML2 Single Sign-On**.</span></span> 
 2. <span data-ttu-id="0f9b7-150">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-150">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span> 
 3. <span data-ttu-id="0f9b7-151">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-151">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
 4. <span data-ttu-id="0f9b7-152">Click **Save SAML2 settings**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-152">Click **Save SAML2 settings**.</span></span>

8. <span data-ttu-id="0f9b7-153">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-153">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="0f9b7-154">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805845.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-154">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805845.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="0f9b7-155">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="0f9b7-155">Configure user provisioning</span></span>
<span data-ttu-id="0f9b7-156">In order to enable Azure AD users to log into Thirdlight, they must be provisioned into Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-156">In order to enable Azure AD users to log into Thirdlight, they must be provisioned into Thirdlight.</span></span>  

* <span data-ttu-id="0f9b7-157">In the case of Thirdlight, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-157">In the case of Thirdlight, provisioning is a manual task.</span></span>

<span data-ttu-id="0f9b7-158">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0f9b7-158">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0f9b7-159">Log in to your **Thirdlight** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-159">Log in to your **Thirdlight** company site as an administrator.</span></span>

2. <span data-ttu-id="0f9b7-160">Go to **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-160">Go to **Users** tab.</span></span>

3. <span data-ttu-id="0f9b7-161">Select **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-161">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="0f9b7-162">Click **Add new User** button.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-162">Click **Add new User** button.</span></span>

5. <span data-ttu-id="0f9b7-163">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-163">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="0f9b7-164">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-164">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="0f9b7-165">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-165">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="0f9b7-166">Assign users</span><span class="sxs-lookup"><span data-stu-id="0f9b7-166">Assign users</span></span>
<span data-ttu-id="0f9b7-167">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-167">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="0f9b7-168">**To assign users to Thirdlight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0f9b7-168">**To assign users to Thirdlight, perform the following steps:**</span></span>

1. <span data-ttu-id="0f9b7-169">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-169">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="0f9b7-170">On the \*\*Thirdlight \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-170">On the \*\*Thirdlight \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="0f9b7-171">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805846.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-171">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC805846.png "Assign Users")</span></span>

3. <span data-ttu-id="0f9b7-172">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-172">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="0f9b7-173">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="0f9b7-173">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-thirdlight-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="0f9b7-174">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0f9b7-174">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="0f9b7-175">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0f9b7-175">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















