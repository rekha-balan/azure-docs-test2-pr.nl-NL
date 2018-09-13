---
title: 'Tutorial: Azure Active Directory integration with TeamSeer | Microsoft Docs'
description: Learn how to use TeamSeer with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 2b2dc7d090293ebe9064c3eb9cb3c40bbf42bcd2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556676"
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="26531-103">Tutorial: Azure Active Directory integration with TeamSeer</span><span class="sxs-lookup"><span data-stu-id="26531-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>
<span data-ttu-id="26531-104">The objective of this tutorial is to show the integration of Azure and TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="26531-104">The objective of this tutorial is to show the integration of Azure and TeamSeer.</span></span>  
<span data-ttu-id="26531-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="26531-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="26531-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="26531-106">A valid Azure subscription</span></span>
* <span data-ttu-id="26531-107">A TeamSeer tenant</span><span class="sxs-lookup"><span data-stu-id="26531-107">A TeamSeer tenant</span></span>

<span data-ttu-id="26531-108">After completing this tutorial, the Azure AD users you have assigned to TeamSeer will be able to single sign into the application at your TeamSeer company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26531-108">After completing this tutorial, the Azure AD users you have assigned to TeamSeer will be able to single sign into the application at your TeamSeer company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="26531-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="26531-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="26531-110">Enabling the application integration for TeamSeer</span><span class="sxs-lookup"><span data-stu-id="26531-110">Enabling the application integration for TeamSeer</span></span>
2. <span data-ttu-id="26531-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="26531-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="26531-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="26531-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="26531-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="26531-113">Assigning users</span></span>

<span data-ttu-id="26531-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789618.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="26531-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789618.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-teamseer"></a><span data-ttu-id="26531-115">Enable the application integration for TeamSeer</span><span class="sxs-lookup"><span data-stu-id="26531-115">Enable the application integration for TeamSeer</span></span>
<span data-ttu-id="26531-116">The objective of this section is to outline how to enable the application integration for TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="26531-116">The objective of this section is to outline how to enable the application integration for TeamSeer.</span></span>

<span data-ttu-id="26531-117">**To enable the application integration for TeamSeer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26531-117">**To enable the application integration for TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="26531-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26531-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="26531-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="26531-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="26531-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="26531-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="26531-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="26531-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="26531-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="26531-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="26531-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="26531-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="26531-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="26531-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="26531-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="26531-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="26531-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="26531-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="26531-127">In the **search box**, type **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="26531-127">In the **search box**, type **TeamSeer**.</span></span>
   
    <span data-ttu-id="26531-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789619.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="26531-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789619.png "Application Gallery")</span></span>

7. <span data-ttu-id="26531-129">In the results pane, select **TeamSeer**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="26531-129">In the results pane, select **TeamSeer**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="26531-130">![TeamSeer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789620.png "TeamSeer")</span><span class="sxs-lookup"><span data-stu-id="26531-130">![TeamSeer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789620.png "TeamSeer")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="26531-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="26531-131">Configure single sign-on</span></span>
<span data-ttu-id="26531-132">The objective of this section is to outline how to enable users to authenticate to TeamSeer with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="26531-132">The objective of this section is to outline how to enable users to authenticate to TeamSeer with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="26531-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="26531-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  

<span data-ttu-id="26531-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="26531-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="26531-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26531-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="26531-136">In the Azure classic portal, on the **TeamSeer** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="26531-136">In the Azure classic portal, on the **TeamSeer** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="26531-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789621.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="26531-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789621.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="26531-138">On the **How would you like users to sign on to TeamSeer** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26531-138">On the **How would you like users to sign on to TeamSeer** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="26531-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789628.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="26531-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789628.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="26531-140">On the **Configure App URL** page, in the **TeamSeer Sign In URL** textbox, type your URL using the following pattern "*http://www.teamseer.com/companyid*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26531-140">On the **Configure App URL** page, in the **TeamSeer Sign In URL** textbox, type your URL using the following pattern "*http://www.teamseer.com/companyid*", and then click **Next**.</span></span>
   
    <span data-ttu-id="26531-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789629.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="26531-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789629.png "Configure App URL")</span></span>

4. <span data-ttu-id="26531-142">On the **Configure single sign-on at TeamSeer** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="26531-142">On the **Configure single sign-on at TeamSeer** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="26531-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789630.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="26531-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789630.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="26531-144">In a different web browser window, log into your TeamSeer company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="26531-144">In a different web browser window, log into your TeamSeer company site as an administrator.</span></span>

6. <span data-ttu-id="26531-145">Go to **HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="26531-145">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="26531-146">![HR Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789634.png "HR Admin")</span><span class="sxs-lookup"><span data-stu-id="26531-146">![HR Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789634.png "HR Admin")</span></span>

7. <span data-ttu-id="26531-147">Click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="26531-147">Click **Setup**.</span></span>
   
    <span data-ttu-id="26531-148">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789635.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="26531-148">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789635.png "Setup")</span></span>

8. <span data-ttu-id="26531-149">Click **Set up SAML provider details**.</span><span class="sxs-lookup"><span data-stu-id="26531-149">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="26531-150">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789636.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="26531-150">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789636.png "SAML Settings")</span></span>

9. <span data-ttu-id="26531-151">In the SAML provider details section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26531-151">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="26531-152">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789637.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="26531-152">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789637.png "SAML Settings")</span></span>   
  1. <span data-ttu-id="26531-153">In the Azure classic portal, on the **Configure single sign-on at TeamSeer** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="26531-153">In the Azure classic portal, on the **Configure single sign-on at TeamSeer** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **URL** textbox.</span></span>
  2. <span data-ttu-id="26531-154">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="26531-154">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
     >[!TIP]
     ><span data-ttu-id="26531-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="26531-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
     >
     
  3. <span data-ttu-id="26531-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="26531-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

10. <span data-ttu-id="26531-157">To complete the SAML provider configuration, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26531-157">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="26531-158">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789638.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="26531-158">![SAML Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789638.png "SAML Settings")</span></span> 
  1. <span data-ttu-id="26531-159">In the **Test Email Addresses**, type the test user’s email address.</span><span class="sxs-lookup"><span data-stu-id="26531-159">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  2. <span data-ttu-id="26531-160">In the **Issuer** textbox, type the Issuer URL of the service provider.</span><span class="sxs-lookup"><span data-stu-id="26531-160">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  3. <span data-ttu-id="26531-161">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="26531-161">Click **Save**.</span></span>

11. <span data-ttu-id="26531-162">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="26531-162">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="26531-163">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789639.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="26531-163">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789639.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="26531-164">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="26531-164">Configure user provisioning</span></span>
<span data-ttu-id="26531-165">In order to enable Azure AD users to log into TeamSeer, they must be provisioned into ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="26531-165">In order to enable Azure AD users to log into TeamSeer, they must be provisioned into ShiftPlanning.</span></span>  

* <span data-ttu-id="26531-166">In the case of TeamSeer, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="26531-166">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="26531-167">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26531-167">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="26531-168">Log in to your **TeamSeer** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="26531-168">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="26531-169">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26531-169">Perform the following steps:</span></span>
   
    <span data-ttu-id="26531-170">![HR Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789640.png "HR Admin")</span><span class="sxs-lookup"><span data-stu-id="26531-170">![HR Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789640.png "HR Admin")</span></span>   
  1. <span data-ttu-id="26531-171">Go to **HR Admin \> Users**.</span><span class="sxs-lookup"><span data-stu-id="26531-171">Go to **HR Admin \> Users**.</span></span>
  2. <span data-ttu-id="26531-172">Click **Run the New User wizard**.</span><span class="sxs-lookup"><span data-stu-id="26531-172">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="26531-173">In the **User Details** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26531-173">In the **User Details** section, perform the following steps:</span></span>
   
   <span data-ttu-id="26531-174">![User Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789641.png "User Details")</span><span class="sxs-lookup"><span data-stu-id="26531-174">![User Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789641.png "User Details")</span></span>
  1. <span data-ttu-id="26531-175">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="26531-175">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="26531-176">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26531-176">Click **Next**.</span></span>

4. <span data-ttu-id="26531-177">Follow the on screen instructions for adding a new user, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="26531-177">Follow the on screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="26531-178">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="26531-178">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="26531-179">Assign users</span><span class="sxs-lookup"><span data-stu-id="26531-179">Assign users</span></span>
<span data-ttu-id="26531-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="26531-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="26531-181">**To assign users to TeamSeer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26531-181">**To assign users to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="26531-182">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="26531-182">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="26531-183">On the \*\*TeamSeer \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="26531-183">On the \*\*TeamSeer \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="26531-184">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789642.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="26531-184">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC789642.png "Assign Users")</span></span>

3. <span data-ttu-id="26531-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="26531-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="26531-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="26531-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamseer-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="26531-187">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="26531-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="26531-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26531-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















