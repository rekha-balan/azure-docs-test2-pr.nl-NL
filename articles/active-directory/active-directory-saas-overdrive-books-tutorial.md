---
title: 'Tutorial: Azure Active Directory integration with Overdrive Books | Microsoft Docs'
description: Learn how to use Overdrive Books with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: c04654604281a88b016a8f5fdc69e052b054e12a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550289"
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive-books"></a><span data-ttu-id="d33b8-103">Tutorial: Azure Active Directory integration with Overdrive Books</span><span class="sxs-lookup"><span data-stu-id="d33b8-103">Tutorial: Azure Active Directory integration with Overdrive Books</span></span>
<span data-ttu-id="d33b8-104">The objective of this tutorial is to show the integration of Azure and OverDrive.</span><span class="sxs-lookup"><span data-stu-id="d33b8-104">The objective of this tutorial is to show the integration of Azure and OverDrive.</span></span>  

<span data-ttu-id="d33b8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="d33b8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d33b8-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d33b8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d33b8-107">An OverDrive single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d33b8-107">An OverDrive single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="d33b8-108">After completing this tutorial, the Azure AD users you have assigned to OverDrive will be able to single sign-on (SSO) to the application at your OverDrive company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d33b8-108">After completing this tutorial, the Azure AD users you have assigned to OverDrive will be able to single sign-on (SSO) to the application at your OverDrive company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d33b8-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d33b8-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d33b8-110">Enabling the application integration for OverDrive</span><span class="sxs-lookup"><span data-stu-id="d33b8-110">Enabling the application integration for OverDrive</span></span>
2. <span data-ttu-id="d33b8-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="d33b8-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d33b8-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="d33b8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d33b8-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="d33b8-113">Assigning users</span></span>

<span data-ttu-id="d33b8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784462.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="d33b8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784462.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-overdrive"></a><span data-ttu-id="d33b8-115">Enable the application integration for OverDrive</span><span class="sxs-lookup"><span data-stu-id="d33b8-115">Enable the application integration for OverDrive</span></span>
<span data-ttu-id="d33b8-116">The objective of this section is to outline how to enable the application integration for OverDrive.</span><span class="sxs-lookup"><span data-stu-id="d33b8-116">The objective of this section is to outline how to enable the application integration for OverDrive.</span></span>

<span data-ttu-id="d33b8-117">**To enable the application integration for OverDrive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d33b8-117">**To enable the application integration for OverDrive, perform the following steps:**</span></span>

1. <span data-ttu-id="d33b8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d33b8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d33b8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d33b8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d33b8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d33b8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d33b8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d33b8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="d33b8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="d33b8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d33b8-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d33b8-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="d33b8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="d33b8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d33b8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d33b8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="d33b8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="d33b8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d33b8-127">In the **search box**, type **OverDrive**.</span><span class="sxs-lookup"><span data-stu-id="d33b8-127">In the **search box**, type **OverDrive**.</span></span>
   
   <span data-ttu-id="d33b8-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784463.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="d33b8-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784463.png "Application Gallery")</span></span>
7. <span data-ttu-id="d33b8-129">In the results pane, select **OverDrive**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d33b8-129">In the results pane, select **OverDrive**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="d33b8-130">![OverDrive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC799950.png "OverDrive")</span><span class="sxs-lookup"><span data-stu-id="d33b8-130">![OverDrive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC799950.png "OverDrive")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d33b8-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="d33b8-131">Configure single sign-on</span></span>

<span data-ttu-id="d33b8-132">The objective of this section is to outline how to enable users to authenticate to OverDrive with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="d33b8-132">The objective of this section is to outline how to enable users to authenticate to OverDrive with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="d33b8-133">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d33b8-133">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="d33b8-134">In the Azure classic portal, on the **OverDrive** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="d33b8-134">In the Azure classic portal, on the **OverDrive** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="d33b8-135">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784465.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d33b8-135">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784465.png "Enable single sign-on")</span></span>
2. <span data-ttu-id="d33b8-136">On the **How would you like users to sign on to OverDrive** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d33b8-136">On the **How would you like users to sign on to OverDrive** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d33b8-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784466.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d33b8-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784466.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="d33b8-138">On the **Configure App URL** page, in the **OverDrive Sign In URL** textbox, type your URL using the following pattern "*http://mslibrarytest.libraryreserve.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d33b8-138">On the **Configure App URL** page, in the **OverDrive Sign In URL** textbox, type your URL using the following pattern "*http://mslibrarytest.libraryreserve.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="d33b8-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784467.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="d33b8-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784467.png "Configure App URL")</span></span>
4. <span data-ttu-id="d33b8-140">On the **Configure single sign-on at OverDrive** page, to download the metadata file, and then send it to the OverDrive support team.</span><span class="sxs-lookup"><span data-stu-id="d33b8-140">On the **Configure single sign-on at OverDrive** page, to download the metadata file, and then send it to the OverDrive support team.</span></span>
   
   <span data-ttu-id="d33b8-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784468.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d33b8-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784468.png "Configure single sign-on")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d33b8-142">The OverDrive support team configures single sign-on for you and sends you a notification when the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="d33b8-142">The OverDrive support team configures single sign-on for you and sends you a notification when the configuration has been completed.</span></span>
   > 
   > 
5. <span data-ttu-id="d33b8-143">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="d33b8-143">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d33b8-144">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784469.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d33b8-144">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784469.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="d33b8-145">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="d33b8-145">Configure user provisioning</span></span>

<span data-ttu-id="d33b8-146">There is no action item for you to configure user provisioning to OverDrive.</span><span class="sxs-lookup"><span data-stu-id="d33b8-146">There is no action item for you to configure user provisioning to OverDrive.</span></span>  

<span data-ttu-id="d33b8-147">When an assigned user tries to log into OverDrive, an OverDrive account is automatically created if necessary.</span><span class="sxs-lookup"><span data-stu-id="d33b8-147">When an assigned user tries to log into OverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="d33b8-148">You can use any other OverDrive user account creation tools or APIs provided by OverDrive to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="d33b8-148">You can use any other OverDrive user account creation tools or APIs provided by OverDrive to provision AAD user accounts.</span></span>
>
>
 
## <a name="assign-users"></a><span data-ttu-id="d33b8-149">Assign users</span><span class="sxs-lookup"><span data-stu-id="d33b8-149">Assign users</span></span>
<span data-ttu-id="d33b8-150">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="d33b8-150">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="d33b8-151">**To assign users to OverDrive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d33b8-151">**To assign users to OverDrive, perform the following steps:**</span></span>

1. <span data-ttu-id="d33b8-152">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="d33b8-152">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d33b8-153">On the **OverDrive** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="d33b8-153">On the **OverDrive** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d33b8-154">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784470.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="d33b8-154">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC784470.png "Assign Users")</span></span>
   
3. <span data-ttu-id="d33b8-155">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="d33b8-155">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="d33b8-156">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="d33b8-156">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-overdrive-books-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d33b8-157">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d33b8-157">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="d33b8-158">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d33b8-158">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d33b8-159">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d33b8-159">Additional resources</span></span>

* [<span data-ttu-id="d33b8-160">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d33b8-160">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d33b8-161">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d33b8-161">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)














