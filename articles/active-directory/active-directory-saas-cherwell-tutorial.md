---
title: 'Tutorial: Azure Active Directory integration with Cherwell | Microsoft Docs'
description: Learn how to use Cherwell with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: d5b72801c20f23ffb105bccb9d5f4caee2875d65
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550091"
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="5cf50-103">Tutorial: Azure Active Directory integration with Cherwell</span><span class="sxs-lookup"><span data-stu-id="5cf50-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>
<span data-ttu-id="5cf50-104">The objective of this tutorial is to show the integration of Azure and Cherwell.</span><span class="sxs-lookup"><span data-stu-id="5cf50-104">The objective of this tutorial is to show the integration of Azure and Cherwell.</span></span> <span data-ttu-id="5cf50-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="5cf50-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5cf50-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5cf50-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5cf50-107">A Cherwell single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5cf50-107">A Cherwell single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="5cf50-108">After completing this tutorial, the Azure AD users you have assigned to Cherwell will be able to single sign into the application at your Cherwell company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5cf50-108">After completing this tutorial, the Azure AD users you have assigned to Cherwell will be able to single sign into the application at your Cherwell company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5cf50-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5cf50-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="5cf50-110">Enabling the application integration for Cherwell</span><span class="sxs-lookup"><span data-stu-id="5cf50-110">Enabling the application integration for Cherwell</span></span>
2. <span data-ttu-id="5cf50-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="5cf50-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="5cf50-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5cf50-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5cf50-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5cf50-113">Assigning users</span></span>

<span data-ttu-id="5cf50-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798988.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="5cf50-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798988.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cherwell"></a><span data-ttu-id="5cf50-115">Enable the application integration for Cherwell</span><span class="sxs-lookup"><span data-stu-id="5cf50-115">Enable the application integration for Cherwell</span></span>
<span data-ttu-id="5cf50-116">The objective of this section is to outline how to enable the application integration for Cherwell.</span><span class="sxs-lookup"><span data-stu-id="5cf50-116">The objective of this section is to outline how to enable the application integration for Cherwell.</span></span>

<span data-ttu-id="5cf50-117">**To enable the application integration for Cherwell, perform the following** steps:</span><span class="sxs-lookup"><span data-stu-id="5cf50-117">**To enable the application integration for Cherwell, perform the following** steps:</span></span>
1. <span data-ttu-id="5cf50-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5cf50-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5cf50-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5cf50-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5cf50-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5cf50-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5cf50-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5cf50-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="5cf50-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5cf50-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5cf50-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5cf50-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="5cf50-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5cf50-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5cf50-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="5cf50-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5cf50-127">In the **search box**, type **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-127">In the **search box**, type **Cherwell**.</span></span>
   
   <span data-ttu-id="5cf50-128">![Cherwell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798989.png "Cherwell")</span><span class="sxs-lookup"><span data-stu-id="5cf50-128">![Cherwell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798989.png "Cherwell")</span></span>
7. <span data-ttu-id="5cf50-129">In the results pane, select **Cherwell**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5cf50-129">In the results pane, select **Cherwell**, and then click **Complete** to add the application.</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5cf50-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="5cf50-130">Configure single sign-on</span></span>
   <span data-ttu-id="5cf50-131">![Cherwell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798996.png "Cherwell")</span><span class="sxs-lookup"><span data-stu-id="5cf50-131">![Cherwell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798996.png "Cherwell")</span></span>

<span data-ttu-id="5cf50-132">The objective of this section is to outline how to enable users to authenticate to Cherwell with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="5cf50-132">The objective of this section is to outline how to enable users to authenticate to Cherwell with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="5cf50-133">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5cf50-133">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="5cf50-134">In the Azure classic portal, on the **Cherwell** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5cf50-134">In the Azure classic portal, on the **Cherwell** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5cf50-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798990.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5cf50-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798990.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="5cf50-136">On the **How would you like users to sign on to Cherwell** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-136">On the **How would you like users to sign on to Cherwell** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5cf50-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798991.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5cf50-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798991.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="5cf50-138">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5cf50-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="5cf50-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798992.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="5cf50-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798992.png "Configure App URL")</span></span>
  1. <span data-ttu-id="5cf50-140">In the **Sign On URL** textbox, type the URL used by your users to sign into your **Cherwell** (e.g.: *https://\<company name\>.cherwellondemand.com/cherwellclient*).</span><span class="sxs-lookup"><span data-stu-id="5cf50-140">In the **Sign On URL** textbox, type the URL used by your users to sign into your **Cherwell** (e.g.: *https://\<company name\>.cherwellondemand.com/cherwellclient*).</span></span> 
  2.  <span data-ttu-id="5cf50-141">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-141">Click **Next**.</span></span>
4. <span data-ttu-id="5cf50-142">On the **Configure single sign-on at Cherwell** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5cf50-142">On the **Configure single sign-on at Cherwell** page, perform the following steps:</span></span>
   
   <span data-ttu-id="5cf50-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798993.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5cf50-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798993.png "Configure Single Sign-On")</span></span>
  1.  <span data-ttu-id="5cf50-144">Click **Download certificate**, and then save the certificate locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="5cf50-144">Click **Download certificate**, and then save the certificate locally on your computer.</span></span>
  2.  <span data-ttu-id="5cf50-145">Copy the **Identity Provider URL**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-145">Copy the **Identity Provider URL**.</span></span>
  3.  <span data-ttu-id="5cf50-146">Copy the **Single Sign-On Service URL**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-146">Copy the **Single Sign-On Service URL**.</span></span>
  4.  <span data-ttu-id="5cf50-147">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-147">Click **Next**.</span></span>
5. <span data-ttu-id="5cf50-148">Submit the downloaded certificate, the **Identity Provider URL** and the **Single Sign-On Service URL** to your Cherwell support team.</span><span class="sxs-lookup"><span data-stu-id="5cf50-148">Submit the downloaded certificate, the **Identity Provider URL** and the **Single Sign-On Service URL** to your Cherwell support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5cf50-149">Your Cherwell support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="5cf50-149">Your Cherwell support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="5cf50-150">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="5cf50-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   > 
6. <span data-ttu-id="5cf50-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5cf50-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
  <span data-ttu-id="5cf50-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798994.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5cf50-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798994.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="5cf50-153">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="5cf50-153">Configure user provisioning</span></span>
<span data-ttu-id="5cf50-154">In order to enable Azure AD users to log into Cherwell, they must be provisioned into Cherwell.</span><span class="sxs-lookup"><span data-stu-id="5cf50-154">In order to enable Azure AD users to log into Cherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="5cf50-155">In the case of Cherwell, the user accounts need to be created by your Cherwell support team.</span><span class="sxs-lookup"><span data-stu-id="5cf50-155">In the case of Cherwell, the user accounts need to be created by your Cherwell support team.</span></span>

>[!NOTE]
><span data-ttu-id="5cf50-156">You can use any other Cherwell user account creation tools or APIs provided by Cherwell to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="5cf50-156">You can use any other Cherwell user account creation tools or APIs provided by Cherwell to provision Azure Active Directory user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="5cf50-157">Assign users</span><span class="sxs-lookup"><span data-stu-id="5cf50-157">Assign users</span></span>
<span data-ttu-id="5cf50-158">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="5cf50-158">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="5cf50-159">**To assign users to Cherwell, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5cf50-159">**To assign users to Cherwell, perform the following steps:**</span></span>

1. <span data-ttu-id="5cf50-160">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="5cf50-160">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5cf50-161">On the **Cherwell** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="5cf50-161">On the **Cherwell** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5cf50-162">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798995.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="5cf50-162">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798995.png "Assign Users")</span></span>
3. <span data-ttu-id="5cf50-163">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="5cf50-163">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5cf50-164">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="5cf50-164">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5cf50-165">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5cf50-165">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5cf50-166">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5cf50-166">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















