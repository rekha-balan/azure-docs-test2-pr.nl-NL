---
title: 'Tutorial: Azure Active Directory integration with Coupa | Microsoft Docs'
description: Learn how to use Coupa with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 3f26f61d7b9dc395ef433c691a57c49ae9cd732a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554523"
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="534b4-103">Tutorial: Azure Active Directory integration with Coupa</span><span class="sxs-lookup"><span data-stu-id="534b4-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="534b4-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span><span class="sxs-lookup"><span data-stu-id="534b4-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="534b4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="534b4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="534b4-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="534b4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="534b4-107">A Coupa single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="534b4-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="534b4-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="534b4-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="534b4-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="534b4-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="534b4-110">Enabling the application integration for Coupa</span><span class="sxs-lookup"><span data-stu-id="534b4-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="534b4-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="534b4-111">Configuring single sign-on</span></span>
* <span data-ttu-id="534b4-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="534b4-112">Configuring user provisioning</span></span>
* <span data-ttu-id="534b4-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="534b4-113">Assigning users</span></span>

<span data-ttu-id="534b4-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="534b4-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="534b4-115">Enable the application integration for Coupa</span><span class="sxs-lookup"><span data-stu-id="534b4-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="534b4-116">The objective of this section is to outline how to enable the application integration for Coupa.</span><span class="sxs-lookup"><span data-stu-id="534b4-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="534b4-117">**To enable the application integration for Coupa, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="534b4-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="534b4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="534b4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="534b4-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="534b4-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="534b4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="534b4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="534b4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="534b4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="534b4-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="534b4-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="534b4-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="534b4-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="534b4-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="534b4-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="534b4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="534b4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="534b4-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="534b4-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="534b4-127">In the **search box**, type **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="534b4-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="534b4-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="534b4-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="534b4-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="534b4-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="534b4-130">![Coupa](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="534b4-130">![Coupa](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="534b4-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="534b4-131">Configure single sign-on</span></span>

<span data-ttu-id="534b4-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="534b4-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="534b4-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="534b4-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="534b4-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="534b4-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="534b4-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="534b4-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="534b4-136">Sign on to your Coupa company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="534b4-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="534b4-137">Go to **Setup \> Security Control**.</span><span class="sxs-lookup"><span data-stu-id="534b4-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="534b4-138">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="534b4-138">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="534b4-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span><span class="sxs-lookup"><span data-stu-id="534b4-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="534b4-140">![Coupa SP metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span><span class="sxs-lookup"><span data-stu-id="534b4-140">![Coupa SP metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="534b4-141">In a different browser window, sign on to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="534b4-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="534b4-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="534b4-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="534b4-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="534b4-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="534b4-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="534b4-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="534b4-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="534b4-145">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="534b4-146">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="534b4-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="534b4-147">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="534b4-147">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="534b4-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span><span class="sxs-lookup"><span data-stu-id="534b4-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="534b4-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="534b4-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="534b4-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span><span class="sxs-lookup"><span data-stu-id="534b4-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="534b4-151">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="534b4-151">Click **Next**.</span></span>
8. <span data-ttu-id="534b4-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="534b4-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="534b4-153">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="534b4-153">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="534b4-154">On the Coupa company site, go to **Setup \> Security Control**.</span><span class="sxs-lookup"><span data-stu-id="534b4-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="534b4-155">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="534b4-155">![Security Controls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="534b4-156">In the **Log in using Coupa credentials** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="534b4-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="534b4-157">![Log in using Coupa credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span><span class="sxs-lookup"><span data-stu-id="534b4-157">![Log in using Coupa credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="534b4-158">Select **Log in using SAML**.</span><span class="sxs-lookup"><span data-stu-id="534b4-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="534b4-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span><span class="sxs-lookup"><span data-stu-id="534b4-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="534b4-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="534b4-160">Click **Save**.</span></span>
11. <span data-ttu-id="534b4-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="534b4-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="534b4-162">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="534b4-162">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="534b4-163">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="534b4-163">Configure user provisioning</span></span>

<span data-ttu-id="534b4-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span><span class="sxs-lookup"><span data-stu-id="534b4-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="534b4-165">In the case of Coupa, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="534b4-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="534b4-166">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="534b4-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="534b4-167">Log in to your **Coupa** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="534b4-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="534b4-168">In the menu on the top, click **Setup**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="534b4-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="534b4-169">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span><span class="sxs-lookup"><span data-stu-id="534b4-169">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="534b4-170">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="534b4-170">Click **Create**.</span></span>
   
   <span data-ttu-id="534b4-171">![Create Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span><span class="sxs-lookup"><span data-stu-id="534b4-171">![Create Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="534b4-172">In the **User Create** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="534b4-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="534b4-173">![User Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span><span class="sxs-lookup"><span data-stu-id="534b4-173">![User Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="534b4-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="534b4-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="534b4-175">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="534b4-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="534b4-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="534b4-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="534b4-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="534b4-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="534b4-178">Assign users</span><span class="sxs-lookup"><span data-stu-id="534b4-178">Assign users</span></span>
<span data-ttu-id="534b4-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="534b4-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="534b4-180">**To assign users to Coupa, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="534b4-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="534b4-181">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="534b4-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="534b4-182">On the \*\*Coupa \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="534b4-182">On the \*\*Coupa \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="534b4-183">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="534b4-183">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="534b4-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="534b4-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="534b4-185">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="534b4-185">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="534b4-186">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="534b4-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="534b4-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="534b4-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















