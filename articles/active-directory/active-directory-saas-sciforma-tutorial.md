---
title: 'Tutorial: Azure Active Directory integration with Sciforma | Microsoft Docs'
description: Learn how to use Sciforma with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 010ec3b21cb1375eeb717f812248eff84b2e8cd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549381"
---
# <a name="tutorial-azure-ad-integration-with-sciforma"></a><span data-ttu-id="9dbc8-103">Tutorial: Azure AD integration with Sciforma</span><span class="sxs-lookup"><span data-stu-id="9dbc8-103">Tutorial: Azure AD integration with Sciforma</span></span>
<span data-ttu-id="9dbc8-104">The objective of this tutorial is to show the integration of Azure and Sciforma.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-104">The objective of this tutorial is to show the integration of Azure and Sciforma.</span></span>  

<span data-ttu-id="9dbc8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="9dbc8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="9dbc8-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="9dbc8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="9dbc8-107">A Sciforma tenant</span><span class="sxs-lookup"><span data-stu-id="9dbc8-107">A Sciforma tenant</span></span>

<span data-ttu-id="9dbc8-108">After completing this tutorial, the Azure AD users you have assigned to Sciforma will be able to single sign into the application at your Sciforma company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9dbc8-108">After completing this tutorial, the Azure AD users you have assigned to Sciforma will be able to single sign into the application at your Sciforma company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="9dbc8-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9dbc8-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="9dbc8-110">Enabling the application integration for Sciforma</span><span class="sxs-lookup"><span data-stu-id="9dbc8-110">Enabling the application integration for Sciforma</span></span>
2. <span data-ttu-id="9dbc8-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="9dbc8-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="9dbc8-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="9dbc8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="9dbc8-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="9dbc8-113">Assigning users</span></span>

<span data-ttu-id="9dbc8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777369.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777369.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-sciforma"></a><span data-ttu-id="9dbc8-115">Enable the application integration for Sciforma</span><span class="sxs-lookup"><span data-stu-id="9dbc8-115">Enable the application integration for Sciforma</span></span>
<span data-ttu-id="9dbc8-116">The objective of this section is to outline how to enable the application integration for Sciforma.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-116">The objective of this section is to outline how to enable the application integration for Sciforma.</span></span>

<span data-ttu-id="9dbc8-117">**To enable the application integration for Sciforma, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dbc8-117">**To enable the application integration for Sciforma, perform the following steps:**</span></span>

1. <span data-ttu-id="9dbc8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="9dbc8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="9dbc8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="9dbc8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="9dbc8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="9dbc8-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="9dbc8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="9dbc8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="9dbc8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="9dbc8-127">In the **search box**, type **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-127">In the **search box**, type **Sciforma**.</span></span>
   
    <span data-ttu-id="9dbc8-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777370.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777370.png "Application gallery")</span></span>

7. <span data-ttu-id="9dbc8-129">In the results pane, select **Sciforma**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-129">In the results pane, select **Sciforma**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="9dbc8-130">![Sciforma](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777371.png "Sciforma")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-130">![Sciforma](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777371.png "Sciforma")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="9dbc8-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="9dbc8-131">Configure single sign-on</span></span>

<span data-ttu-id="9dbc8-132">The objective of this section is to outline how to enable users to authenticate to Sciforma with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-132">The objective of this section is to outline how to enable users to authenticate to Sciforma with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="9dbc8-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dbc8-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="9dbc8-134">In the Azure classic portal, on the **Sciforma** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-134">In the Azure classic portal, on the **Sciforma** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="9dbc8-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777372.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777372.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="9dbc8-136">On the **How would you like users to sign on to Sciforma** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-136">On the **How would you like users to sign on to Sciforma** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="9dbc8-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777373.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777373.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="9dbc8-138">On the **Configure App URL** page, in the **Sciforma Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Sciforma.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-138">On the **Configure App URL** page, in the **Sciforma Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Sciforma.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="9dbc8-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777374.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777374.png "Configure app URL")</span></span>

4. <span data-ttu-id="9dbc8-140">On the **Configure single sign-on at Sciforma** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\SciformaMetaData.xml**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-140">On the **Configure single sign-on at Sciforma** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\SciformaMetaData.xml**.</span></span>
   
    <span data-ttu-id="9dbc8-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777375.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777375.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="9dbc8-142">Forward that metadata file to Sciforma support team.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-142">Forward that metadata file to Sciforma support team.</span></span> <span data-ttu-id="9dbc8-143">The support team configures single sign-on for you.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-143">The support team configures single sign-on for you.</span></span>

6. <span data-ttu-id="9dbc8-144">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-144">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="9dbc8-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777376.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777376.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="9dbc8-146">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="9dbc8-146">Configure user provisioning</span></span>

<span data-ttu-id="9dbc8-147">There is no action item for you to configure user provisioning to Sciforma.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-147">There is no action item for you to configure user provisioning to Sciforma.</span></span> <span data-ttu-id="9dbc8-148">When an assigned user tries to log into Sciforma using the access panel, Sciforma checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-148">When an assigned user tries to log into Sciforma using the access panel, Sciforma checks whether the user exists.</span></span>  

* <span data-ttu-id="9dbc8-149">If there is no user account available yet, it is automatically created by Sciforma.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-149">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

## <a name="assign-users"></a><span data-ttu-id="9dbc8-150">Assign users</span><span class="sxs-lookup"><span data-stu-id="9dbc8-150">Assign users</span></span>
<span data-ttu-id="9dbc8-151">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-151">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="9dbc8-152">**To assign users to Sciforma, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dbc8-152">**To assign users to Sciforma, perform the following steps:**</span></span>

1. <span data-ttu-id="9dbc8-153">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-153">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="9dbc8-154">On the \*\*Sciforma \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-154">On the \*\*Sciforma \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="9dbc8-155">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777377.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-155">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC777377.png "Assign users")</span></span>
3. <span data-ttu-id="9dbc8-156">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-156">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="9dbc8-157">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="9dbc8-157">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sciforma-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="9dbc8-158">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9dbc8-158">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="9dbc8-159">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9dbc8-159">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















