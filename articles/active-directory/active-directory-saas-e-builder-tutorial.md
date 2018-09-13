---
title: 'Tutorial: Azure Active Directory integration with e-Builder | Microsoft Docs'
description: Learn how to use e-Builder with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: d5068007-5a54-40ac-9cb8-2ceca89fd8ab
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9d8d739a4d5e4cf62502e2e9c05857f13a6fa2e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550755"
---
# <a name="tutorial-azure-active-directory-integration-with-e-builder"></a><span data-ttu-id="2b7cb-103">Tutorial: Azure Active Directory integration with e-Builder</span><span class="sxs-lookup"><span data-stu-id="2b7cb-103">Tutorial: Azure Active Directory integration with e-Builder</span></span>
<span data-ttu-id="2b7cb-104">The objective of this tutorial is to show the integration of Azure and e-Builder.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-104">The objective of this tutorial is to show the integration of Azure and e-Builder.</span></span>  

<span data-ttu-id="2b7cb-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="2b7cb-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2b7cb-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="2b7cb-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2b7cb-107">An e-Builder tenant</span><span class="sxs-lookup"><span data-stu-id="2b7cb-107">An e-Builder tenant</span></span>

<span data-ttu-id="2b7cb-108">After completing this tutorial, the Azure AD users you have assigned to e-Builder will be able to single sign into the application at your e-Builder company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b7cb-108">After completing this tutorial, the Azure AD users you have assigned to e-Builder will be able to single sign into the application at your e-Builder company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="2b7cb-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2b7cb-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="2b7cb-110">Enabling the application integration for e-Builder</span><span class="sxs-lookup"><span data-stu-id="2b7cb-110">Enabling the application integration for e-Builder</span></span>
* <span data-ttu-id="2b7cb-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="2b7cb-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="2b7cb-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="2b7cb-112">Configuring user provisioning</span></span>
* <span data-ttu-id="2b7cb-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="2b7cb-113">Assigning users</span></span>

<span data-ttu-id="2b7cb-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777378.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777378.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-e-builder"></a><span data-ttu-id="2b7cb-115">Enable the application integration for e-Builder</span><span class="sxs-lookup"><span data-stu-id="2b7cb-115">Enable the application integration for e-Builder</span></span>
<span data-ttu-id="2b7cb-116">The objective of this section is to outline how to enable the application integration for e-Builder.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-116">The objective of this section is to outline how to enable the application integration for e-Builder.</span></span>

<span data-ttu-id="2b7cb-117">**To enable the application integration for e-Builder, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b7cb-117">**To enable the application integration for e-Builder, perform the following steps:**</span></span>

1. <span data-ttu-id="2b7cb-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="2b7cb-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2b7cb-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2b7cb-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2b7cb-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2b7cb-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="2b7cb-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2b7cb-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="2b7cb-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2b7cb-127">In the **search box**, type **e-Builder**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-127">In the **search box**, type **e-Builder**.</span></span>
   
   <span data-ttu-id="2b7cb-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777379.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777379.png "Application gallery")</span></span>
7. <span data-ttu-id="2b7cb-129">In the results pane, select **e-Builder**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-129">In the results pane, select **e-Builder**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2b7cb-130">![e-Builder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777380.png "e-Builder")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-130">![e-Builder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777380.png "e-Builder")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2b7cb-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b7cb-131">Configure single sign-on</span></span>

<span data-ttu-id="2b7cb-132">The objective of this section is to outline how to enable users to authenticate to e-Builder with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-132">The objective of this section is to outline how to enable users to authenticate to e-Builder with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="2b7cb-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b7cb-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2b7cb-134">In the Azure classic portal, on the **e-Builder** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-134">In the Azure classic portal, on the **e-Builder** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="2b7cb-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777381.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777381.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="2b7cb-136">On the **How would you like users to sign on to e-Builder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-136">On the **How would you like users to sign on to e-Builder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2b7cb-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777382.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777382.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="2b7cb-138">On the **Configure App URL** page, in the **e-Builder Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.e-Builder.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-138">On the **Configure App URL** page, in the **e-Builder Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.e-Builder.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="2b7cb-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777383.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777383.png "Configure app URL")</span></span>
4. <span data-ttu-id="2b7cb-140">On the **Configure single sign-on at e-Builder** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\e-BuilderMetaData.xml**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-140">On the **Configure single sign-on at e-Builder** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\e-BuilderMetaData.xml**.</span></span>
   
   <span data-ttu-id="2b7cb-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777384.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777384.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="2b7cb-142">Forward that metadata file to e-Builder support team.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-142">Forward that metadata file to e-Builder support team.</span></span> <span data-ttu-id="2b7cb-143">The support team needs configures single sign-on for you.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-143">The support team needs configures single sign-on for you.</span></span>
6. <span data-ttu-id="2b7cb-144">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-144">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="2b7cb-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777385.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777385.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="2b7cb-146">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="2b7cb-146">Configure user provisioning</span></span>

<span data-ttu-id="2b7cb-147">There is no action item for you to configure user provisioning to e-Builder.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-147">There is no action item for you to configure user provisioning to e-Builder.</span></span>  
<span data-ttu-id="2b7cb-148">When an assigned user tries to log into e-Builder using the access panel, e-Builder checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-148">When an assigned user tries to log into e-Builder using the access panel, e-Builder checks whether the user exists.</span></span>  

* <span data-ttu-id="2b7cb-149">If there is no user account available yet, it is automatically created by e-Builder.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-149">If there is no user account available yet, it is automatically created by e-Builder.</span></span>

## <a name="assign-users"></a><span data-ttu-id="2b7cb-150">Assign users</span><span class="sxs-lookup"><span data-stu-id="2b7cb-150">Assign users</span></span>
<span data-ttu-id="2b7cb-151">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-151">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2b7cb-152">**To assign users to e-Builder, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b7cb-152">**To assign users to e-Builder, perform the following steps:**</span></span>

1. <span data-ttu-id="2b7cb-153">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-153">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2b7cb-154">On the \*\*e-Builder \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-154">On the \*\*e-Builder \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2b7cb-155">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777386.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-155">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC777386.png "Assign users")</span></span>
3. <span data-ttu-id="2b7cb-156">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-156">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2b7cb-157">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="2b7cb-157">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-e-builder-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2b7cb-158">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2b7cb-158">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2b7cb-159">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b7cb-159">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















