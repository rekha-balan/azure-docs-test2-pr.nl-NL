---
title: 'Tutorial: Azure Active Directory integration with Directions on Microsoft | Microsoft Docs'
description: Learn how to use Directions on Microsoft with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 4c7eb39c4dd3d7404c25e1a70064a0d4bfd65028
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554963"
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="19f34-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="19f34-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>
<span data-ttu-id="19f34-104">The objective of this tutorial is to show the integration of Azure Active Directory and Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19f34-104">The objective of this tutorial is to show the integration of Azure Active Directory and Directions on Microsoft.</span></span>  

<span data-ttu-id="19f34-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="19f34-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="19f34-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="19f34-106">A valid Azure subscription</span></span>
* <span data-ttu-id="19f34-107">A Directions on Microsoft subscription</span><span class="sxs-lookup"><span data-stu-id="19f34-107">A Directions on Microsoft subscription</span></span>

<span data-ttu-id="19f34-108">If you don’t have a federated Directions on Microsoft subscription yet, email a request to **service@DirectionsOnMicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="19f34-108">If you don’t have a federated Directions on Microsoft subscription yet, email a request to **service@DirectionsOnMicrosoft.com**.</span></span>

<span data-ttu-id="19f34-109">After completing this tutorial, the Azure Active Directory users you have assigned to Directions on Microsoft will be able to single sign into the application using single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19f34-109">After completing this tutorial, the Azure Active Directory users you have assigned to Directions on Microsoft will be able to single sign into the application using single sign-on.</span></span>

<span data-ttu-id="19f34-110">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19f34-110">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="19f34-111">Enabling the application integration for Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="19f34-111">Enabling the application integration for Directions on Microsoft</span></span>
* <span data-ttu-id="19f34-112">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="19f34-112">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="19f34-113">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="19f34-113">Configuring user provisioning</span></span>
* <span data-ttu-id="19f34-114">Assigning users</span><span class="sxs-lookup"><span data-stu-id="19f34-114">Assigning users</span></span>

<span data-ttu-id="19f34-115">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786877.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="19f34-115">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786877.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-directions-on-microsoft"></a><span data-ttu-id="19f34-116">Enable the application integration for Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="19f34-116">Enable the application integration for Directions on Microsoft</span></span>
<span data-ttu-id="19f34-117">The objective of this section is to outline how to enable the application integration for Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19f34-117">The objective of this section is to outline how to enable the application integration for Directions on Microsoft.</span></span>

<span data-ttu-id="19f34-118">**To enable the application integration for Directions on Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19f34-118">**To enable the application integration for Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="19f34-119">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19f34-119">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="19f34-120">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="19f34-120">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="19f34-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19f34-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="19f34-122">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19f34-122">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="19f34-123">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="19f34-123">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="19f34-124">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19f34-124">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="19f34-125">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="19f34-125">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="19f34-126">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="19f34-126">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="19f34-127">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="19f34-127">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="19f34-128">In the **search box**, type **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="19f34-128">In the **search box**, type **Directions on Microsoft**.</span></span>
   
   <span data-ttu-id="19f34-129">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786878.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="19f34-129">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786878.png "Application Gallery")</span></span>
7. <span data-ttu-id="19f34-130">In the results pane, select **Directions on Microsoft**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="19f34-130">In the results pane, select **Directions on Microsoft**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="19f34-131">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC793922.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="19f34-131">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC793922.png "Scenario")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="19f34-132">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="19f34-132">Configure single sign-on</span></span>

<span data-ttu-id="19f34-133">The objective of this section is to outline how to enable users to authenticate to Directions on Microsoft with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="19f34-133">The objective of this section is to outline how to enable users to authenticate to Directions on Microsoft with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="19f34-134">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19f34-134">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="19f34-135">In the Azure classic portal, on the **Directions on Microsoft** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="19f34-135">In the Azure classic portal, on the **Directions on Microsoft** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="19f34-136">![Enable Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786879.png "Enable Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19f34-136">![Enable Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786879.png "Enable Single Sign-On")</span></span>
2. <span data-ttu-id="19f34-137">On the **How would you like users to sign on to Directions on Microsoft** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19f34-137">On the **How would you like users to sign on to Directions on Microsoft** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="19f34-138">![Microsoft Azure AD Singel Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786880.png "Microsoft Azure AD Singel Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19f34-138">![Microsoft Azure AD Singel Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786880.png "Microsoft Azure AD Singel Sign-On")</span></span>
3. <span data-ttu-id="19f34-139">On the **Configure App URL** page, in the Sign On URL textbox, type **https://www.directionsonmicrosoft.com/user/login**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19f34-139">On the **Configure App URL** page, in the Sign On URL textbox, type **https://www.directionsonmicrosoft.com/user/login**, and then click **Next**.</span></span>
   
   <span data-ttu-id="19f34-140">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786881.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="19f34-140">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786881.png "Configure App URL")</span></span>
4. <span data-ttu-id="19f34-141">On the **Configure single sign-on at Directions on Microsoft** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="19f34-141">On the **Configure single sign-on at Directions on Microsoft** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="19f34-142">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786882.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19f34-142">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786882.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="19f34-143">Send the metadata file to the Directions on Microsoft support team (*service@DirectionsOnMicrosoft.com*).</span><span class="sxs-lookup"><span data-stu-id="19f34-143">Send the metadata file to the Directions on Microsoft support team (*service@DirectionsOnMicrosoft.com*).</span></span> <span data-ttu-id="19f34-144">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span><span class="sxs-lookup"><span data-stu-id="19f34-144">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="19f34-145">Single sign-on for Directions on Microsoft needs to be enabled by the Directions on Microsoft support team.</span><span class="sxs-lookup"><span data-stu-id="19f34-145">Single sign-on for Directions on Microsoft needs to be enabled by the Directions on Microsoft support team.</span></span> <span data-ttu-id="19f34-146">You will receive a notification when single sign-on has been enabled.</span><span class="sxs-lookup"><span data-stu-id="19f34-146">You will receive a notification when single sign-on has been enabled.</span></span> 
   > 
6. <span data-ttu-id="19f34-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="19f34-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
  <span data-ttu-id="19f34-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786883.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="19f34-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786883.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="19f34-149">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="19f34-149">Configure user provisioning</span></span>

<span data-ttu-id="19f34-150">There is no action item for you to configure user provisioning to Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19f34-150">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="19f34-151">When an assigned user tries to log into Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="19f34-151">When an assigned user tries to log into Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="19f34-152">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19f34-152">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

## <a name="assign-users"></a><span data-ttu-id="19f34-153">Assign users</span><span class="sxs-lookup"><span data-stu-id="19f34-153">Assign users</span></span>
<span data-ttu-id="19f34-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="19f34-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="19f34-155">**To assign users to Directions on Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19f34-155">**To assign users to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="19f34-156">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="19f34-156">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="19f34-157">On the **Directions on Microsoft** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="19f34-157">On the **Directions on Microsoft** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="19f34-158">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786884.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="19f34-158">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC786884.png "Assign users")</span></span>
3. <span data-ttu-id="19f34-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="19f34-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="19f34-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="19f34-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-directions-microsoft-tutorial/IC767830.png "Yes")</span></span>















