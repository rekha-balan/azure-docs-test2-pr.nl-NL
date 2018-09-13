---
title: 'Tutorial: Azure Active Directory integration with Chromeriver | Microsoft Docs'
description: Learn how to use Chromeriver with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 71947bd47a41905e38f54a70b4e88125e40326e4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540667"
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="be171-103">Tutorial: Azure Active Directory integration with Chromeriver</span><span class="sxs-lookup"><span data-stu-id="be171-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>
<span data-ttu-id="be171-104">The objective of this tutorial is to show the integration of Azure and Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="be171-104">The objective of this tutorial is to show the integration of Azure and Chromeriver.</span></span>  

<span data-ttu-id="be171-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="be171-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="be171-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="be171-106">A valid Azure subscription</span></span>
* <span data-ttu-id="be171-107">A Chromeriver single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="be171-107">A Chromeriver single sign-on enabled subscription</span></span>

<span data-ttu-id="be171-108">After completing this tutorial, the Azure AD users you have assigned to Chromeriver will be able to single sign into the application at your Chromeriver company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be171-108">After completing this tutorial, the Azure AD users you have assigned to Chromeriver will be able to single sign into the application at your Chromeriver company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="be171-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="be171-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="be171-110">Enabling the application integration for Chromeriver</span><span class="sxs-lookup"><span data-stu-id="be171-110">Enabling the application integration for Chromeriver</span></span>
* <span data-ttu-id="be171-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="be171-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="be171-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="be171-112">Configuring user provisioning</span></span>
* <span data-ttu-id="be171-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="be171-113">Assigning users</span></span>

<span data-ttu-id="be171-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802755.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="be171-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802755.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-chromeriver"></a><span data-ttu-id="be171-115">Enable the application integration for Chromeriver</span><span class="sxs-lookup"><span data-stu-id="be171-115">Enable the application integration for Chromeriver</span></span>
<span data-ttu-id="be171-116">The objective of this section is to outline how to enable the application integration for Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="be171-116">The objective of this section is to outline how to enable the application integration for Chromeriver.</span></span>

<span data-ttu-id="be171-117">**To enable the application integration for Chromeriver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be171-117">**To enable the application integration for Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="be171-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be171-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="be171-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="be171-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="be171-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="be171-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="be171-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="be171-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="be171-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="be171-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="be171-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="be171-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="be171-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="be171-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="be171-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="be171-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
      <span data-ttu-id="be171-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="be171-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="be171-127">In the **search box**, type **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="be171-127">In the **search box**, type **Chromeriver**.</span></span>
   
   <span data-ttu-id="be171-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802756.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="be171-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802756.png "Application Gallery")</span></span>
7. <span data-ttu-id="be171-129">In the results pane, select **Chromeriver**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="be171-129">In the results pane, select **Chromeriver**, and then click **Complete** to add the application.</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="be171-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="be171-130">Configure single sign-on</span></span>

<span data-ttu-id="be171-131">The objective of this section is to outline how to enable users to authenticate to Chromeriver with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="be171-131">The objective of this section is to outline how to enable users to authenticate to Chromeriver with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="be171-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be171-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="be171-133">In the Azure classic portal, on the **Chromeriver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="be171-133">In the Azure classic portal, on the **Chromeriver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="be171-134">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802757.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be171-134">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802757.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="be171-135">On the **How would you like users to sign on to Chromeriver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="be171-135">On the **How would you like users to sign on to Chromeriver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="be171-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802758.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be171-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802758.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="be171-137">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="be171-137">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="be171-138">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802759.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="be171-138">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802759.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="be171-139">In the **Reply URL** textbox, type your Chromeriver **AssertionConsumerService URL** (e.g.: *https://qa-app.chromeriver.com/login/sso/saml/consume?customerId=911*).</span><span class="sxs-lookup"><span data-stu-id="be171-139">In the **Reply URL** textbox, type your Chromeriver **AssertionConsumerService URL** (e.g.: *https://qa-app.chromeriver.com/login/sso/saml/consume?customerId=911*).</span></span>  
   
     >[!NOTE]
     ><span data-ttu-id="be171-140">You can get this value from your Chromeriver support team.</span><span class="sxs-lookup"><span data-stu-id="be171-140">You can get this value from your Chromeriver support team.</span></span>
     >  
   2. <span data-ttu-id="be171-141">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="be171-141">Click **Next**</span></span>
4. <span data-ttu-id="be171-142">On the **Configure single sign-on at Chromeriver** page, to download your metadata, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="be171-142">On the **Configure single sign-on at Chromeriver** page, to download your metadata, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="be171-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802760.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be171-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802760.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="be171-144">Send the downloaded metadata file to your Chromeriver support team.</span><span class="sxs-lookup"><span data-stu-id="be171-144">Send the downloaded metadata file to your Chromeriver support team.</span></span>
   
 >[!NOTE]
 ><span data-ttu-id="be171-145">Your Chromeriver support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="be171-145">Your Chromeriver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="be171-146">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="be171-146">You will get a notification when SSO has been enabled for your subscription.</span></span>
 >

6. <span data-ttu-id="be171-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="be171-147">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="be171-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802761.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="be171-148">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802761.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="be171-149">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="be171-149">Configure user provisioning</span></span>

<span data-ttu-id="be171-150">In order to enable Azure AD users to log into Chromeriver, they must be provisioned into Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="be171-150">In order to enable Azure AD users to log into Chromeriver, they must be provisioned into Chromeriver.</span></span>  

* <span data-ttu-id="be171-151">In the case of Chromeriver, the user accounts need to be created by your Chromeriver support team.</span><span class="sxs-lookup"><span data-stu-id="be171-151">In the case of Chromeriver, the user accounts need to be created by your Chromeriver support team.</span></span>

>[!NOTE]
><span data-ttu-id="be171-152">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="be171-152">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="be171-153">Assign users</span><span class="sxs-lookup"><span data-stu-id="be171-153">Assign users</span></span>
<span data-ttu-id="be171-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="be171-154">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="be171-155">**To assign users to Chromeriver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be171-155">**To assign users to Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="be171-156">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="be171-156">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="be171-157">On the **Chromeriver** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="be171-157">On the **Chromeriver** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="be171-158">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802762.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="be171-158">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC802762.png "Assign Users")</span></span>
3. <span data-ttu-id="be171-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="be171-159">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="be171-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="be171-160">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-chromeriver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="be171-161">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="be171-161">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="be171-162">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be171-162">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>














