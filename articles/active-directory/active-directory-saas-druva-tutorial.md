---
title: 'Tutorial: Azure Active Directory integration integration with Druva | Microsoft Docs'
description: Learn how to use Druva with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f0041f1d81e2dd07511b11dd941ccaaa8fc099e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551944"
---
# <a name="tutorial-azure-active-directory-integration-integration-with-druva"></a><span data-ttu-id="bb539-103">Tutorial: Azure Active Directory integration integration with Druva</span><span class="sxs-lookup"><span data-stu-id="bb539-103">Tutorial: Azure Active Directory integration integration with Druva</span></span>
<span data-ttu-id="bb539-104">The objective of this tutorial is to show the integration of Azure and Druva.</span><span class="sxs-lookup"><span data-stu-id="bb539-104">The objective of this tutorial is to show the integration of Azure and Druva.</span></span>  

<span data-ttu-id="bb539-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="bb539-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="bb539-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="bb539-106">A valid Azure subscription</span></span>
* <span data-ttu-id="bb539-107">A Druva single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bb539-107">A Druva single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="bb539-108">After completing this tutorial, the Azure AD users you have assigned to Druva will be able to single sign into the application at your Druva company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb539-108">After completing this tutorial, the Azure AD users you have assigned to Druva will be able to single sign into the application at your Druva company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="bb539-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bb539-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="bb539-110">Enabling the application integration for Druva</span><span class="sxs-lookup"><span data-stu-id="bb539-110">Enabling the application integration for Druva</span></span>
* <span data-ttu-id="bb539-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="bb539-111">Configuring single sign-on</span></span>
* <span data-ttu-id="bb539-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="bb539-112">Configuring user provisioning</span></span>
* <span data-ttu-id="bb539-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="bb539-113">Assigning users</span></span>

<span data-ttu-id="bb539-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795084.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="bb539-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795084.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-druva"></a><span data-ttu-id="bb539-115">Enable the application integration for Druva</span><span class="sxs-lookup"><span data-stu-id="bb539-115">Enable the application integration for Druva</span></span>
<span data-ttu-id="bb539-116">The objective of this section is to outline how to enable the application integration for Druva.</span><span class="sxs-lookup"><span data-stu-id="bb539-116">The objective of this section is to outline how to enable the application integration for Druva.</span></span>

<span data-ttu-id="bb539-117">**To enable the application integration for Druva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb539-117">**To enable the application integration for Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="bb539-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bb539-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="bb539-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="bb539-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="bb539-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="bb539-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="bb539-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="bb539-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="bb539-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="bb539-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="bb539-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="bb539-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="bb539-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="bb539-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="bb539-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="bb539-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="bb539-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="bb539-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="bb539-127">In the **search box**, type **Druva**.</span><span class="sxs-lookup"><span data-stu-id="bb539-127">In the **search box**, type **Druva**.</span></span>
   
   <span data-ttu-id="bb539-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795085.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="bb539-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795085.png "Application Gallery")</span></span>
7. <span data-ttu-id="bb539-129">In the results pane, select **Druva**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="bb539-129">In the results pane, select **Druva**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="bb539-130">![Druva](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795086.png "Druva")</span><span class="sxs-lookup"><span data-stu-id="bb539-130">![Druva](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795086.png "Druva")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="bb539-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="bb539-131">Configure single sign-on</span></span>

<span data-ttu-id="bb539-132">The objective of this section is to outline how to enable users to authenticate to Druva with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="bb539-132">The objective of this section is to outline how to enable users to authenticate to Druva with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="bb539-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="bb539-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="bb539-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="bb539-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="bb539-135">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="bb539-135">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="bb539-136">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="bb539-136">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="bb539-137">![SAML Token Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795087.png "SAML Token Attributes")</span><span class="sxs-lookup"><span data-stu-id="bb539-137">![SAML Token Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795087.png "SAML Token Attributes")</span></span>

<span data-ttu-id="bb539-138">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb539-138">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="bb539-139">In the Azure classic portal, on the **Druva** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="bb539-139">In the Azure classic portal, on the **Druva** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="bb539-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795027.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bb539-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795027.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="bb539-141">On the **How would you like users to sign on to Druva** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bb539-141">On the **How would you like users to sign on to Druva** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="bb539-142">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795088.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bb539-142">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795088.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="bb539-143">On the **Configure App URL** page, in the **Druva Sign On URL** textbox, type the URL used by your users to sign on to your Druva application (e.g.: "*https://cloud.druva.com/home/*”), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bb539-143">On the **Configure App URL** page, in the **Druva Sign On URL** textbox, type the URL used by your users to sign on to your Druva application (e.g.: "*https://cloud.druva.com/home/*”), and then click **Next**.</span></span>
   
   <span data-ttu-id="bb539-144">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795089.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="bb539-144">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795089.png "Configure App URL")</span></span>
4. <span data-ttu-id="bb539-145">On the **Configure single sign-on at Druva** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="bb539-145">On the **Configure single sign-on at Druva** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="bb539-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795090.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bb539-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795090.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="bb539-147">In a different web browser window, log into your Druva company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bb539-147">In a different web browser window, log into your Druva company site as an administrator.</span></span>
6. <span data-ttu-id="bb539-148">Go to **Manage \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="bb539-148">Go to **Manage \> Settings**.</span></span>
   
   <span data-ttu-id="bb539-149">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795091.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="bb539-149">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795091.png "Settings")</span></span>
7. <span data-ttu-id="bb539-150">On the Single Sign-On Settings dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb539-150">On the Single Sign-On Settings dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="bb539-151">![Singl Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795092.png "Singl Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="bb539-151">![Singl Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795092.png "Singl Sign-On Settings")</span></span>   
   1. <span data-ttu-id="bb539-152">In the Azure classic portal, on the **Configure single sign-on at Druva** dialog page, copy the **Remote Login URL** value, and then paste it into the **ID Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="bb539-152">In the Azure classic portal, on the **Configure single sign-on at Druva** dialog page, copy the **Remote Login URL** value, and then paste it into the **ID Provider Login URL** textbox.</span></span>
   2. <span data-ttu-id="bb539-153">In the Azure classic portal, on the **Configure single sign-on at Druva** dialog page, copy the **Remote Logout URL** value, and then paste it into the **ID Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="bb539-153">In the Azure classic portal, on the **Configure single sign-on at Druva** dialog page, copy the **Remote Logout URL** value, and then paste it into the **ID Provider Logout URL** textbox.</span></span>
   3. <span data-ttu-id="bb539-154">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="bb539-154">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
     >[!TIP]
     ><span data-ttu-id="bb539-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="bb539-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
     > 
   4. <span data-ttu-id="bb539-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="bb539-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
   5. <span data-ttu-id="bb539-157">To open the **Settings** page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bb539-157">To open the **Settings** page, click **Save**.</span></span>
8. <span data-ttu-id="bb539-158">On the **Settings** page, click **Generate SSO Token**.</span><span class="sxs-lookup"><span data-stu-id="bb539-158">On the **Settings** page, click **Generate SSO Token**.</span></span>
   
   <span data-ttu-id="bb539-159">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795093.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="bb539-159">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795093.png "Settings")</span></span>
9. <span data-ttu-id="bb539-160">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb539-160">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="bb539-161">![SSO Token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795094.png "SSO Token")</span><span class="sxs-lookup"><span data-stu-id="bb539-161">![SSO Token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795094.png "SSO Token")</span></span>
   1. <span data-ttu-id="bb539-162">Click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="bb539-162">Click **Copy**.</span></span>
   2. <span data-ttu-id="bb539-163">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="bb539-163">Click **Close**.</span></span>
10. <span data-ttu-id="bb539-164">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="bb539-164">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="bb539-165">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795095.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bb539-165">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795095.png "Configure Single Sign-On")</span></span>
11. <span data-ttu-id="bb539-166">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="bb539-166">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
    
    <span data-ttu-id="bb539-167">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795096.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="bb539-167">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795096.png "Attributes")</span></span>
12. <span data-ttu-id="bb539-168">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb539-168">To add the required attribute mappings, perform the following steps:</span></span>
    
   | <span data-ttu-id="bb539-169">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="bb539-169">Attribute Name</span></span> | <span data-ttu-id="bb539-170">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="bb539-170">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="bb539-171">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="bb539-171">insync\_auth\_token</span></span> |<span data-ttu-id="bb539-172"><*clipboard value*></span><span class="sxs-lookup"><span data-stu-id="bb539-172"><*clipboard value*></span></span> |
    
   1. <span data-ttu-id="bb539-173">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="bb539-173">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="bb539-174">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="bb539-174">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="bb539-175">In the **Attribute Value** textbox, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="bb539-175">In the **Attribute Value** textbox, type the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="bb539-176">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bb539-176">Click **Complete**.</span></span>
13. <span data-ttu-id="bb539-177">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="bb539-177">Click **Apply Changes**.</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="bb539-178">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="bb539-178">Configure user provisioning</span></span>

<span data-ttu-id="bb539-179">In order to enable Azure AD users to log into Druva, they must be provisioned into Druva.</span><span class="sxs-lookup"><span data-stu-id="bb539-179">In order to enable Azure AD users to log into Druva, they must be provisioned into Druva.</span></span> 

* <span data-ttu-id="bb539-180">In the case of Druva, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="bb539-180">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="bb539-181">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb539-181">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="bb539-182">Log in to your **Druva** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="bb539-182">Log in to your **Druva** company site as administrator.</span></span>
2. <span data-ttu-id="bb539-183">Go to **Manage \> Users**.</span><span class="sxs-lookup"><span data-stu-id="bb539-183">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="bb539-184">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795097.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="bb539-184">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795097.png "Manage Users")</span></span>
3. <span data-ttu-id="bb539-185">Click **Create New**.</span><span class="sxs-lookup"><span data-stu-id="bb539-185">Click **Create New**.</span></span>
   
   <span data-ttu-id="bb539-186">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795098.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="bb539-186">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795098.png "Manage Users")</span></span>
4. <span data-ttu-id="bb539-187">On the Create New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb539-187">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="bb539-188">![Create NewUser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795099.png "Create NewUser")</span><span class="sxs-lookup"><span data-stu-id="bb539-188">![Create NewUser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795099.png "Create NewUser")</span></span>
   
   1. <span data-ttu-id="bb539-189">Type the email address and the name of a valid Azure Active Directory user account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="bb539-189">Type the email address and the name of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="bb539-190">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="bb539-190">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="bb539-191">You can use any other Druva user account creation tools or APIs provided by Druva to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="bb539-191">You can use any other Druva user account creation tools or APIs provided by Druva to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="bb539-192">Assign users</span><span class="sxs-lookup"><span data-stu-id="bb539-192">Assign users</span></span>
<span data-ttu-id="bb539-193">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="bb539-193">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="bb539-194">**To assign users to Druva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb539-194">**To assign users to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="bb539-195">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="bb539-195">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="bb539-196">On the \*\*Druva \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="bb539-196">On the \*\*Druva \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="bb539-197">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795100.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="bb539-197">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC795100.png "Assign Users")</span></span>
3. <span data-ttu-id="bb539-198">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="bb539-198">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="bb539-199">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="bb539-199">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-druva-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="bb539-200">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bb539-200">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="bb539-201">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb539-201">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
























