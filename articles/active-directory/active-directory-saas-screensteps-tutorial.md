---
title: 'Tutorial: Azure Active Directory integration with ScreenSteps | Microsoft Docs'
description: Learn how to use ScreenSteps with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 6be961649ee11adf0f383cf473bb696cd85bb77d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554521"
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="8144b-103">Tutorial: Azure Active Directory integration with ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="8144b-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>
<span data-ttu-id="8144b-104">The objective of this tutorial is to show the integration of Azure and ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="8144b-104">The objective of this tutorial is to show the integration of Azure and ScreenSteps.</span></span>
<span data-ttu-id="8144b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="8144b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="8144b-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="8144b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8144b-107">A ScreenSteps tenant</span><span class="sxs-lookup"><span data-stu-id="8144b-107">A ScreenSteps tenant</span></span>

<span data-ttu-id="8144b-108">After completing this tutorial, the Azure AD users you have assigned to ScreenSteps will be able to sign into the application using single sign-on (SSO) at your ScreenSteps company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8144b-108">After completing this tutorial, the Azure AD users you have assigned to ScreenSteps will be able to sign into the application using single sign-on (SSO) at your ScreenSteps company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8144b-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8144b-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="8144b-110">Enabling the application integration for ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="8144b-110">Enabling the application integration for ScreenSteps</span></span>
2. <span data-ttu-id="8144b-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="8144b-111">Configuring single sign-on (SSO)</span></span> 
3. <span data-ttu-id="8144b-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="8144b-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8144b-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="8144b-113">Assigning users</span></span>

<span data-ttu-id="8144b-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778516.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="8144b-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778516.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-screensteps"></a><span data-ttu-id="8144b-115">Enable the application integration for ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="8144b-115">Enable the application integration for ScreenSteps</span></span>
<span data-ttu-id="8144b-116">The objective of this section is to outline how to enable the application integration for ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="8144b-116">The objective of this section is to outline how to enable the application integration for ScreenSteps.</span></span>

<span data-ttu-id="8144b-117">**To enable the application integration for ScreenSteps, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8144b-117">**To enable the application integration for ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="8144b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8144b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>

    <span data-ttu-id="8144b-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8144b-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8144b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8144b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8144b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8144b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    <span data-ttu-id="8144b-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="8144b-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8144b-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8144b-123">Click **Add** at the bottom of the page.</span></span>

    <span data-ttu-id="8144b-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="8144b-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8144b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8144b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    <span data-ttu-id="8144b-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="8144b-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8144b-127">In the **search box**, type **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="8144b-127">In the **search box**, type **ScreenSteps**.</span></span>

    <span data-ttu-id="8144b-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778517.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="8144b-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778517.png "Application gallery")</span></span>
7. <span data-ttu-id="8144b-129">In the results pane, select **ScreenSteps**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8144b-129">In the results pane, select **ScreenSteps**, and then click **Complete** to add the application.</span></span>

    <span data-ttu-id="8144b-130">![ScreenSteps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778518.png "ScreenSteps")</span><span class="sxs-lookup"><span data-stu-id="8144b-130">![ScreenSteps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778518.png "ScreenSteps")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8144b-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="8144b-131">Configure single sign-on</span></span>
<span data-ttu-id="8144b-132">The objective of this section is to outline how to enable users to authenticate to ScreenSteps with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="8144b-132">The objective of this section is to outline how to enable users to authenticate to ScreenSteps with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="8144b-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8144b-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="8144b-134">In the Azure classic portal, on the **ScreenSteps** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="8144b-134">In the Azure classic portal, on the **ScreenSteps** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>

    <span data-ttu-id="8144b-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778519.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8144b-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778519.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="8144b-136">On the **How would you like users to sign on to ScreenSteps** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8144b-136">On the **How would you like users to sign on to ScreenSteps** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>

    <span data-ttu-id="8144b-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778520.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8144b-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778520.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="8144b-138">In a different web browser window, log into your ScreenSteps company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8144b-138">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

4. <span data-ttu-id="8144b-139">Click **Account Management**.</span><span class="sxs-lookup"><span data-stu-id="8144b-139">Click **Account Management**.</span></span>

    <span data-ttu-id="8144b-140">![Account management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778523.png "Account management")</span><span class="sxs-lookup"><span data-stu-id="8144b-140">![Account management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778523.png "Account management")</span></span>

5. <span data-ttu-id="8144b-141">Click **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8144b-141">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="8144b-142">![Remote authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778524.png "Remote authentication")</span><span class="sxs-lookup"><span data-stu-id="8144b-142">![Remote authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778524.png "Remote authentication")</span></span>

6. <span data-ttu-id="8144b-143">Click **Create Single Sign-on Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8144b-143">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="8144b-144">![Remote authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778525.png "Remote authentication")</span><span class="sxs-lookup"><span data-stu-id="8144b-144">![Remote authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778525.png "Remote authentication")</span></span>

7. <span data-ttu-id="8144b-145">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8144b-145">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="8144b-146">![Create an authentication endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778526.png "Create an authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="8144b-146">![Create an authentication endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778526.png "Create an authentication endpoint")</span></span>

    1. <span data-ttu-id="8144b-147">In the **Title** textbox, type a title.</span><span class="sxs-lookup"><span data-stu-id="8144b-147">In the **Title** textbox, type a title.</span></span>
    2. <span data-ttu-id="8144b-148">From the **Mode** list, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8144b-148">From the **Mode** list, select **SAML**.</span></span>
    3. <span data-ttu-id="8144b-149">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8144b-149">Click **Create**.</span></span>

8. <span data-ttu-id="8144b-150">Edit the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="8144b-150">Edit the new endpoint.</span></span>

    <span data-ttu-id="8144b-151">![Edit endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778528.png "Edit endpoint")</span><span class="sxs-lookup"><span data-stu-id="8144b-151">![Edit endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778528.png "Edit endpoint")</span></span>

9. <span data-ttu-id="8144b-152">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8144b-152">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="8144b-153">![Remote authentication endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778527.png "Remote authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="8144b-153">![Remote authentication endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778527.png "Remote authentication endpoint")</span></span>

    1. <span data-ttu-id="8144b-154">Copy the **SAML Consumer URL** to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="8144b-154">Copy the **SAML Consumer URL** to the clipboard.</span></span>

10. <span data-ttu-id="8144b-155">On the **Configure App URL** page of the Azure classic portal, in the **ScreenSteps Sign In URL** textbox, paste the **SAML Consumer URL**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8144b-155">On the **Configure App URL** page of the Azure classic portal, in the **ScreenSteps Sign In URL** textbox, paste the **SAML Consumer URL**, and then click **Next**.</span></span>

    <span data-ttu-id="8144b-156">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778521.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="8144b-156">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778521.png "Configure app URL")</span></span>

11. <span data-ttu-id="8144b-157">On the **Configure single sign-on at ScreenSteps** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8144b-157">On the **Configure single sign-on at ScreenSteps** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="8144b-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778522.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8144b-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778522.png "Configure single sign-on")</span></span>


12. <span data-ttu-id="8144b-159">Return to the **Edit Single Sign-on Endpoint** section and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8144b-159">Return to the **Edit Single Sign-on Endpoint** section and perform the following steps:</span></span>

    <span data-ttu-id="8144b-160">![Remote authentication endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778527.png "Remote authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="8144b-160">![Remote authentication endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778527.png "Remote authentication endpoint")</span></span>

    1. <span data-ttu-id="8144b-161">Click **Upload new SAML Certificate file**, and then upload the downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="8144b-161">Click **Upload new SAML Certificate file**, and then upload the downloaded certificate.</span></span>
    2. <span data-ttu-id="8144b-162">In the Azure classic portal, on the **Configure single sign-on at ScreenSteps** page, copy the **Remote Login URL** value, and then paste it into the **Remote Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8144b-162">In the Azure classic portal, on the **Configure single sign-on at ScreenSteps** page, copy the **Remote Login URL** value, and then paste it into the **Remote Login URL** textbox.</span></span>
    3. <span data-ttu-id="8144b-163">In the Azure classic portal, on the **Configure single sign-on at ScreenSteps** page, copy the **Remote Logout URL** value, and then paste it into the **Log out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8144b-163">In the Azure classic portal, on the **Configure single sign-on at ScreenSteps** page, copy the **Remote Logout URL** value, and then paste it into the **Log out URL** textbox.</span></span>
    4. <span data-ttu-id="8144b-164">Select a **Group** to assign users to when they are provisioned.</span><span class="sxs-lookup"><span data-stu-id="8144b-164">Select a **Group** to assign users to when they are provisioned.</span></span>
    5. <span data-ttu-id="8144b-165">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="8144b-165">Click **Update**.</span></span>
    6. <span data-ttu-id="8144b-166">Return to the **Edit Single Sign-on Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8144b-166">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    7. <span data-ttu-id="8144b-167">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="8144b-167">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="8144b-168">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="8144b-168">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>


12. <span data-ttu-id="8144b-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="8144b-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>

    <span data-ttu-id="8144b-170">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778542.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8144b-170">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778542.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="8144b-171">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="8144b-171">Configuring user provisioning</span></span>



## <a name="assign-users"></a><span data-ttu-id="8144b-172">Assign users</span><span class="sxs-lookup"><span data-stu-id="8144b-172">Assign users</span></span>
<span data-ttu-id="8144b-173">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="8144b-173">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="8144b-174">**To assign users to ScreenSteps, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8144b-174">**To assign users to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="8144b-175">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="8144b-175">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8144b-176">On the **ScreenSteps** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="8144b-176">On the **ScreenSteps** application integration page, click **Assign users**.</span></span>

    <span data-ttu-id="8144b-177">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778548.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="8144b-177">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-screensteps-tutorial/IC778548.png "Assign users")</span></span>
3. <span data-ttu-id="8144b-178">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="8144b-178">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>


<span data-ttu-id="8144b-179">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8144b-179">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="8144b-180">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8144b-180">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















