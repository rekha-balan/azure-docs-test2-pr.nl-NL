---
title: 'Tutorial: Azure Active Directory integration with RightAnswers | Microsoft Docs'
description: Learn how to use RightAnswers with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 15f59603fee13dff86c470f04d8ea9aaa1f169b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540811"
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="b5c95-103">Tutorial: Azure Active Directory integration with RightAnswers</span><span class="sxs-lookup"><span data-stu-id="b5c95-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>
<span data-ttu-id="b5c95-104">The objective of this tutorial is to show the integration of Azure and RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="b5c95-104">The objective of this tutorial is to show the integration of Azure and RightAnswers.</span></span> <span data-ttu-id="b5c95-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="b5c95-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b5c95-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b5c95-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b5c95-107">A RightAnswers single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b5c95-107">A RightAnswers single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="b5c95-108">After completing this tutorial, the Azure AD users you have assigned to RightAnswers will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5c95-108">After completing this tutorial, the Azure AD users you have assigned to RightAnswers will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="b5c95-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b5c95-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="b5c95-110">Enabling the application integration for RightAnswers</span><span class="sxs-lookup"><span data-stu-id="b5c95-110">Enabling the application integration for RightAnswers</span></span>
2. <span data-ttu-id="b5c95-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="b5c95-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="b5c95-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="b5c95-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="b5c95-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="b5c95-113">Assigning users</span></span>

<span data-ttu-id="b5c95-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802925.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="b5c95-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802925.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-rightanswers"></a><span data-ttu-id="b5c95-115">Enable the application integration for RightAnswers</span><span class="sxs-lookup"><span data-stu-id="b5c95-115">Enable the application integration for RightAnswers</span></span>
<span data-ttu-id="b5c95-116">The objective of this section is to outline how to enable the application integration for RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="b5c95-116">The objective of this section is to outline how to enable the application integration for RightAnswers.</span></span>

<span data-ttu-id="b5c95-117">**To enable the application integration for RightAnswers, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b5c95-117">**To enable the application integration for RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="b5c95-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5c95-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="b5c95-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b5c95-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="b5c95-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b5c95-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b5c95-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b5c95-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="b5c95-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="b5c95-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="b5c95-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b5c95-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="b5c95-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="b5c95-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="b5c95-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b5c95-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="b5c95-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="b5c95-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="b5c95-127">In the **search box**, type **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="b5c95-127">In the **search box**, type **RightAnswers**.</span></span>
   
    <span data-ttu-id="b5c95-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802926.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="b5c95-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802926.png "Application Gallery")</span></span>
7. <span data-ttu-id="b5c95-129">In the results pane, select **RightAnswers**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b5c95-129">In the results pane, select **RightAnswers**, and then click **Complete** to add the application.</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="b5c95-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="b5c95-130">Configure single sign-on</span></span>

<span data-ttu-id="b5c95-131">The objective of this section is to outline how to enable users to authenticate to RightAnswers with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="b5c95-131">The objective of this section is to outline how to enable users to authenticate to RightAnswers with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="b5c95-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b5c95-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="b5c95-133">In the Azure classic portal, on the **RightAnswers** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="b5c95-133">In the Azure classic portal, on the **RightAnswers** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b5c95-134">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802927.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="b5c95-134">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802927.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="b5c95-135">On the **How would you like users to sign on to RightAnswers** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b5c95-135">On the **How would you like users to sign on to RightAnswers** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="b5c95-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802928.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="b5c95-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802928.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="b5c95-137">On the **Configure App Settings** page, in the **Sign On URL** textbox, type the URL used by your users to sign-on to your RightAnswers application (e.g.: *https://fortify.rightanswers.com/portal/ss/*), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b5c95-137">On the **Configure App Settings** page, in the **Sign On URL** textbox, type the URL used by your users to sign-on to your RightAnswers application (e.g.: *https://fortify.rightanswers.com/portal/ss/*), and then click **Next**.</span></span>
   
    <span data-ttu-id="b5c95-138">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802929.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="b5c95-138">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802929.png "Configure App Settings")</span></span>
4. <span data-ttu-id="b5c95-139">On the **Configure single sign-on at RightAnswers** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="b5c95-139">On the **Configure single sign-on at RightAnswers** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    <span data-ttu-id="b5c95-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802930.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="b5c95-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802930.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="b5c95-141">Send the downloaded metadata file to your RightAnswers support team.</span><span class="sxs-lookup"><span data-stu-id="b5c95-141">Send the downloaded metadata file to your RightAnswers support team.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b5c95-142">Your RightAnswers support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="b5c95-142">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="b5c95-143">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="b5c95-143">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    > 

6. <span data-ttu-id="b5c95-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="b5c95-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b5c95-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802931.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="b5c95-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802931.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="b5c95-146">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="b5c95-146">Configure user provisioning</span></span>

<span data-ttu-id="b5c95-147">In order to enable Azure AD users to log into RightAnswers, they must be provisioned into RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="b5c95-147">In order to enable Azure AD users to log into RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="b5c95-148">In the case of RightAnswers, provisioning is an automated task so there is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="b5c95-148">In the case of RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="b5c95-149">Users are automatically created if necessary during the first single sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="b5c95-149">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="b5c95-150">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="b5c95-150">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="b5c95-151">Assign users</span><span class="sxs-lookup"><span data-stu-id="b5c95-151">Assign users</span></span>
<span data-ttu-id="b5c95-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="b5c95-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="b5c95-153">**To assign users to RightAnswers, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b5c95-153">**To assign users to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="b5c95-154">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="b5c95-154">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="b5c95-155">On the **RightAnswers** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="b5c95-155">On the **RightAnswers** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="b5c95-156">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802932.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="b5c95-156">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC802932.png "Assign Users")</span></span>
3. <span data-ttu-id="b5c95-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="b5c95-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="b5c95-158">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="b5c95-158">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightanswers-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b5c95-159">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b5c95-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="b5c95-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5c95-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>














