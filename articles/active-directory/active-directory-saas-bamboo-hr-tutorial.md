---
title: 'Tutorial: Azure Active Directory Integration with Bamboo HR | Microsoft Docs'
description: Learn how to use Bamboo HR with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e6aa5079d9a841d3dc7cbfb14f765e2a7ed785b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552815"
---
# <a name="tutorial-azure-active-directory-integration-with-bamboo-hr"></a><span data-ttu-id="82d10-103">Tutorial: Azure Active Directory Integration with Bamboo HR</span><span class="sxs-lookup"><span data-stu-id="82d10-103">Tutorial: Azure Active Directory Integration with Bamboo HR</span></span>
<span data-ttu-id="82d10-104">The objective of this tutorial is to show the integration of Azure and BambooHR.</span><span class="sxs-lookup"><span data-stu-id="82d10-104">The objective of this tutorial is to show the integration of Azure and BambooHR.</span></span>  

<span data-ttu-id="82d10-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="82d10-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="82d10-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="82d10-106">A valid Azure subscription</span></span>
* <span data-ttu-id="82d10-107">A BambooHR single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="82d10-107">A BambooHR single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="82d10-108">After completing this tutorial, the Azure AD users you have assigned to BambooHR will be able to single sign into the application at your BambooHR company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82d10-108">After completing this tutorial, the Azure AD users you have assigned to BambooHR will be able to single sign into the application at your BambooHR company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="82d10-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="82d10-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="82d10-110">Enabling the application integration for BambooHR</span><span class="sxs-lookup"><span data-stu-id="82d10-110">Enabling the application integration for BambooHR</span></span>
* <span data-ttu-id="82d10-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="82d10-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="82d10-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="82d10-112">Configuring user provisioning</span></span>
* <span data-ttu-id="82d10-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="82d10-113">Assigning users</span></span>

<span data-ttu-id="82d10-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796685.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="82d10-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796685.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-bamboohr"></a><span data-ttu-id="82d10-115">Enable the application integration for BambooHR</span><span class="sxs-lookup"><span data-stu-id="82d10-115">Enable the application integration for BambooHR</span></span>
<span data-ttu-id="82d10-116">The objective of this section is to outline how to enable the application integration for BambooHR.</span><span class="sxs-lookup"><span data-stu-id="82d10-116">The objective of this section is to outline how to enable the application integration for BambooHR.</span></span>

<span data-ttu-id="82d10-117">**To enable the application integration for BambooHR, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d10-117">**To enable the application integration for BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="82d10-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82d10-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="82d10-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="82d10-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="82d10-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="82d10-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="82d10-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="82d10-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="82d10-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="82d10-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="82d10-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="82d10-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="82d10-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="82d10-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="82d10-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="82d10-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="82d10-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="82d10-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="82d10-127">In the **search box**, type **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="82d10-127">In the **search box**, type **BambooHR**.</span></span>
   
   <span data-ttu-id="82d10-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796686.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="82d10-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796686.png "Application gallery")</span></span>
7. <span data-ttu-id="82d10-129">In the results pane, select **BambooHR**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="82d10-129">In the results pane, select **BambooHR**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="82d10-130">![BambooHR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796687.png "BambooHR")</span><span class="sxs-lookup"><span data-stu-id="82d10-130">![BambooHR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796687.png "BambooHR")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="82d10-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="82d10-131">Configure single sign-on</span></span>

<span data-ttu-id="82d10-132">The objective of this section is to outline how to enable users to authenticate to BambooHR with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="82d10-132">The objective of this section is to outline how to enable users to authenticate to BambooHR with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="82d10-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="82d10-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="82d10-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="82d10-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="82d10-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d10-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="82d10-136">In the Azure classic portal, on the **BambooHR** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="82d10-136">In the Azure classic portal, on the **BambooHR** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="82d10-137">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796685.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="82d10-137">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796685.png "Scenario")</span></span>
2. <span data-ttu-id="82d10-138">On the **How would you like users to sign on to BambooHR** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="82d10-138">On the **How would you like users to sign on to BambooHR** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="82d10-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796688.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="82d10-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796688.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="82d10-140">On the **Configure App URL** page, in the **BambooHR Sign On URL** textbox, type your URL used by your users to sign on to your BambooHR application (e.g.: https://company.bamboohr.com), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="82d10-140">On the **Configure App URL** page, in the **BambooHR Sign On URL** textbox, type your URL used by your users to sign on to your BambooHR application (e.g.: https://company.bamboohr.com), and then click **Next**.</span></span>
   
   <span data-ttu-id="82d10-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796689.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="82d10-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796689.png "Configure app URL")</span></span>
4. <span data-ttu-id="82d10-142">On the **Configure single sign-on at BambooHR** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="82d10-142">On the **Configure single sign-on at BambooHR** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="82d10-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796690.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="82d10-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796690.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="82d10-144">In a different web browser window, log into your BambooHR company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="82d10-144">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>
6. <span data-ttu-id="82d10-145">On the homepage, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d10-145">On the homepage, perform the following steps:</span></span>
   
   <span data-ttu-id="82d10-146">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796691.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="82d10-146">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796691.png "Single Sign-On")</span></span>   
   1. <span data-ttu-id="82d10-147">Click **Apps**.</span><span class="sxs-lookup"><span data-stu-id="82d10-147">Click **Apps**.</span></span>
   2. <span data-ttu-id="82d10-148">In the apps menu on the left, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="82d10-148">In the apps menu on the left, click **Single Sign-On**.</span></span>
   3. <span data-ttu-id="82d10-149">Click **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="82d10-149">Click **SAML Single Sign-On**.</span></span>
7. <span data-ttu-id="82d10-150">In the **SAML Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d10-150">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
   <span data-ttu-id="82d10-151">![SAML Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796692.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="82d10-151">![SAML Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796692.png "SAML Single Sign-On")</span></span>
   
   1. <span data-ttu-id="82d10-152">In the Azure classic portal, on the **Configure single sign-on at BambooHR** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the \*\*SSO Login URL \*\* textbox.</span><span class="sxs-lookup"><span data-stu-id="82d10-152">In the Azure classic portal, on the **Configure single sign-on at BambooHR** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the \*\*SSO Login URL \*\* textbox.</span></span>
   2. <span data-ttu-id="82d10-153">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="82d10-153">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
   
      >[!TIP]
      ><span data-ttu-id="82d10-154">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="82d10-154">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
      > 
   3. <span data-ttu-id="82d10-155">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="82d10-155">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   4. <span data-ttu-id="82d10-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="82d10-156">Click **Save**.</span></span>
8. <span data-ttu-id="82d10-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="82d10-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="82d10-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796693.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="82d10-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796693.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="82d10-159">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="82d10-159">Configure user provisioning</span></span>

<span data-ttu-id="82d10-160">In order to enable Azure AD users to log into BambooHR, they must be provisioned into BambooHR.</span><span class="sxs-lookup"><span data-stu-id="82d10-160">In order to enable Azure AD users to log into BambooHR, they must be provisioned into BambooHR.</span></span>  

* <span data-ttu-id="82d10-161">In the case of BambooHR, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="82d10-161">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="82d10-162">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d10-162">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="82d10-163">Log in to your **BambooHR** site as administrator.</span><span class="sxs-lookup"><span data-stu-id="82d10-163">Log in to your **BambooHR** site as administrator.</span></span>
2. <span data-ttu-id="82d10-164">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="82d10-164">In the toolbar on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="82d10-165">![Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796694.png "Setting")</span><span class="sxs-lookup"><span data-stu-id="82d10-165">![Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796694.png "Setting")</span></span>
3. <span data-ttu-id="82d10-166">Click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="82d10-166">Click **Overview**.</span></span>
4. <span data-ttu-id="82d10-167">In the left navigation pane, go to **Security \> Users**.</span><span class="sxs-lookup"><span data-stu-id="82d10-167">In the left navigation pane, go to **Security \> Users**.</span></span>
5. <span data-ttu-id="82d10-168">Type the user name, password and email address of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="82d10-168">Type the user name, password and email address of a valid AAD account you want to provision into the related textboxes.</span></span>
6. <span data-ttu-id="82d10-169">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="82d10-169">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="82d10-170">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="82d10-170">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="82d10-171">Assign users</span><span class="sxs-lookup"><span data-stu-id="82d10-171">Assign users</span></span>
<span data-ttu-id="82d10-172">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="82d10-172">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="82d10-173">**To assign users to BambooHR, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d10-173">**To assign users to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="82d10-174">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="82d10-174">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="82d10-175">On the **BambooHR** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="82d10-175">On the **BambooHR** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="82d10-176">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796695.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="82d10-176">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC796695.png "Assign users")</span></span>
3. <span data-ttu-id="82d10-177">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="82d10-177">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="82d10-178">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="82d10-178">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bamboo-hr-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="82d10-179">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="82d10-179">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="82d10-180">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82d10-180">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















