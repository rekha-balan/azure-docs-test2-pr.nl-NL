---
title: 'Tutorial: Azure Active Directory integration with SpringCM | Microsoft Docs'
description: Learn how to use Spring CM with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/10/2017
ms.author: jeedes
ms.openlocfilehash: ccb6ae4291aa0813775d6adfe342b47673a67f1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553154"
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="56d9c-103">Tutorial: Azure Active Directory integration with SpringCM</span><span class="sxs-lookup"><span data-stu-id="56d9c-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>
<span data-ttu-id="56d9c-104">The objective of this tutorial is to show how to set up single sign-on (SSO) between Azure Active Directory and SpringCM.</span><span class="sxs-lookup"><span data-stu-id="56d9c-104">The objective of this tutorial is to show how to set up single sign-on (SSO) between Azure Active Directory and SpringCM.</span></span>

<span data-ttu-id="56d9c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="56d9c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="56d9c-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="56d9c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="56d9c-107">A SpringCM single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="56d9c-107">A SpringCM single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="56d9c-108">After completing this tutorial, the Azure Active Directory users you have assigned to SpringCM will be able to SSO using the AAD Access Panel.</span><span class="sxs-lookup"><span data-stu-id="56d9c-108">After completing this tutorial, the Azure Active Directory users you have assigned to SpringCM will be able to SSO using the AAD Access Panel.</span></span>

1. <span data-ttu-id="56d9c-109">Enabling the application integration for SpringCM</span><span class="sxs-lookup"><span data-stu-id="56d9c-109">Enabling the application integration for SpringCM</span></span>
2. <span data-ttu-id="56d9c-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="56d9c-110">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="56d9c-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="56d9c-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="56d9c-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="56d9c-112">Assigning users</span></span>

<span data-ttu-id="56d9c-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797044.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="56d9c-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797044.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-springcm"></a><span data-ttu-id="56d9c-114">Enabling the application integration for SpringCM</span><span class="sxs-lookup"><span data-stu-id="56d9c-114">Enabling the application integration for SpringCM</span></span>
<span data-ttu-id="56d9c-115">The objective of this section is to outline how to enable the application integration for SpringCM.</span><span class="sxs-lookup"><span data-stu-id="56d9c-115">The objective of this section is to outline how to enable the application integration for SpringCM.</span></span>

<span data-ttu-id="56d9c-116">**To enable the application integration for SpringCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56d9c-116">**To enable the application integration for SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="56d9c-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="56d9c-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="56d9c-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="56d9c-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="56d9c-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="56d9c-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="56d9c-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="56d9c-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="56d9c-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="56d9c-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="56d9c-122">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="56d9c-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="56d9c-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="56d9c-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="56d9c-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="56d9c-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="56d9c-126">In the **search box**, type **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-126">In the **search box**, type **SpringCM**.</span></span>
   
    <span data-ttu-id="56d9c-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797045.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="56d9c-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797045.png "Application Gallery")</span></span>

7. <span data-ttu-id="56d9c-128">In the results pane, select **SpringCM**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="56d9c-128">In the results pane, select **SpringCM**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="56d9c-129">![SpringCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797046.png "SpringCM")</span><span class="sxs-lookup"><span data-stu-id="56d9c-129">![SpringCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797046.png "SpringCM")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="56d9c-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="56d9c-130">Configure single sign-on</span></span>
<span data-ttu-id="56d9c-131">This section outlines how to enable users to authenticate to SpringCM with their account in Azure Active Directory, using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="56d9c-131">This section outlines how to enable users to authenticate to SpringCM with their account in Azure Active Directory, using federation based on the SAML protocol.</span></span>

<span data-ttu-id="56d9c-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56d9c-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="56d9c-133">In the Azure classic portal, on the **SpringCM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="56d9c-133">In the Azure classic portal, on the **SpringCM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="56d9c-134">![Configure single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797047.png "Configure single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="56d9c-134">![Configure single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797047.png "Configure single Sign-On")</span></span>

2. <span data-ttu-id="56d9c-135">On the **How would you like users to sign on to SpringCM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-135">On the **How would you like users to sign on to SpringCM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="56d9c-136">![Configure single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797048.png "Configure single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="56d9c-136">![Configure single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797048.png "Configure single Sign-On")</span></span>

3. <span data-ttu-id="56d9c-137">On the **Configure App URL** page, in the **SpringCM Sign On URL** textbox, type the URL used by your users to sign on to your SpringCM application, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-137">On the **Configure App URL** page, in the **SpringCM Sign On URL** textbox, type the URL used by your users to sign on to your SpringCM application, and then click **Next**.</span></span> 
   
    <span data-ttu-id="56d9c-138">The app URL is your SpringCM tenant URL (e.g.: *https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=16826*):</span><span class="sxs-lookup"><span data-stu-id="56d9c-138">The app URL is your SpringCM tenant URL (e.g.: *https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=16826*):</span></span>
   
    <span data-ttu-id="56d9c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797049.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="56d9c-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797049.png "Configure App URL")</span></span>

4. <span data-ttu-id="56d9c-140">On the **Configure single sign-on at SpringCM** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span><span class="sxs-lookup"><span data-stu-id="56d9c-140">On the **Configure single sign-on at SpringCM** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.</span></span>
   
    <span data-ttu-id="56d9c-141">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797050.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="56d9c-141">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797050.png "Configure Single SignOn")</span></span>

5. <span data-ttu-id="56d9c-142">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="56d9c-142">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

6. <span data-ttu-id="56d9c-143">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-143">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="56d9c-144">![SAML SSO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="56d9c-144">![SAML SSO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797051.png "SAML SSO")</span></span>

7. <span data-ttu-id="56d9c-145">In the Identity Provider Configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56d9c-145">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="56d9c-146">![Identity Provider Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797052.png "Identity Provider Configuration")</span><span class="sxs-lookup"><span data-stu-id="56d9c-146">![Identity Provider Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797052.png "Identity Provider Configuration")</span></span>   
  1. <span data-ttu-id="56d9c-147">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-147">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
  2. <span data-ttu-id="56d9c-148">In the Azure classic portal, on the **Configure single sign-on at SpringCM** page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="56d9c-148">In the Azure classic portal, on the **Configure single sign-on at SpringCM** page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
  3. <span data-ttu-id="56d9c-149">In the Azure classic portal, on the **Configure single sign-on at SpringCM** page, copy the **Singel Sign-On Service URL** value, and then paste it into the **Service Provider (SP) Initiated Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="56d9c-149">In the Azure classic portal, on the **Configure single sign-on at SpringCM** page, copy the **Singel Sign-On Service URL** value, and then paste it into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
  4. <span data-ttu-id="56d9c-150">As **SAML Enabled**, select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-150">As **SAML Enabled**, select **Enable**.</span></span>
  5. <span data-ttu-id="56d9c-151">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-151">Click **Save**.</span></span>

8. <span data-ttu-id="56d9c-152">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="56d9c-152">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="56d9c-153">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797053.png "Configure Single SignOn")</span><span class="sxs-lookup"><span data-stu-id="56d9c-153">![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797053.png "Configure Single SignOn")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="56d9c-154">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="56d9c-154">Configure user provisioning</span></span>
<span data-ttu-id="56d9c-155">In order to enable Azure Active Directory users to log into SpringCM, they must be provisioned into SpringCM.</span><span class="sxs-lookup"><span data-stu-id="56d9c-155">In order to enable Azure Active Directory users to log into SpringCM, they must be provisioned into SpringCM.</span></span>  

<span data-ttu-id="56d9c-156">In the case of SpringCM, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="56d9c-156">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="56d9c-157">For more details, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="56d9c-157">For more details, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 
> 

<span data-ttu-id="56d9c-158">**To provision a user account to SpringCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56d9c-158">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="56d9c-159">Log in to your **SpringCM** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="56d9c-159">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="56d9c-160">Click **GOTO**, and then click **Address Book**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-160">Click **GOTO**, and then click **Address Book**.</span></span>
   
    <span data-ttu-id="56d9c-161">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797054.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="56d9c-161">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797054.png "Create User")</span></span>

3. <span data-ttu-id="56d9c-162">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-162">Click **Create User**.</span></span>

4. <span data-ttu-id="56d9c-163">Select a **User Role**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-163">Select a **User Role**.</span></span>

5. <span data-ttu-id="56d9c-164">Select **Send Activation Email**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-164">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="56d9c-165">Type the first name, last name and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="56d9c-165">Type the first name, last name and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="56d9c-166">Add the user to a **Security group**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-166">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="56d9c-167">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-167">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="56d9c-168">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="56d9c-168">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

## <a name="assign-users"></a><span data-ttu-id="56d9c-169">Assign users</span><span class="sxs-lookup"><span data-stu-id="56d9c-169">Assign users</span></span>
<span data-ttu-id="56d9c-170">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="56d9c-170">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="56d9c-171">**To assign users to SpringCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56d9c-171">**To assign users to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="56d9c-172">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="56d9c-172">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="56d9c-173">On the **SpringCM** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="56d9c-173">On the **SpringCM** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="56d9c-174">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797055.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="56d9c-174">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797055.png "Assign Users")</span></span>

3. <span data-ttu-id="56d9c-175">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="56d9c-175">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="56d9c-176">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="56d9c-176">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="56d9c-177">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="56d9c-177">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="56d9c-178">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="56d9c-178">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















