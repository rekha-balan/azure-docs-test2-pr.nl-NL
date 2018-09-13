---
title: 'Tutorial: Azure Active Directory integration with Lucidchart | Microsoft Docs'
description: Learn how to use Lucidchart with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: ea18349815de19a24a0a8c775111762d66849d57
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662179"
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="6c420-103">Tutorial: Azure Active Directory integration with Lucidchart</span><span class="sxs-lookup"><span data-stu-id="6c420-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>
<span data-ttu-id="6c420-104">The objective of this tutorial is to show the integration of Azure and Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c420-104">The objective of this tutorial is to show the integration of Azure and Lucidchart.</span></span>  

<span data-ttu-id="6c420-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6c420-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6c420-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="6c420-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6c420-107">A Lucidchart single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6c420-107">A Lucidchart single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="6c420-108">After completing this tutorial, the Azure AD users you have assigned to Lucidchart will be able to single sign into the application at your Lucidchart company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c420-108">After completing this tutorial, the Azure AD users you have assigned to Lucidchart will be able to single sign into the application at your Lucidchart company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6c420-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c420-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="6c420-110">Enabling the application integration for Lucidchart</span><span class="sxs-lookup"><span data-stu-id="6c420-110">Enabling the application integration for Lucidchart</span></span>
2. <span data-ttu-id="6c420-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c420-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="6c420-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6c420-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="6c420-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6c420-113">Assigning users</span></span>

<span data-ttu-id="6c420-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791183.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="6c420-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791183.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-lucidchart"></a><span data-ttu-id="6c420-115">Enabling the application integration for Lucidchart</span><span class="sxs-lookup"><span data-stu-id="6c420-115">Enabling the application integration for Lucidchart</span></span>
<span data-ttu-id="6c420-116">The objective of this section is to outline how to enable the application integration for Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c420-116">The objective of this section is to outline how to enable the application integration for Lucidchart.</span></span>

<span data-ttu-id="6c420-117">**To enable the application integration for Lucidchart, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c420-117">**To enable the application integration for Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="6c420-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c420-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6c420-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6c420-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6c420-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6c420-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6c420-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6c420-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="6c420-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6c420-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6c420-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6c420-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="6c420-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="6c420-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6c420-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6c420-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="6c420-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="6c420-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6c420-127">In the **search box**, type **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="6c420-127">In the **search box**, type **Lucidchart**.</span></span>
   
   <span data-ttu-id="6c420-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791184.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="6c420-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791184.png "Application Gallery")</span></span>
7. <span data-ttu-id="6c420-129">In the results pane, select **Lucidchart**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6c420-129">In the results pane, select **Lucidchart**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="6c420-130">![Lucidchart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791185.png "Lucidchart")</span><span class="sxs-lookup"><span data-stu-id="6c420-130">![Lucidchart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791185.png "Lucidchart")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="6c420-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c420-131">Configuring single sign-on</span></span>

<span data-ttu-id="6c420-132">The objective of this section is to outline how to enable users to authenticate to Lucidchart with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="6c420-132">The objective of this section is to outline how to enable users to authenticate to Lucidchart with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="6c420-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c420-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="6c420-134">In the Azure classic portal, on the **Lucidchart** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c420-134">In the Azure classic portal, on the **Lucidchart** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="6c420-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791186.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6c420-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791186.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="6c420-136">On the **How would you like users to sign on to Lucidchart** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c420-136">On the **How would you like users to sign on to Lucidchart** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6c420-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791187.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6c420-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791187.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="6c420-138">On the **Configure App URL** page, in the **Lucidchart Sign On URL** textbox, type the URL used by your users to sign on to your Lucidchart application (e.g.: "*https://chart2.office.lucidchart.com/saml/sso/azure*"), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c420-138">On the **Configure App URL** page, in the **Lucidchart Sign On URL** textbox, type the URL used by your users to sign on to your Lucidchart application (e.g.: "*https://chart2.office.lucidchart.com/saml/sso/azure*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="6c420-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791188.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="6c420-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791188.png "Configure App URL")</span></span>
4. <span data-ttu-id="6c420-140">On the **Configure single sign-on at Lucidchart** page, to download your metadata, click **Download metadata**, and then save the data file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="6c420-140">On the **Configure single sign-on at Lucidchart** page, to download your metadata, click **Download metadata**, and then save the data file locally on your computer.</span></span>
   
   <span data-ttu-id="6c420-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791189.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6c420-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791189.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="6c420-142">In a different web browser window, log into your Lucidchart company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6c420-142">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>
6. <span data-ttu-id="6c420-143">In the menu on the top, click **Team**.</span><span class="sxs-lookup"><span data-stu-id="6c420-143">In the menu on the top, click **Team**.</span></span>
   
   <span data-ttu-id="6c420-144">![Team](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791190.png "Team")</span><span class="sxs-lookup"><span data-stu-id="6c420-144">![Team](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791190.png "Team")</span></span>
7. <span data-ttu-id="6c420-145">Click **Application \> Manage SAML**.</span><span class="sxs-lookup"><span data-stu-id="6c420-145">Click **Application \> Manage SAML**.</span></span>
   
   <span data-ttu-id="6c420-146">![Manage SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791191.png "Manage SAML")</span><span class="sxs-lookup"><span data-stu-id="6c420-146">![Manage SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791191.png "Manage SAML")</span></span>
8. <span data-ttu-id="6c420-147">On the **SAML Authentication Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c420-147">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
   1. <span data-ttu-id="6c420-148">Select **Enable SAML Authentication**, and then click **Optional**.</span><span class="sxs-lookup"><span data-stu-id="6c420-148">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

  <span data-ttu-id="6c420-149">![SAML Authentication Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791192.png "SAML Authentication Settings")</span><span class="sxs-lookup"><span data-stu-id="6c420-149">![SAML Authentication Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791192.png "SAML Authentication Settings")</span></span>
   2. <span data-ttu-id="6c420-150">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span><span class="sxs-lookup"><span data-stu-id="6c420-150">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

  <span data-ttu-id="6c420-151">![Change Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791193.png "Change Certificate")</span><span class="sxs-lookup"><span data-stu-id="6c420-151">![Change Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791193.png "Change Certificate")</span></span>
   3. <span data-ttu-id="6c420-152">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="6c420-152">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

  <span data-ttu-id="6c420-153">![Upload Metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791194.png "Upload Metadata")</span><span class="sxs-lookup"><span data-stu-id="6c420-153">![Upload Metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791194.png "Upload Metadata")</span></span>
   4. <span data-ttu-id="6c420-154">Select **Automatically Add new user to the team**, and then click **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="6c420-154">Select **Automatically Add new user to the team**, and then click **Save changes**.</span></span>

  <span data-ttu-id="6c420-155">![Save Changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791195.png "Save Changes")</span><span class="sxs-lookup"><span data-stu-id="6c420-155">![Save Changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791195.png "Save Changes")</span></span>
9. <span data-ttu-id="6c420-156">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c420-156">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
  <span data-ttu-id="6c420-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791196.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6c420-157">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791196.png "Configure Single Sign-On")</span></span>
   
## <a name="configuring-user-provisioning"></a><span data-ttu-id="6c420-158">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6c420-158">Configuring user provisioning</span></span>

<span data-ttu-id="6c420-159">There is no action item for you to configure user provisioning to Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c420-159">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="6c420-160">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="6c420-160">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="6c420-161">If there is no user account available yet, it is automatically created by Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c420-161">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

## <a name="assigning-users"></a><span data-ttu-id="6c420-162">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6c420-162">Assigning users</span></span>
<span data-ttu-id="6c420-163">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="6c420-163">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="6c420-164">**To assign users to Lucidchart, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c420-164">**To assign users to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="6c420-165">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="6c420-165">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6c420-166">On the **Lucidchart** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="6c420-166">On the **Lucidchart** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6c420-167">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791197.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="6c420-167">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC791197.png "Assign Users")</span></span>
3. <span data-ttu-id="6c420-168">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="6c420-168">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="6c420-169">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="6c420-169">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lucidchart-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6c420-170">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6c420-170">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="6c420-171">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c420-171">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















