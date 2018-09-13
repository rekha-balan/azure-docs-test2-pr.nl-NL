---
title: 'Tutorial: Azure Active Directory integration with LogicMonitor | Microsoft Docs'
description: Learn how to use LogicMonitor with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/22/2017
ms.author: jeedes
ms.openlocfilehash: 0c5b3af8d1b722b83a48adafbd1d7bab41b274b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554427"
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="ce27a-103">Tutorial: Azure Active Directory integration with LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="ce27a-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>
<span data-ttu-id="ce27a-104">The objective of this tutorial is to show the integration of Azure and LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="ce27a-104">The objective of this tutorial is to show the integration of Azure and LogicMonitor.</span></span>  

<span data-ttu-id="ce27a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="ce27a-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ce27a-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="ce27a-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ce27a-107">A LogicMonitor tenant</span><span class="sxs-lookup"><span data-stu-id="ce27a-107">A LogicMonitor tenant</span></span>

<span data-ttu-id="ce27a-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ce27a-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="ce27a-109">Enabling the application integration for LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="ce27a-109">Enabling the application integration for LogicMonitor</span></span>
2. <span data-ttu-id="ce27a-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="ce27a-110">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="ce27a-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="ce27a-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="ce27a-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="ce27a-112">Assigning users</span></span>

<span data-ttu-id="ce27a-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790045.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="ce27a-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790045.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-logicmonitor"></a><span data-ttu-id="ce27a-114">Enable the application integration for LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="ce27a-114">Enable the application integration for LogicMonitor</span></span>
<span data-ttu-id="ce27a-115">The objective of this section is to outline how to enable the application integration for LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="ce27a-115">The objective of this section is to outline how to enable the application integration for LogicMonitor.</span></span>

<span data-ttu-id="ce27a-116">**To enable the application integration for LogicMonitor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce27a-116">**To enable the application integration for LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="ce27a-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ce27a-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ce27a-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ce27a-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ce27a-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ce27a-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ce27a-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ce27a-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="ce27a-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ce27a-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ce27a-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ce27a-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="ce27a-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ce27a-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ce27a-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="ce27a-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ce27a-126">In the **search box**, type **logicmonitor**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-126">In the **search box**, type **logicmonitor**.</span></span>
   
   <span data-ttu-id="ce27a-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790046.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="ce27a-127">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790046.png "Application Gallery")</span></span>
7. <span data-ttu-id="ce27a-128">In the results pane, select **LogicMonitor**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ce27a-128">In the results pane, select **LogicMonitor**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ce27a-129">![LogicMonitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790047.png "LogicMonitor")</span><span class="sxs-lookup"><span data-stu-id="ce27a-129">![LogicMonitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790047.png "LogicMonitor")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ce27a-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="ce27a-130">Configure single sign-on</span></span>

<span data-ttu-id="ce27a-131">The objective of this section is to outline how to enable users to authenticate to LogicMonitor with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="ce27a-131">The objective of this section is to outline how to enable users to authenticate to LogicMonitor with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="ce27a-132">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce27a-132">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ce27a-133">In the Azure classic portal, on the \*\*LogicMonitor \*\*application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ce27a-133">In the Azure classic portal, on the \*\*LogicMonitor \*\*application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="ce27a-134">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790048.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ce27a-134">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790048.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="ce27a-135">On the **How would you like users to sign on to LogicMonitor** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-135">On the **How would you like users to sign on to LogicMonitor** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ce27a-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790049.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ce27a-136">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790049.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="ce27a-137">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL used by your users to sign on to LogicMonitor \(e,g,: "*http://company.logicmonitor.com*"\), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-137">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL used by your users to sign on to LogicMonitor \(e,g,: "*http://company.logicmonitor.com*"\), and then click **Next**.</span></span>
   
   <span data-ttu-id="ce27a-138">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790050.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="ce27a-138">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790050.png "Configure App URL")</span></span>
4. <span data-ttu-id="ce27a-139">On the **Configure single sign-on at LogicMonitor** page, click **Download metadata**, and then save it on your computer.</span><span class="sxs-lookup"><span data-stu-id="ce27a-139">On the **Configure single sign-on at LogicMonitor** page, click **Download metadata**, and then save it on your computer.</span></span>
   
   <span data-ttu-id="ce27a-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790051.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ce27a-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790051.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="ce27a-141">Log in to your **LogicMonitor** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ce27a-141">Log in to your **LogicMonitor** company site as an administrator.</span></span>
6. <span data-ttu-id="ce27a-142">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-142">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="ce27a-143">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790052.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="ce27a-143">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790052.png "Settings")</span></span>
7. <span data-ttu-id="ce27a-144">In the navigation bat on the left side, click **Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="ce27a-144">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="ce27a-145">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790053.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ce27a-145">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790053.png "Single Sign-On")</span></span>
8. <span data-ttu-id="ce27a-146">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ce27a-146">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ce27a-147">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790054.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="ce27a-147">![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790054.png "Single Sign-On Settings")</span></span>
   
   1. <span data-ttu-id="ce27a-148">Select **Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-148">Select **Enable Single Sign-on**.</span></span>
   2. <span data-ttu-id="ce27a-149">As **Default Role Assignment**, select **readonly**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-149">As **Default Role Assignment**, select **readonly**.</span></span>
   3. <span data-ttu-id="ce27a-150">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="ce27a-150">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   4. <span data-ttu-id="ce27a-151">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-151">Click **Save Changes**.</span></span>
9. <span data-ttu-id="ce27a-152">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ce27a-152">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="ce27a-153">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790055.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ce27a-153">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790055.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="ce27a-154">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="ce27a-154">Configure user provisioning</span></span>

<span data-ttu-id="ce27a-155">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span><span class="sxs-lookup"><span data-stu-id="ce27a-155">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="ce27a-156">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce27a-156">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ce27a-157">Log in to your LogicMonitor company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ce27a-157">Log in to your LogicMonitor company site as an administrator.</span></span>
2. <span data-ttu-id="ce27a-158">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-158">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="ce27a-159">![Roles and Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790056.png "Roles and Users")</span><span class="sxs-lookup"><span data-stu-id="ce27a-159">![Roles and Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790056.png "Roles and Users")</span></span>
3. <span data-ttu-id="ce27a-160">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-160">Click **Add**.</span></span>
4. <span data-ttu-id="ce27a-161">In the **Add an account** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ce27a-161">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ce27a-162">![Add an account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790057.png "Add an account")</span><span class="sxs-lookup"><span data-stu-id="ce27a-162">![Add an account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790057.png "Add an account")</span></span>
   
   1. <span data-ttu-id="ce27a-163">Type the **Username**, **Email**, **Password** and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="ce27a-163">Type the **Username**, **Email**, **Password** and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="ce27a-164">Select **Roles**, **View Permissions** and the **Status**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-164">Select **Roles**, **View Permissions** and the **Status**.</span></span>
   3. <span data-ttu-id="ce27a-165">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-165">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="ce27a-166">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="ce27a-166">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="ce27a-167">Assign users</span><span class="sxs-lookup"><span data-stu-id="ce27a-167">Assign users</span></span>
<span data-ttu-id="ce27a-168">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="ce27a-168">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ce27a-169">**To assign users to LogicMonitor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce27a-169">**To assign users to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="ce27a-170">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="ce27a-170">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ce27a-171">On the **LogicMonitor** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-171">On the **LogicMonitor** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ce27a-172">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790058.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="ce27a-172">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC790058.png "Assign Users")</span></span>
3. <span data-ttu-id="ce27a-173">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="ce27a-173">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ce27a-174">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="ce27a-174">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-logicmonitor-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ce27a-175">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ce27a-175">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ce27a-176">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce27a-176">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















