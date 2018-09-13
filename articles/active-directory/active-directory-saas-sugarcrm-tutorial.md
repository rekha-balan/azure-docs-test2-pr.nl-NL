---
title: 'Tutorial: Azure Active Directory integration integration with SugarCRM | Microsoft Docs'
description: Learn how to use SugarCRM with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/07/2017
ms.author: jeedes
ms.openlocfilehash: 6c853d6acbe6d5abae6ea2a72800f01217fb3dc7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661030"
---
# <a name="tutorial-azure-active-directory-integration-integration-with-sugarcrm"></a><span data-ttu-id="cbccb-103">Tutorial: Azure Active Directory integration integration with SugarCRM</span><span class="sxs-lookup"><span data-stu-id="cbccb-103">Tutorial: Azure Active Directory integration integration with SugarCRM</span></span>
<span data-ttu-id="cbccb-104">The objective of this tutorial is to show the integration of Azure and Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="cbccb-104">The objective of this tutorial is to show the integration of Azure and Sugar CRM.</span></span>  

<span data-ttu-id="cbccb-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="cbccb-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="cbccb-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="cbccb-106">A valid Azure subscription</span></span>
* <span data-ttu-id="cbccb-107">A Sugar CRM single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cbccb-107">A Sugar CRM single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="cbccb-108">After completing this tutorial, the Azure AD users you have assigned to Sugar CRM will be able to sign into the application using SSO at your Sugar CRM company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cbccb-108">After completing this tutorial, the Azure AD users you have assigned to Sugar CRM will be able to sign into the application using SSO at your Sugar CRM company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="cbccb-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cbccb-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="cbccb-110">Enabling the application integration for Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="cbccb-110">Enabling the application integration for Sugar CRM</span></span>
2. <span data-ttu-id="cbccb-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="cbccb-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="cbccb-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="cbccb-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="cbccb-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="cbccb-113">Assigning users</span></span>

<span data-ttu-id="cbccb-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795881.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="cbccb-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795881.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-sugar-crm"></a><span data-ttu-id="cbccb-115">Enable the application integration for Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="cbccb-115">Enable the application integration for Sugar CRM</span></span>
<span data-ttu-id="cbccb-116">The objective of this section is to outline how to enable the application integration for Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="cbccb-116">The objective of this section is to outline how to enable the application integration for Sugar CRM.</span></span>

<span data-ttu-id="cbccb-117">**To enable the application integration for Sugar CRM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbccb-117">**To enable the application integration for Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="cbccb-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="cbccb-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="cbccb-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="cbccb-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="cbccb-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="cbccb-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="cbccb-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="cbccb-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="cbccb-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="cbccb-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="cbccb-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="cbccb-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="cbccb-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="cbccb-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="cbccb-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="cbccb-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="cbccb-127">In the **search box**, type **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-127">In the **search box**, type **Sugar CRM**.</span></span>
   
    <span data-ttu-id="cbccb-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795882.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="cbccb-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795882.png "Application Gallery")</span></span>

7. <span data-ttu-id="cbccb-129">In the results pane, select **Sugar CRM**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="cbccb-129">In the results pane, select **Sugar CRM**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="cbccb-130">![Sugar CRM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795883.png "Sugar CRM")</span><span class="sxs-lookup"><span data-stu-id="cbccb-130">![Sugar CRM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795883.png "Sugar CRM")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="cbccb-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="cbccb-131">Configure single sign-on</span></span>
<span data-ttu-id="cbccb-132">The objective of this section is to outline how to enable users to authenticate to Sugar CRM with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="cbccb-132">The objective of this section is to outline how to enable users to authenticate to Sugar CRM with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="cbccb-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Sugar CRM tenant.</span><span class="sxs-lookup"><span data-stu-id="cbccb-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Sugar CRM tenant.</span></span>  

<span data-ttu-id="cbccb-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="cbccb-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="cbccb-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbccb-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="cbccb-136">In the Azure classic portal, on the **Sugar CRM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="cbccb-136">In the Azure classic portal, on the **Sugar CRM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="cbccb-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795884.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbccb-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795884.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="cbccb-138">On the **How would you like users to sign on to Sugar CRM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-138">On the **How would you like users to sign on to Sugar CRM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="cbccb-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795885.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbccb-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795885.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="cbccb-140">On the **Configure App URL** page, in the **Sugar CRM Sign On URL** textbox, type the URL used by your users to sign-on to your Sugar CRM application (e.g.: "*http://company.sugarondemand.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-140">On the **Configure App URL** page, in the **Sugar CRM Sign On URL** textbox, type the URL used by your users to sign-on to your Sugar CRM application (e.g.: "*http://company.sugarondemand.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="cbccb-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795886.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="cbccb-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795886.png "Configure App URL")</span></span>

4. <span data-ttu-id="cbccb-142">On the **Configure single sign-on at Sugar CRM** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cbccb-142">On the **Configure single sign-on at Sugar CRM** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="cbccb-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC796918.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbccb-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC796918.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="cbccb-144">In a different web browser window, log into your Sugar CRM company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cbccb-144">In a different web browser window, log into your Sugar CRM company site as an administrator.</span></span>

6. <span data-ttu-id="cbccb-145">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-145">Go to **Admin**.</span></span>
   
    <span data-ttu-id="cbccb-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="cbccb-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795888.png "Admin")</span></span>

7. <span data-ttu-id="cbccb-147">In the **Administration** section, click **Password Management**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-147">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="cbccb-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795889.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="cbccb-148">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795889.png "Administration")</span></span>

8. <span data-ttu-id="cbccb-149">Select **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-149">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="cbccb-150">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795890.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="cbccb-150">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795890.png "Administration")</span></span>

9. <span data-ttu-id="cbccb-151">In the **SAML Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbccb-151">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="cbccb-152">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795891.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="cbccb-152">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795891.png "SAML Authentication")</span></span>   
  1. <span data-ttu-id="cbccb-153">In the Azure classic portal, on the **Configure single sign-on at Sugar CRM** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="cbccb-153">In the Azure classic portal, on the **Configure single sign-on at Sugar CRM** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
  2. <span data-ttu-id="cbccb-154">In the Azure classic portal, on the **Configure single sign-on at Sugar CRM** dialog page, copy the **Remote Login URL** value, and then paste it into the **SLO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="cbccb-154">In the Azure classic portal, on the **Configure single sign-on at Sugar CRM** dialog page, copy the **Remote Login URL** value, and then paste it into the **SLO URL** textbox.</span></span>
  3. <span data-ttu-id="cbccb-155">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="cbccb-155">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>
      
     >[!TIP]
     ><span data-ttu-id="cbccb-156">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="cbccb-156">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
     > 

  4. <span data-ttu-id="cbccb-157">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="cbccb-157">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  5. <span data-ttu-id="cbccb-158">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-158">Click **Save**.</span></span>

10. <span data-ttu-id="cbccb-159">In the Azure classic portal, on the **Configure single sign-on at Sugar CRM** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-159">In the Azure classic portal, on the **Configure single sign-on at Sugar CRM** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="cbccb-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC796919.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cbccb-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC796919.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="cbccb-161">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="cbccb-161">Configure user provisioning</span></span>
<span data-ttu-id="cbccb-162">In order to enable Azure AD users to log into Sugar CRM, they must be provisioned to Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="cbccb-162">In order to enable Azure AD users to log into Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="cbccb-163">In the case of Sugar CRM, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="cbccb-163">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="cbccb-164">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbccb-164">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="cbccb-165">Log in to your **Sugar CRM** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="cbccb-165">Log in to your **Sugar CRM** company site as administrator.</span></span>
2. <span data-ttu-id="cbccb-166">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-166">Go to **Admin**.</span></span>
   
    <span data-ttu-id="cbccb-167">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="cbccb-167">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795888.png "Admin")</span></span>

3. <span data-ttu-id="cbccb-168">In the **Administration** section, click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-168">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="cbccb-169">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795893.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="cbccb-169">![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795893.png "Administration")</span></span>

4. <span data-ttu-id="cbccb-170">Go to **Users \> Create New User**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-170">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="cbccb-171">![Create New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795894.png "Create New User")</span><span class="sxs-lookup"><span data-stu-id="cbccb-171">![Create New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795894.png "Create New User")</span></span>

5. <span data-ttu-id="cbccb-172">On the **User Profile** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbccb-172">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="cbccb-173">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795895.png "New User")</span><span class="sxs-lookup"><span data-stu-id="cbccb-173">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795895.png "New User")</span></span>
  * <span data-ttu-id="cbccb-174">Type the user name, last name and email address of a valid Azure Active Directory user into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="cbccb-174">Type the user name, last name and email address of a valid Azure Active Directory user into the related textboxes.</span></span>
6. <span data-ttu-id="cbccb-175">As **Status**, select **Active**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-175">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="cbccb-176">On the Password tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbccb-176">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="cbccb-177">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795896.png "New User")</span><span class="sxs-lookup"><span data-stu-id="cbccb-177">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795896.png "New User")</span></span>
  1. <span data-ttu-id="cbccb-178">Type the password into the related textbox.</span><span class="sxs-lookup"><span data-stu-id="cbccb-178">Type the password into the related textbox.</span></span>
  2. <span data-ttu-id="cbccb-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-179">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="cbccb-180">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="cbccb-180">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="cbccb-181">Assign users</span><span class="sxs-lookup"><span data-stu-id="cbccb-181">Assign users</span></span>
<span data-ttu-id="cbccb-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="cbccb-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="cbccb-183">**To assign users to Sugar CRM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbccb-183">**To assign users to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="cbccb-184">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="cbccb-184">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="cbccb-185">On the **Sugar CRM** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="cbccb-185">On the **Sugar CRM** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="cbccb-186">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795897.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="cbccb-186">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC795897.png "Assign Users")</span></span>

3. <span data-ttu-id="cbccb-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="cbccb-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="cbccb-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="cbccb-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sugarcrm-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="cbccb-189">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cbccb-189">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="cbccb-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cbccb-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
























