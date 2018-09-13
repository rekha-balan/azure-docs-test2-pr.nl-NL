---
title: 'Tutorial: Azure Active Directory integration with InsideView | Microsoft Docs'
description: Learn how to use InsideView with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 10934b34a9884a9c71e33894ec1eff9de0b07d4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552703"
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="532ba-103">Tutorial: Azure Active Directory integration with InsideView</span><span class="sxs-lookup"><span data-stu-id="532ba-103">Tutorial: Azure Active Directory integration with InsideView</span></span>
<span data-ttu-id="532ba-104">The objective of this tutorial is to show the integration of Azure and InsideView.</span><span class="sxs-lookup"><span data-stu-id="532ba-104">The objective of this tutorial is to show the integration of Azure and InsideView.</span></span>  
<span data-ttu-id="532ba-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="532ba-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="532ba-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="532ba-106">A valid Azure subscription</span></span>
* <span data-ttu-id="532ba-107">A InsideView tenant</span><span class="sxs-lookup"><span data-stu-id="532ba-107">A InsideView tenant</span></span>

<span data-ttu-id="532ba-108">After completing this tutorial, the Azure AD users you have assigned to InsideView will be able to single sign into the application at your InsideView company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="532ba-108">After completing this tutorial, the Azure AD users you have assigned to InsideView will be able to single sign into the application at your InsideView company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="532ba-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="532ba-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="532ba-110">Enabling the application integration for InsideView</span><span class="sxs-lookup"><span data-stu-id="532ba-110">Enabling the application integration for InsideView</span></span>
* <span data-ttu-id="532ba-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="532ba-111">Configuring single sign-on</span></span>
* <span data-ttu-id="532ba-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="532ba-112">Configuring user provisioning</span></span>
* <span data-ttu-id="532ba-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="532ba-113">Assigning users</span></span>

<span data-ttu-id="532ba-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794128.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="532ba-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794128.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-insideview"></a><span data-ttu-id="532ba-115">Enable the application integration for InsideView</span><span class="sxs-lookup"><span data-stu-id="532ba-115">Enable the application integration for InsideView</span></span>
<span data-ttu-id="532ba-116">The objective of this section is to outline how to enable the application integration for InsideView.</span><span class="sxs-lookup"><span data-stu-id="532ba-116">The objective of this section is to outline how to enable the application integration for InsideView.</span></span>

<span data-ttu-id="532ba-117">**To enable the application integration for InsideView, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="532ba-117">**To enable the application integration for InsideView, perform the following steps:**</span></span>
 
1. <span data-ttu-id="532ba-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="532ba-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="532ba-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="532ba-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="532ba-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="532ba-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="532ba-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="532ba-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="532ba-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="532ba-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="532ba-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="532ba-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="532ba-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="532ba-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="532ba-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="532ba-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="532ba-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="532ba-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="532ba-127">In the **search box**, type **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="532ba-127">In the **search box**, type **InsideView**.</span></span>
   
   <span data-ttu-id="532ba-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794129.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="532ba-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794129.png "Application Gallery")</span></span>
7. <span data-ttu-id="532ba-129">In the results pane, select **InsideView**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="532ba-129">In the results pane, select **InsideView**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="532ba-130">![InsideView](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794130.png "InsideView")</span><span class="sxs-lookup"><span data-stu-id="532ba-130">![InsideView](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794130.png "InsideView")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="532ba-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="532ba-131">Configure single sign-on</span></span>

<span data-ttu-id="532ba-132">The objective of this section is to outline how to enable users to authenticate to InsideView with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="532ba-132">The objective of this section is to outline how to enable users to authenticate to InsideView with their account in Azure AD using federation based on the SAML protocol.</span></span>  
 
<span data-ttu-id="532ba-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="532ba-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="532ba-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="532ba-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="532ba-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="532ba-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="532ba-136">In the Azure classic portal, on the **InsideView** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="532ba-136">In the Azure classic portal, on the **InsideView** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="532ba-137">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794131.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="532ba-137">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794131.png "Configure Single SignOn")</span></span>
2. <span data-ttu-id="532ba-138">On the **How would you like users to sign on to InsideView** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="532ba-138">On the **How would you like users to sign on to InsideView** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="532ba-139">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794132.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="532ba-139">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794132.png "Configure Single SignOn")</span></span>
3. <span data-ttu-id="532ba-140">On the **Configure App URL** page, in the **InsideView Reply URL** textbox, type your InsideView SSO URL (e.g.: `https://my.insideview.com/iv/<STS Name>/login.iv`), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="532ba-140">On the **Configure App URL** page, in the **InsideView Reply URL** textbox, type your InsideView SSO URL (e.g.: `https://my.insideview.com/iv/<STS Name>/login.iv`), and then click **Next**.</span></span>
   
   <span data-ttu-id="532ba-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794133.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="532ba-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794133.png "Configure App URL")</span></span>
4. <span data-ttu-id="532ba-142">On the **Configure single sign-on at InsideView** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="532ba-142">On the **Configure single sign-on at InsideView** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="532ba-143">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794134.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="532ba-143">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794134.png "Configure Single SignOn")</span></span>
5. <span data-ttu-id="532ba-144">In a different web browser window, log into your InsideView company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="532ba-144">In a different web browser window, log into your InsideView company site as an administrator.</span></span>
6. <span data-ttu-id="532ba-145">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span><span class="sxs-lookup"><span data-stu-id="532ba-145">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="532ba-146">![SAML Single Sign On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794135.png "SAML Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="532ba-146">![SAML Single Sign On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794135.png "SAML Single Sign On Settings")</span></span>
7. <span data-ttu-id="532ba-147">In the **Add a New SAML** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="532ba-147">In the **Add a New SAML** section, perform the following steps:</span></span>
   
   <span data-ttu-id="532ba-148">![Add a New SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794136.png "Add a New SAML")</span><span class="sxs-lookup"><span data-stu-id="532ba-148">![Add a New SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794136.png "Add a New SAML")</span></span>
   
   1. <span data-ttu-id="532ba-149">In the **STS Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="532ba-149">In the **STS Name** textbox, type a name for your configuration.</span></span>
   2. <span data-ttu-id="532ba-150">In the Azure classic portal, on the **Configure single sign-on at InsideView** dialog page, copy the **Service Provider (SP) Initiated Endpoint** value, and then paste it into the **SamlP/WS-Fed Unsolicated EndPoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="532ba-150">In the Azure classic portal, on the **Configure single sign-on at InsideView** dialog page, copy the **Service Provider (SP) Initiated Endpoint** value, and then paste it into the **SamlP/WS-Fed Unsolicated EndPoint** textbox.</span></span>
   3. <span data-ttu-id="532ba-151">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="532ba-151">Create a **base-64 encoded** file from your downloaded certificate.</span></span>      

     >[!TIP]
     ><span data-ttu-id="532ba-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="532ba-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
     >
   4. <span data-ttu-id="532ba-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="532ba-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox</span></span>
   5. <span data-ttu-id="532ba-154">Complete the following:</span><span class="sxs-lookup"><span data-stu-id="532ba-154">Complete the following:</span></span>
    * <span data-ttu-id="532ba-155">In the **Crm User Id Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="532ba-155">In the **Crm User Id Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
    * <span data-ttu-id="532ba-156">In the **Crm Email Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="532ba-156">In the **Crm Email Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
    * <span data-ttu-id="532ba-157">In the **Crm First Name Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="532ba-157">In the **Crm First Name Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
    * <span data-ttu-id="532ba-158">In the **Crm lastName Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="532ba-158">In the **Crm lastName Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>
   9. <span data-ttu-id="532ba-159">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="532ba-159">Click **Save**.</span></span>
8. <span data-ttu-id="532ba-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="532ba-160">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="532ba-161">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794137.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="532ba-161">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794137.png "Configure Single SignOn")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="532ba-162">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="532ba-162">Configure user provisioning</span></span>

<span data-ttu-id="532ba-163">In order to enable Azure AD users to log into InsideView, they must be provisioned into InsideView.</span><span class="sxs-lookup"><span data-stu-id="532ba-163">In order to enable Azure AD users to log into InsideView, they must be provisioned into InsideView.</span></span> <span data-ttu-id="532ba-164">In the case of InsideView, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="532ba-164">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="532ba-165">To get users or contacts created in InsideView, contact your customer success manager or send email to **support@insideview.com**</span><span class="sxs-lookup"><span data-stu-id="532ba-165">To get users or contacts created in InsideView, contact your customer success manager or send email to **support@insideview.com**</span></span>

>[!NOTE]
><span data-ttu-id="532ba-166">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="532ba-166">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="532ba-167">Assign users</span><span class="sxs-lookup"><span data-stu-id="532ba-167">Assign users</span></span>
<span data-ttu-id="532ba-168">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="532ba-168">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="532ba-169">**To assign users to InsideView, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="532ba-169">**To assign users to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="532ba-170">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="532ba-170">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="532ba-171">On the **InsideView** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="532ba-171">On the **InsideView** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="532ba-172">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794138.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="532ba-172">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794138.png "Assign Users")</span></span>
3. <span data-ttu-id="532ba-173">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="532ba-173">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="532ba-174">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="532ba-174">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="532ba-175">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="532ba-175">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="532ba-176">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="532ba-176">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















