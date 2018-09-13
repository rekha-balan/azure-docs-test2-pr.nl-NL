---
title: 'Tutorial: Azure Active Directory integration with SumoLogic | Microsoft Docs'
description: Learn how to use SumoLogic with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/07/2017
ms.author: jeedes
ms.openlocfilehash: 050ba3fc361bdaca8fb5c809b41675521bc2fa2b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661891"
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="46c00-103">Tutorial: Azure Active Directory Integration with SumoLogic</span><span class="sxs-lookup"><span data-stu-id="46c00-103">Tutorial: Azure Active Directory Integration with SumoLogic</span></span>
<span data-ttu-id="46c00-104">The objective of this tutorial is to show the integration of Azure and SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="46c00-104">The objective of this tutorial is to show the integration of Azure and SumoLogic.</span></span>  

<span data-ttu-id="46c00-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="46c00-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="46c00-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="46c00-106">A valid Azure subscription</span></span>
* <span data-ttu-id="46c00-107">A SumoLogic tenant</span><span class="sxs-lookup"><span data-stu-id="46c00-107">A SumoLogic tenant</span></span>

<span data-ttu-id="46c00-108">After completing this tutorial, the Azure AD users you have assigned to SumoLogicwill be able to single sign into the application at your SumoLogic company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46c00-108">After completing this tutorial, the Azure AD users you have assigned to SumoLogicwill be able to single sign into the application at your SumoLogic company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="46c00-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="46c00-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="46c00-110">Enabling the application integration for SumoLogic</span><span class="sxs-lookup"><span data-stu-id="46c00-110">Enabling the application integration for SumoLogic</span></span>
2. <span data-ttu-id="46c00-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="46c00-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="46c00-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="46c00-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="46c00-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="46c00-113">Assigning users</span></span>

<span data-ttu-id="46c00-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778549.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="46c00-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778549.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-sumologic"></a><span data-ttu-id="46c00-115">Enable the application integration for SumoLogic</span><span class="sxs-lookup"><span data-stu-id="46c00-115">Enable the application integration for SumoLogic</span></span>
<span data-ttu-id="46c00-116">The objective of this section is to outline how to enable the application integration for SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="46c00-116">The objective of this section is to outline how to enable the application integration for SumoLogic.</span></span>

<span data-ttu-id="46c00-117">**To enable the application integration for SumoLogic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46c00-117">**To enable the application integration for SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="46c00-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46c00-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="46c00-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="46c00-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="46c00-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="46c00-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="46c00-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="46c00-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="46c00-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="46c00-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="46c00-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="46c00-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="46c00-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="46c00-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="46c00-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="46c00-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="46c00-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="46c00-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="46c00-127">In the **search box**, type **sumologic**.</span><span class="sxs-lookup"><span data-stu-id="46c00-127">In the **search box**, type **sumologic**.</span></span>
   
    <span data-ttu-id="46c00-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778550.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="46c00-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778550.png "Application gallery")</span></span>

7. <span data-ttu-id="46c00-129">In the results pane, select **SumoLogic**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="46c00-129">In the results pane, select **SumoLogic**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="46c00-130">![SumoLogic](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778551.png "SumoLogic")</span><span class="sxs-lookup"><span data-stu-id="46c00-130">![SumoLogic](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778551.png "SumoLogic")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="46c00-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="46c00-131">Configure single sign-on</span></span>
<span data-ttu-id="46c00-132">The objective of this section is to outline how to enable users to authenticate to SumoLogic with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="46c00-132">The objective of this section is to outline how to enable users to authenticate to SumoLogic with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="46c00-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your SumoLogictenant.</span><span class="sxs-lookup"><span data-stu-id="46c00-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your SumoLogictenant.</span></span>  

<span data-ttu-id="46c00-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="46c00-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="46c00-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46c00-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="46c00-136">In the Azure classic portal, on the **SumoLogic** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="46c00-136">In the Azure classic portal, on the **SumoLogic** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="46c00-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778552.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="46c00-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778552.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="46c00-138">On the **How would you like users to sign on to SumoLogic** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="46c00-138">On the **How would you like users to sign on to SumoLogic** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="46c00-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778553.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="46c00-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778553.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="46c00-140">On the **Configure App URL** page, in the **SumoLogic Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.SumoLogic.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="46c00-140">On the **Configure App URL** page, in the **SumoLogic Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.SumoLogic.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="46c00-141">![Configure aoo URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778554.png "Configure aoo URL")</span><span class="sxs-lookup"><span data-stu-id="46c00-141">![Configure aoo URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778554.png "Configure aoo URL")</span></span>

4. <span data-ttu-id="46c00-142">On the **Configure single sign-on at SumoLogic** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="46c00-142">On the **Configure single sign-on at SumoLogic** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="46c00-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778555.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="46c00-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778555.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="46c00-144">In a different web browser window, log into your SumoLogic company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="46c00-144">In a different web browser window, log into your SumoLogic company site as an administrator.</span></span>

6. <span data-ttu-id="46c00-145">Go to **Manage \> Security**.</span><span class="sxs-lookup"><span data-stu-id="46c00-145">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="46c00-146">![Manage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778556.png "Manage")</span><span class="sxs-lookup"><span data-stu-id="46c00-146">![Manage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778556.png "Manage")</span></span>

7. <span data-ttu-id="46c00-147">Click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="46c00-147">Click **SAML**.</span></span>
   
    <span data-ttu-id="46c00-148">![Global security settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778557.png "Global security settings")</span><span class="sxs-lookup"><span data-stu-id="46c00-148">![Global security settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778557.png "Global security settings")</span></span>

8. <span data-ttu-id="46c00-149">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="46c00-149">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="46c00-150">![Configure SAML 2.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778558.png "Configure SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="46c00-150">![Configure SAML 2.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778558.png "Configure SAML 2.0")</span></span>

9. <span data-ttu-id="46c00-151">On the **Configure SAML 2.0** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46c00-151">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="46c00-152">![Configure SAML 2.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778559.png "Configure SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="46c00-152">![Configure SAML 2.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778559.png "Configure SAML 2.0")</span></span>   
  1. <span data-ttu-id="46c00-153">In the **Configuration Name** textbox, type **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="46c00-153">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 
  2. <span data-ttu-id="46c00-154">Select **Debug Mode**.</span><span class="sxs-lookup"><span data-stu-id="46c00-154">Select **Debug Mode**.</span></span>
  3. <span data-ttu-id="46c00-155">In the Azure classic portal, on the **Configure single sign-on at SumoLogic** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="46c00-155">In the Azure classic portal, on the **Configure single sign-on at SumoLogic** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
  4. <span data-ttu-id="46c00-156">In the Azure classic portal, on the **Configure single sign-on at SumoLogic** dialogue page, copy the **Authentication Request URL** value, and then paste it into the **Authn Request URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="46c00-156">In the Azure classic portal, on the **Configure single sign-on at SumoLogic** dialogue page, copy the **Authentication Request URL** value, and then paste it into the **Authn Request URL** textbox.</span></span>
  5. <span data-ttu-id="46c00-157">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="46c00-157">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
      
     >[!TIP]
     ><span data-ttu-id="46c00-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="46c00-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
     >  

  6. <span data-ttu-id="46c00-159">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="46c00-159">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  7. <span data-ttu-id="46c00-160">As **Email Attribute**, select **Use SAML subject**.</span><span class="sxs-lookup"><span data-stu-id="46c00-160">As **Email Attribute**, select **Use SAML subject**.</span></span>  
  8. <span data-ttu-id="46c00-161">Select **SP initiated Login Configuration**.</span><span class="sxs-lookup"><span data-stu-id="46c00-161">Select **SP initiated Login Configuration**.</span></span>
  9. <span data-ttu-id="46c00-162">In the **Login Path** textbox, type **Azure** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="46c00-162">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

10. <span data-ttu-id="46c00-163">In the Azure classic portal, on the **Configure single sign-on at SumoLogic** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="46c00-163">In the Azure classic portal, on the **Configure single sign-on at SumoLogic** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="46c00-164">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778560.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="46c00-164">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778560.png "Configure single sign-on")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="46c00-165">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="46c00-165">Configure user provisioning</span></span>
<span data-ttu-id="46c00-166">In order to enable Azure AD users to log into SumoLogic, they must be provisioned to SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="46c00-166">In order to enable Azure AD users to log into SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="46c00-167">In the case of SumoLogic, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="46c00-167">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="46c00-168">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46c00-168">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="46c00-169">Log in to your **SumoLogic** tenant.</span><span class="sxs-lookup"><span data-stu-id="46c00-169">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="46c00-170">Go to **Manage \> Users**.</span><span class="sxs-lookup"><span data-stu-id="46c00-170">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="46c00-171">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778561.png "Users")</span><span class="sxs-lookup"><span data-stu-id="46c00-171">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778561.png "Users")</span></span>

3. <span data-ttu-id="46c00-172">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="46c00-172">Click **Add**.</span></span>
   
    <span data-ttu-id="46c00-173">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778562.png "Users")</span><span class="sxs-lookup"><span data-stu-id="46c00-173">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778562.png "Users")</span></span>

4. <span data-ttu-id="46c00-174">On the **New User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46c00-174">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="46c00-175">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778563.png "New User")</span><span class="sxs-lookup"><span data-stu-id="46c00-175">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778563.png "New User")</span></span>  
  1. <span data-ttu-id="46c00-176">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name** and **Email** textboxes.</span><span class="sxs-lookup"><span data-stu-id="46c00-176">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name** and **Email** textboxes.</span></span>
  2. <span data-ttu-id="46c00-177">Select a role.</span><span class="sxs-lookup"><span data-stu-id="46c00-177">Select a role.</span></span>
  3. <span data-ttu-id="46c00-178">As **Status**, select **Active**.</span><span class="sxs-lookup"><span data-stu-id="46c00-178">As **Status**, select **Active**.</span></span>
  4. <span data-ttu-id="46c00-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="46c00-179">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="46c00-180">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="46c00-180">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="46c00-181">Assign users</span><span class="sxs-lookup"><span data-stu-id="46c00-181">Assign users</span></span>
<span data-ttu-id="46c00-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="46c00-182">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="46c00-183">**To assign users to SumoLogic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46c00-183">**To assign users to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="46c00-184">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="46c00-184">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="46c00-185">On the **SumoLogic** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="46c00-185">On the **SumoLogic** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="46c00-186">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778564.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="46c00-186">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC778564.png "Assign users")</span></span>

3. <span data-ttu-id="46c00-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="46c00-187">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="46c00-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="46c00-188">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sumologic-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="46c00-189">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="46c00-189">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="46c00-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46c00-190">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















