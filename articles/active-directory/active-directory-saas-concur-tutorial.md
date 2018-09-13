---
title: 'Tutorial: Azure Active Directory integration with Concur | Microsoft Docs'
description: Learn how to use Concur with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 8bf48b7454e1574612def957924b857eb8477bc5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551491"
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="458bc-103">Tutorial: Azure Active Directory integration with Concur</span><span class="sxs-lookup"><span data-stu-id="458bc-103">Tutorial: Azure Active Directory integration with Concur</span></span>
<span data-ttu-id="458bc-104">The objective of this tutorial is to show the integration of Azure and Concur.</span><span class="sxs-lookup"><span data-stu-id="458bc-104">The objective of this tutorial is to show the integration of Azure and Concur.</span></span>  
<span data-ttu-id="458bc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="458bc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="458bc-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="458bc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="458bc-107">A tenant in Concur</span><span class="sxs-lookup"><span data-stu-id="458bc-107">A tenant in Concur</span></span>

<span data-ttu-id="458bc-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="458bc-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="458bc-109">Enabling the application integration for Concur</span><span class="sxs-lookup"><span data-stu-id="458bc-109">Enabling the application integration for Concur</span></span>
* <span data-ttu-id="458bc-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="458bc-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="458bc-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="458bc-111">Configuring user provisioning</span></span>
* <span data-ttu-id="458bc-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="458bc-112">Assigning users</span></span>

<span data-ttu-id="458bc-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769766.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="458bc-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769766.png "Scenario")</span></span>

>[!NOTE]
><span data-ttu-id="458bc-114">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.</span><span class="sxs-lookup"><span data-stu-id="458bc-114">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.</span></span> 
> 

## <a name="enable-the-application-integration-for-concur"></a><span data-ttu-id="458bc-115">Enable the application integration for Concur</span><span class="sxs-lookup"><span data-stu-id="458bc-115">Enable the application integration for Concur</span></span>
<span data-ttu-id="458bc-116">The objective of this section is to outline how to enable the application integration for Concur.</span><span class="sxs-lookup"><span data-stu-id="458bc-116">The objective of this section is to outline how to enable the application integration for Concur.</span></span>

<span data-ttu-id="458bc-117">**To enable the application integration for Concur, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="458bc-117">**To enable the application integration for Concur, perform the following steps:**</span></span>
1. <span data-ttu-id="458bc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="458bc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
  <span data-ttu-id="458bc-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="458bc-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="458bc-120">From the **Directory** list, select the directory for which want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="458bc-120">From the **Directory** list, select the directory for which want to enable directory integration.</span></span>
3. <span data-ttu-id="458bc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="458bc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
  <span data-ttu-id="458bc-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="458bc-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="458bc-123">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span><span class="sxs-lookup"><span data-stu-id="458bc-123">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
  <span data-ttu-id="458bc-124">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700995.png "What do you want to do?")</span><span class="sxs-lookup"><span data-stu-id="458bc-124">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="458bc-125">In the **search box**, type **Concur**.</span><span class="sxs-lookup"><span data-stu-id="458bc-125">In the **search box**, type **Concur**.</span></span>
   
  <span data-ttu-id="458bc-126">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721727.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="458bc-126">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721727.png "Application Gallery")</span></span>
6. <span data-ttu-id="458bc-127">In the results pane, select **Concur**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="458bc-127">In the results pane, select **Concur**, and then click **Complete** to add the application.</span></span>
   
  <span data-ttu-id="458bc-128">![Concur](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721728.png "Concur")</span><span class="sxs-lookup"><span data-stu-id="458bc-128">![Concur](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721728.png "Concur")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="458bc-129">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="458bc-129">Configure single sign-on</span></span>

<span data-ttu-id="458bc-130">The objective of this section is to outline how to enable users to authenticate to Concur with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="458bc-130">The objective of this section is to outline how to enable users to authenticate to Concur with their account in Azure AD using federation based on the SAML protocol.</span></span>

>[!NOTE]
><span data-ttu-id="458bc-131">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.</span><span class="sxs-lookup"><span data-stu-id="458bc-131">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.</span></span>
> 

<span data-ttu-id="458bc-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="458bc-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="458bc-133">In the Azure classic portal, on the \*\*Concur \*\*application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="458bc-133">In the Azure classic portal, on the \*\*Concur \*\*application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="458bc-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769767.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="458bc-134">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769767.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="458bc-135">On the **How would you like users to sign on to Concur** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="458bc-135">On the **How would you like users to sign on to Concur** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="458bc-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769768.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="458bc-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769768.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="458bc-137">On the **Configure App URL** page, in the **Concur Sign In URL** textbox, type your concur tenant sign-in URL, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="458bc-137">On the **Configure App URL** page, in the **Concur Sign In URL** textbox, type your concur tenant sign-in URL, and then click **Next**:</span></span> 
   
   <span data-ttu-id="458bc-138">![Configure sign in URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769769.png "Configure sign in URL")</span><span class="sxs-lookup"><span data-stu-id="458bc-138">![Configure sign in URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769769.png "Configure sign in URL")</span></span>
4. <span data-ttu-id="458bc-139">On the **Configure single sign-on at Concur** page, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="458bc-139">On the **Configure single sign-on at Concur** page, perform the following steps.</span></span>
   
   <span data-ttu-id="458bc-140">![Configure sign in URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769770.png "Configure sign in URL")</span><span class="sxs-lookup"><span data-stu-id="458bc-140">![Configure sign in URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769770.png "Configure sign in URL")</span></span>
   1. <span data-ttu-id="458bc-141">Click Download the metadata, and then safe the data file to your computer.</span><span class="sxs-lookup"><span data-stu-id="458bc-141">Click Download the metadata, and then safe the data file to your computer.</span></span>
   2. <span data-ttu-id="458bc-142">Contact the Concur support team to configure SSO for your tenant.</span><span class="sxs-lookup"><span data-stu-id="458bc-142">Contact the Concur support team to configure SSO for your tenant.</span></span>
   3. <span data-ttu-id="458bc-143">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="458bc-143">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>  
   
   >[!NOTE]
   ><span data-ttu-id="458bc-144">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.</span><span class="sxs-lookup"><span data-stu-id="458bc-144">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.</span></span> 
   > 

## <a name="configure-user-provisioning"></a><span data-ttu-id="458bc-145">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="458bc-145">Configure user provisioning</span></span>
<span data-ttu-id="458bc-146">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span><span class="sxs-lookup"><span data-stu-id="458bc-146">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="458bc-147">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span><span class="sxs-lookup"><span data-stu-id="458bc-147">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="458bc-148">Don't simply add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span><span class="sxs-lookup"><span data-stu-id="458bc-148">Don't simply add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="458bc-149">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (e.g. enabling apps).</span><span class="sxs-lookup"><span data-stu-id="458bc-149">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (e.g. enabling apps).</span></span> <span data-ttu-id="458bc-150">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span><span class="sxs-lookup"><span data-stu-id="458bc-150">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="458bc-151">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span><span class="sxs-lookup"><span data-stu-id="458bc-151">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="458bc-152">This will assign ownership to the profile.Once the profile(s) is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span><span class="sxs-lookup"><span data-stu-id="458bc-152">This will assign ownership to the profile.Once the profile(s) is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="458bc-153">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span><span class="sxs-lookup"><span data-stu-id="458bc-153">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

1. <span data-ttu-id="458bc-154">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span><span class="sxs-lookup"><span data-stu-id="458bc-154">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="458bc-155">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span><span class="sxs-lookup"><span data-stu-id="458bc-155">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>
2. <span data-ttu-id="458bc-156">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile will not function until the app is enabled with another active WS Admin profile.</span><span class="sxs-lookup"><span data-stu-id="458bc-156">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile will not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="458bc-157">This is why you are supposed to create distinct WS Admin profiles.</span><span class="sxs-lookup"><span data-stu-id="458bc-157">This is why you are supposed to create distinct WS Admin profiles.</span></span>
3. <span data-ttu-id="458bc-158">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated</span><span class="sxs-lookup"><span data-stu-id="458bc-158">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated</span></span>

<span data-ttu-id="458bc-159">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="458bc-159">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="458bc-160">Logon to your **Concur** tenant.</span><span class="sxs-lookup"><span data-stu-id="458bc-160">Logon to your **Concur** tenant.</span></span>
2. <span data-ttu-id="458bc-161">From the **Administration** menu, select **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="458bc-161">From the **Administration** menu, select **Web Services**.</span></span>
   
   <span data-ttu-id="458bc-162">![Concur tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721729.png "Concur tenant")</span><span class="sxs-lookup"><span data-stu-id="458bc-162">![Concur tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721729.png "Concur tenant")</span></span>
3. <span data-ttu-id="458bc-163">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span><span class="sxs-lookup"><span data-stu-id="458bc-163">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
   <span data-ttu-id="458bc-164">![Enable Partner Application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721730.png "Enable Partner Application")</span><span class="sxs-lookup"><span data-stu-id="458bc-164">![Enable Partner Application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721730.png "Enable Partner Application")</span></span>
4. <span data-ttu-id="458bc-165">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="458bc-165">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
   <span data-ttu-id="458bc-166">![Microsoft Azure Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="458bc-166">![Microsoft Azure Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721731.png "Microsoft Azure Active Directory")</span></span>
5. <span data-ttu-id="458bc-167">Click **Yes** to close the **Confirm Action** dialog.</span><span class="sxs-lookup"><span data-stu-id="458bc-167">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
   <span data-ttu-id="458bc-168">![Confirm Action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721732.png "Confirm Action")</span><span class="sxs-lookup"><span data-stu-id="458bc-168">![Confirm Action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721732.png "Confirm Action")</span></span>
6. <span data-ttu-id="458bc-169">In the Azure classic portal, select **Concur** from the applications list to open the **Concur** dialog page.</span><span class="sxs-lookup"><span data-stu-id="458bc-169">In the Azure classic portal, select **Concur** from the applications list to open the **Concur** dialog page.</span></span>
7. <span data-ttu-id="458bc-170">To open the **Configure User Provisioning** dialog page, click **Configure user provisioning**.</span><span class="sxs-lookup"><span data-stu-id="458bc-170">To open the **Configure User Provisioning** dialog page, click **Configure user provisioning**.</span></span>
8. <span data-ttu-id="458bc-171">Enter the user name and the password of your Concur administrator, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="458bc-171">Enter the user name and the password of your Concur administrator, and then click **Next**.</span></span>
9. <span data-ttu-id="458bc-172">To finish the configuration, on the **Confirmation** page, click the **Complete** button.</span><span class="sxs-lookup"><span data-stu-id="458bc-172">To finish the configuration, on the **Confirmation** page, click the **Complete** button.</span></span>

<span data-ttu-id="458bc-173">You can now create a test account, wait for 10 minutes and verify that the account has been synchronized to Concur.</span><span class="sxs-lookup"><span data-stu-id="458bc-173">You can now create a test account, wait for 10 minutes and verify that the account has been synchronized to Concur.</span></span>

## <a name="assign-users"></a><span data-ttu-id="458bc-174">Assign users</span><span class="sxs-lookup"><span data-stu-id="458bc-174">Assign users</span></span>
<span data-ttu-id="458bc-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="458bc-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="458bc-176">**To assign users to Concur, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="458bc-176">**To assign users to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="458bc-177">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="458bc-177">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="458bc-178">On the \*\*Concur \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="458bc-178">On the \*\*Concur \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="458bc-179">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769771.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="458bc-179">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769771.png "Assign users")</span></span>
3. <span data-ttu-id="458bc-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="458bc-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="458bc-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="458bc-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="458bc-182">You should now wait for 10 minutes and verify that the account has been synchronized to Concur.</span><span class="sxs-lookup"><span data-stu-id="458bc-182">You should now wait for 10 minutes and verify that the account has been synchronized to Concur.</span></span>

<span data-ttu-id="458bc-183">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="458bc-183">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="458bc-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="458bc-184">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















