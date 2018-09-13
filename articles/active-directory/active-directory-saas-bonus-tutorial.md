---
title: 'Tutorial: Azure Active Directory Integration with Bonus.ly | Microsoft Docs'
description: Learn how to use Bonus.ly with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9856db1447c83d7b551324d1034d739d06b77307
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554504"
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="ae89b-103">Tutorial: Azure Active Directory Integration with Bonus.ly</span><span class="sxs-lookup"><span data-stu-id="ae89b-103">Tutorial: Azure Active Directory Integration with Bonus.ly</span></span>
<span data-ttu-id="ae89b-104">The objective of this tutorial is to show the integration of Azure and Bonus.ly.</span><span class="sxs-lookup"><span data-stu-id="ae89b-104">The objective of this tutorial is to show the integration of Azure and Bonus.ly.</span></span> 

<span data-ttu-id="ae89b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="ae89b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ae89b-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="ae89b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ae89b-107">A test tenant in Bonus.ly</span><span class="sxs-lookup"><span data-stu-id="ae89b-107">A test tenant in Bonus.ly</span></span>

<span data-ttu-id="ae89b-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae89b-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="ae89b-109">Enabling the application integration for Bonus.ly</span><span class="sxs-lookup"><span data-stu-id="ae89b-109">Enabling the application integration for Bonus.ly</span></span>
* <span data-ttu-id="ae89b-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="ae89b-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="ae89b-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="ae89b-111">Configuring user provisioning</span></span>
* <span data-ttu-id="ae89b-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="ae89b-112">Assigning users</span></span>

<span data-ttu-id="ae89b-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773679.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="ae89b-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773679.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-bonusly"></a><span data-ttu-id="ae89b-114">Enable the application integration for Bonus.ly</span><span class="sxs-lookup"><span data-stu-id="ae89b-114">Enable the application integration for Bonus.ly</span></span>
<span data-ttu-id="ae89b-115">The objective of this section is to outline how to enable the application integration for Bonus.ly.</span><span class="sxs-lookup"><span data-stu-id="ae89b-115">The objective of this section is to outline how to enable the application integration for Bonus.ly.</span></span>

<span data-ttu-id="ae89b-116">**To enable the application integration for Bonus.ly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-116">**To enable the application integration for Bonus.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ae89b-118">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773680.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="ae89b-118">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773680.png "Enable single sign-on")</span></span>
2. <span data-ttu-id="ae89b-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ae89b-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ae89b-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ae89b-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ae89b-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="ae89b-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ae89b-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ae89b-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ae89b-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="ae89b-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ae89b-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ae89b-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="ae89b-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ae89b-126">In the **search box**, type **Bonus.ly**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-126">In the **search box**, type **Bonus.ly**.</span></span>
   
   <span data-ttu-id="ae89b-127">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773681.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="ae89b-127">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773681.png "Application gallery")</span></span>
7. <span data-ttu-id="ae89b-128">In the results pane, select **Bonus.ly**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ae89b-128">In the results pane, select **Bonus.ly**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ae89b-129">![Bonusly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773682.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="ae89b-129">![Bonusly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773682.png "Bonusly")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ae89b-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae89b-130">Configure single sign-on</span></span>

<span data-ttu-id="ae89b-131">The objective of this section is to outline how to enable users to authenticate to Bonus.ly with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="ae89b-131">The objective of this section is to outline how to enable users to authenticate to Bonus.ly with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="ae89b-132">Configuring SSO for Bonus.ly requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="ae89b-132">Configuring SSO for Bonus.ly requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="ae89b-133">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="ae89b-133">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="ae89b-134">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-135">In the Azure classic portal, on the **Bonus.ly** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae89b-135">In the Azure classic portal, on the **Bonus.ly** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="ae89b-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="ae89b-136">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="ae89b-137">On the **How would you like users to sign on to Bonus.ly** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-137">On the **How would you like users to sign on to Bonus.ly** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ae89b-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773683.png "Configure single sign-on") \*3.</span><span class="sxs-lookup"><span data-stu-id="ae89b-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773683.png "Configure single sign-on") \*3.</span></span> <span data-ttu-id="ae89b-139">On the **Configure App URL** page, in the **Bonus.ly Tenant URL** textbox, type your URL using the following pattern **https://\<tenant-name\>.Bonus.ly**, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="ae89b-139">On the **Configure App URL** page, in the **Bonus.ly Tenant URL** textbox, type your URL using the following pattern **https://\<tenant-name\>.Bonus.ly**, and then click **Next**:</span></span> 
   
   <span data-ttu-id="ae89b-140">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773684.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="ae89b-140">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773684.png "Configure app URL")</span></span>
4. <span data-ttu-id="ae89b-141">On the **Configure single sign-on at Bonus.ly** page, click **download Certificate**, and then save the certificate file locally as **c:\\Bonusly.cer**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-141">On the **Configure single sign-on at Bonus.ly** page, click **download Certificate**, and then save the certificate file locally as **c:\\Bonusly.cer**.</span></span>
   
   <span data-ttu-id="ae89b-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773685.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="ae89b-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773685.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="ae89b-143">In a different browser window, log in to your **Bonus.ly** tenant.</span><span class="sxs-lookup"><span data-stu-id="ae89b-143">In a different browser window, log in to your **Bonus.ly** tenant.</span></span>
6. <span data-ttu-id="ae89b-144">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-144">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
   <span data-ttu-id="ae89b-145">![Bonusly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="ae89b-145">![Bonusly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773686.png "Bonusly")</span></span>
7. <span data-ttu-id="ae89b-146">Under **Single Sign-On**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-146">Under **Single Sign-On**, select **SAML**.</span></span>
8. <span data-ttu-id="ae89b-147">On the **SAML** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-147">On the **SAML** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="ae89b-148">![Bonusly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="ae89b-148">![Bonusly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773687.png "Bonusly")</span></span>   
   1. <span data-ttu-id="ae89b-149">In the Azure classic portal, on the **Configure single sign-on at Bonus.ly** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP SSO target URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ae89b-149">In the Azure classic portal, on the **Configure single sign-on at Bonus.ly** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP SSO target URL** textbox.</span></span>
   2. <span data-ttu-id="ae89b-150">In the Azure classic portal, on the **Configure single sign-on at Bonus.ly** dialog page, copy the **Issuer ID** value, and then paste it into the **IdP Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="ae89b-150">In the Azure classic portal, on the **Configure single sign-on at Bonus.ly** dialog page, copy the **Issuer ID** value, and then paste it into the **IdP Issuer** textbox.</span></span>
   3. <span data-ttu-id="ae89b-151">In the Azure classic portal, on the **Configure single sign-on at Bonus.ly** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ae89b-151">In the Azure classic portal, on the **Configure single sign-on at Bonus.ly** dialog page, copy the **Remote Login URL** value, and then paste it into the **IdP Login URL** textbox.</span></span>
   4. <span data-ttu-id="ae89b-152">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Cert Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="ae89b-152">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Cert Fingerprint** textbox.</span></span>
   
    >[!TIP]
    ><span data-ttu-id="ae89b-153">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="ae89b-153">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>
    > 
9. <span data-ttu-id="ae89b-154">Click **save**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-154">Click **save**.</span></span>
10. <span data-ttu-id="ae89b-155">On the Microsoft Azure classic portal, select the configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae89b-155">On the Microsoft Azure classic portal, select the configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="ae89b-156">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773689.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="ae89b-156">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773689.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="ae89b-157">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="ae89b-157">Configure user provisioning</span></span>

<span data-ttu-id="ae89b-158">In order to enable Azure AD users to log into Bonus.ly, they must be provisioned into Bonus.ly.</span><span class="sxs-lookup"><span data-stu-id="ae89b-158">In order to enable Azure AD users to log into Bonus.ly, they must be provisioned into Bonus.ly.</span></span> 

* <span data-ttu-id="ae89b-159">In the case of Bonus.ly, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="ae89b-159">In the case of Bonus.ly, provisioning is a manual task.</span></span>

<span data-ttu-id="ae89b-160">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-161">In a web browser window, log into your Bonus.ly tenant.</span><span class="sxs-lookup"><span data-stu-id="ae89b-161">In a web browser window, log into your Bonus.ly tenant.</span></span>
2. <span data-ttu-id="ae89b-162">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-162">Click **Settings**.</span></span>
 
   <span data-ttu-id="ae89b-163">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781041.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="ae89b-163">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781041.png "Settings")</span></span>
3. <span data-ttu-id="ae89b-164">Click the **Users and bonuses** tab.</span><span class="sxs-lookup"><span data-stu-id="ae89b-164">Click the **Users and bonuses** tab.</span></span>
   
   <span data-ttu-id="ae89b-165">![Users and bonuses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781042.png "Users and bonuses")</span><span class="sxs-lookup"><span data-stu-id="ae89b-165">![Users and bonuses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781042.png "Users and bonuses")</span></span>
4. <span data-ttu-id="ae89b-166">Click **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-166">Click **Manage Users**.</span></span>
   
   <span data-ttu-id="ae89b-167">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781043.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="ae89b-167">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781043.png "Manage Users")</span></span>
5. <span data-ttu-id="ae89b-168">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-168">Click **Add User**.</span></span>
   
   <span data-ttu-id="ae89b-169">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781044.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="ae89b-169">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781044.png "Add User")</span></span>
6. <span data-ttu-id="ae89b-170">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-170">On the **Add User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="ae89b-171">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781045.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="ae89b-171">![Add User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC781045.png "Add User")</span></span>  
   1. <span data-ttu-id="ae89b-172">Type the “**Email**, **First name**, **Last name**” of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="ae89b-172">Type the “**Email**, **First name**, **Last name**” of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="ae89b-173">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-173">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="ae89b-174">The AAD account holder will receive an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="ae89b-174">The AAD account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

>[!NOTE]
><span data-ttu-id="ae89b-175">You can use any other Bonus.ly user account creation tools or APIs provided by Bonus.ly to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="ae89b-175">You can use any other Bonus.ly user account creation tools or APIs provided by Bonus.ly to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="ae89b-176">Assign users</span><span class="sxs-lookup"><span data-stu-id="ae89b-176">Assign users</span></span>
<span data-ttu-id="ae89b-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="ae89b-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ae89b-178">**To assign users to Bonus.ly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-178">**To assign users to Bonus.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-179">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="ae89b-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ae89b-180">On the Bonus.ly application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-180">On the Bonus.ly application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ae89b-181">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773690.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="ae89b-181">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC773690.png "Assign users")</span></span>
3. <span data-ttu-id="ae89b-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="ae89b-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ae89b-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="ae89b-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonus-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ae89b-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ae89b-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ae89b-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae89b-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















