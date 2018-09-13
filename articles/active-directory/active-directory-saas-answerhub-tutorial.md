---
title: 'Tutorial: Azure Active Directory integration with AnswerHub | Microsoft Docs'
description: Learn how to use AnswerHub with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 7cc68645329adcb43bf490417f3b96c768192246
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552933"
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="3a489-103">Tutorial: Azure Active Directory integration with AnswerHub</span><span class="sxs-lookup"><span data-stu-id="3a489-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>
<span data-ttu-id="3a489-104">The objective of this tutorial is to show the integration of Azure and [AnswerHub](http://www.dzonesoftware.com/products/answerhub-question-answer-software).</span><span class="sxs-lookup"><span data-stu-id="3a489-104">The objective of this tutorial is to show the integration of Azure and [AnswerHub](http://www.dzonesoftware.com/products/answerhub-question-answer-software).</span></span>  
<span data-ttu-id="3a489-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="3a489-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="3a489-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="3a489-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3a489-107">An [AnswerHub](http://www.dzonesoftware.com/products/answerhub-question-answer-software) single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3a489-107">An [AnswerHub](http://www.dzonesoftware.com/products/answerhub-question-answer-software) single sign-on enabled subscription</span></span>

<span data-ttu-id="3a489-108">After completing this tutorial, the Azure AD users you have assigned to AnswerHub will be able to access the application via single sign-on (SSO) at your AnswerHub company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a489-108">After completing this tutorial, the Azure AD users you have assigned to AnswerHub will be able to access the application via single sign-on (SSO) at your AnswerHub company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="3a489-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3a489-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="3a489-110">Enabling the application integration for AnswerHub</span><span class="sxs-lookup"><span data-stu-id="3a489-110">Enabling the application integration for AnswerHub</span></span>
2. <span data-ttu-id="3a489-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="3a489-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="3a489-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="3a489-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="3a489-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="3a489-113">Assigning users</span></span>

<span data-ttu-id="3a489-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785165.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="3a489-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785165.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-answerhub"></a><span data-ttu-id="3a489-115">Enable the application integration for AnswerHub</span><span class="sxs-lookup"><span data-stu-id="3a489-115">Enable the application integration for AnswerHub</span></span>
<span data-ttu-id="3a489-116">The objective of this section is to outline how to enable the application integration for AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="3a489-116">The objective of this section is to outline how to enable the application integration for AnswerHub.</span></span>

<span data-ttu-id="3a489-117">**To enable the application integration for AnswerHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a489-117">**To enable the application integration for AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="3a489-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a489-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3a489-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3a489-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3a489-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3a489-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3a489-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3a489-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="3a489-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="3a489-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3a489-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3a489-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="3a489-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="3a489-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3a489-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3a489-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="3a489-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="3a489-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3a489-127">In the **search box**, type **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="3a489-127">In the **search box**, type **AnswerHub**.</span></span>
   
   <span data-ttu-id="3a489-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785166.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="3a489-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785166.png "Application Gallery")</span></span>
7. <span data-ttu-id="3a489-129">In the results pane, select **AnswerHub**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3a489-129">In the results pane, select **AnswerHub**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="3a489-130">![AnswerHub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785167.png "AnswerHub")</span><span class="sxs-lookup"><span data-stu-id="3a489-130">![AnswerHub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785167.png "AnswerHub")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="3a489-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="3a489-131">Configure single sign-on</span></span>
<span data-ttu-id="3a489-132">The objective of this section is to outline how to enable users to authenticate to AnswerHub with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="3a489-132">The objective of this section is to outline how to enable users to authenticate to AnswerHub with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="3a489-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="3a489-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="3a489-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="3a489-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="3a489-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a489-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="3a489-136">In the Azure classic portal, on the **AnswerHub** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="3a489-136">In the Azure classic portal, on the **AnswerHub** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3a489-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785168.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3a489-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785168.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="3a489-138">On the **How would you like users to sign on to AnswerHub** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a489-138">On the **How would you like users to sign on to AnswerHub** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3a489-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785169.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3a489-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785169.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="3a489-140">On the **Configure App URL** page, in the **AnswerHub Sign In URL** textbox, type your URL using the following pattern "*https://company.answerhub.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a489-140">On the **Configure App URL** page, in the **AnswerHub Sign In URL** textbox, type your URL using the following pattern "*https://company.answerhub.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="3a489-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785170.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="3a489-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785170.png "Configure App URL")</span></span>
4. <span data-ttu-id="3a489-142">On the **Configure single sign-on at AnswerHub** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="3a489-142">On the **Configure single sign-on at AnswerHub** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="3a489-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785171.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3a489-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785171.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="3a489-144">In a different web browser window, log into your AnswerHub company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3a489-144">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3a489-145">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="3a489-145">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   > 
6. <span data-ttu-id="3a489-146">Go to **Administration**.</span><span class="sxs-lookup"><span data-stu-id="3a489-146">Go to **Administration**.</span></span>
7. <span data-ttu-id="3a489-147">Click the **User and Group** tab.</span><span class="sxs-lookup"><span data-stu-id="3a489-147">Click the **User and Group** tab.</span></span>
8. <span data-ttu-id="3a489-148">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="3a489-148">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>
9. <span data-ttu-id="3a489-149">Click **IDP Config** tab.</span><span class="sxs-lookup"><span data-stu-id="3a489-149">Click **IDP Config** tab.</span></span>
10. <span data-ttu-id="3a489-150">On the **IDP Config** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a489-150">On the **IDP Config** tab, perform the following steps:</span></span>

  <span data-ttu-id="3a489-151">![SAML Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785172.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="3a489-151">![SAML Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785172.png "SAML Setup")</span></span>  
  1. <span data-ttu-id="3a489-152">In the Azure classic portal, on the **Configure single sign-on at AnswerHub** dialog page, copy the **Remote Login URL** value, and then paste it into the **IDP Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3a489-152">In the Azure classic portal, on the **Configure single sign-on at AnswerHub** dialog page, copy the **Remote Login URL** value, and then paste it into the **IDP Login URL** textbox.</span></span>
  2. <span data-ttu-id="3a489-153">In the Azure classic portal, on the **Configure single sign-on at AnswerHub** dialog page, copy the **Remote Logout URL** value, and then paste it into the **IDP Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3a489-153">In the Azure classic portal, on the **Configure single sign-on at AnswerHub** dialog page, copy the **Remote Logout URL** value, and then paste it into the **IDP Logout URL** textbox.</span></span>
  3. <span data-ttu-id="3a489-154">In the Azure classic portal, on the **Configure single sign-on at AnswerHub** dialog page, copy the **Name Identifier Format** value, and then paste it into the **IDP Name Identifier Format** textbox.</span><span class="sxs-lookup"><span data-stu-id="3a489-154">In the Azure classic portal, on the **Configure single sign-on at AnswerHub** dialog page, copy the **Name Identifier Format** value, and then paste it into the **IDP Name Identifier Format** textbox.</span></span>
  4. <span data-ttu-id="3a489-155">Click **Keys and Certificates**.</span><span class="sxs-lookup"><span data-stu-id="3a489-155">Click **Keys and Certificates**.</span></span>
11. <span data-ttu-id="3a489-156">On the Keys and Certificates tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a489-156">On the Keys and Certificates tab, perform the following steps:</span></span>
    
  <span data-ttu-id="3a489-157">![Keys and Certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785173.png "Keys and Certificates")</span><span class="sxs-lookup"><span data-stu-id="3a489-157">![Keys and Certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785173.png "Keys and Certificates")</span></span>  
  1. <span data-ttu-id="3a489-158">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="3a489-158">Create a **base-64 encoded** file from your downloaded certificate.</span></span>
  
    >[!TIP]
    ><span data-ttu-id="3a489-159">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="3a489-159">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
    > 
  2. <span data-ttu-id="3a489-160">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span><span class="sxs-lookup"><span data-stu-id="3a489-160">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  3. <span data-ttu-id="3a489-161">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3a489-161">Click **Save**.</span></span>
12. <span data-ttu-id="3a489-162">On the **IDP Config** tab, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3a489-162">On the **IDP Config** tab, click **Save**.</span></span>
13. <span data-ttu-id="3a489-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="3a489-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
  <span data-ttu-id="3a489-164">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785174.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="3a489-164">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785174.png "Configure single sign-on")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="3a489-165">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="3a489-165">Configure user provisioning</span></span>
<span data-ttu-id="3a489-166">In order to enable Azure AD users to log into AnswerHub, they must be provisioned into AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="3a489-166">In order to enable Azure AD users to log into AnswerHub, they must be provisioned into AnswerHub.</span></span>  

* <span data-ttu-id="3a489-167">In the case of AnswerHub, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3a489-167">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="3a489-168">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a489-168">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3a489-169">Log in to your **AnswerHub** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="3a489-169">Log in to your **AnswerHub** company site as administrator.</span></span>
2. <span data-ttu-id="3a489-170">Go to **Administration**.</span><span class="sxs-lookup"><span data-stu-id="3a489-170">Go to **Administration**.</span></span>
3. <span data-ttu-id="3a489-171">Click the **Users & Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="3a489-171">Click the **Users & Groups** tab.</span></span>
4. <span data-ttu-id="3a489-172">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span><span class="sxs-lookup"><span data-stu-id="3a489-172">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="3a489-173">![Users & Groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785175.png "Users & Groups")</span><span class="sxs-lookup"><span data-stu-id="3a489-173">![Users & Groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785175.png "Users & Groups")</span></span>
5. <span data-ttu-id="3a489-174">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3a489-174">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="3a489-175">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="3a489-175">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>
> 

## <a name="assign-users"></a><span data-ttu-id="3a489-176">Assign users</span><span class="sxs-lookup"><span data-stu-id="3a489-176">Assign users</span></span>
<span data-ttu-id="3a489-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="3a489-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="3a489-178">**To assign users to AnswerHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3a489-178">**To assign users to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="3a489-179">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="3a489-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3a489-180">On the **AnswerHub** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="3a489-180">On the **AnswerHub** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3a489-181">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785176.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="3a489-181">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC785176.png "Assign users")</span></span>
3. <span data-ttu-id="3a489-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="3a489-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="3a489-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="3a489-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-answerhub-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3a489-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3a489-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3a489-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a489-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















