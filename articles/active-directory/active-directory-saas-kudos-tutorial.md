---
title: 'Tutorial: Azure Active Directory integration with Kudos | Microsoft Docs'
description: Learn how to use Kudos with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/04/2017
ms.author: jeedes
ms.openlocfilehash: 7abf27c58c21fb9844e2d68171fa703f82e6725f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551079"
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="983ec-103">Tutorial: Azure Active Directory integration with Kudos</span><span class="sxs-lookup"><span data-stu-id="983ec-103">Tutorial: Azure Active Directory integration with Kudos</span></span>
<span data-ttu-id="983ec-104">The objective of this tutorial is to show the integration of Azure and Kudos.</span><span class="sxs-lookup"><span data-stu-id="983ec-104">The objective of this tutorial is to show the integration of Azure and Kudos.</span></span>  

<span data-ttu-id="983ec-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="983ec-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="983ec-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="983ec-106">A valid Azure subscription</span></span>
* <span data-ttu-id="983ec-107">A Kudos tenant</span><span class="sxs-lookup"><span data-stu-id="983ec-107">A Kudos tenant</span></span>

<span data-ttu-id="983ec-108">After completing this tutorial, the Azure AD users you have assigned to Kudos will be able to single sign into the application at your Kudos company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="983ec-108">After completing this tutorial, the Azure AD users you have assigned to Kudos will be able to single sign into the application at your Kudos company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="983ec-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="983ec-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="983ec-110">Enabling the application integration for Kudos</span><span class="sxs-lookup"><span data-stu-id="983ec-110">Enabling the application integration for Kudos</span></span>
* <span data-ttu-id="983ec-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="983ec-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="983ec-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="983ec-112">Configuring user provisioning</span></span>
* <span data-ttu-id="983ec-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="983ec-113">Assigning users</span></span>

<span data-ttu-id="983ec-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787799.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="983ec-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787799.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-kudos"></a><span data-ttu-id="983ec-115">Enabling the application integration for Kudos</span><span class="sxs-lookup"><span data-stu-id="983ec-115">Enabling the application integration for Kudos</span></span>
<span data-ttu-id="983ec-116">The objective of this section is to outline how to enable the application integration for Kudos.</span><span class="sxs-lookup"><span data-stu-id="983ec-116">The objective of this section is to outline how to enable the application integration for Kudos.</span></span>

<span data-ttu-id="983ec-117">**To enable the application integration for Kudos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="983ec-117">**To enable the application integration for Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="983ec-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983ec-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="983ec-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="983ec-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="983ec-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="983ec-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="983ec-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="983ec-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="983ec-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="983ec-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="983ec-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="983ec-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="983ec-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="983ec-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="983ec-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="983ec-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="983ec-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="983ec-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="983ec-127">In the **search box**, type **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="983ec-127">In the **search box**, type **Kudos**.</span></span>
   
   <span data-ttu-id="983ec-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787800.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="983ec-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787800.png "Application Gallery")</span></span>
7. <span data-ttu-id="983ec-129">In the results pane, select **Kudos**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="983ec-129">In the results pane, select **Kudos**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="983ec-130">![Kudos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787801.png "Kudos")</span><span class="sxs-lookup"><span data-stu-id="983ec-130">![Kudos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787801.png "Kudos")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="983ec-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="983ec-131">Configure single sign-on</span></span>

<span data-ttu-id="983ec-132">The objective of this section is to outline how to enable users to authenticate to Kudos with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="983ec-132">The objective of this section is to outline how to enable users to authenticate to Kudos with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="983ec-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="983ec-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="983ec-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="983ec-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="983ec-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="983ec-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="983ec-136">In the Azure classic portal, on the **Kudos** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="983ec-136">In the Azure classic portal, on the **Kudos** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="983ec-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787802.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="983ec-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787802.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="983ec-138">On the **How would you like users to sign on to Kudos** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="983ec-138">On the **How would you like users to sign on to Kudos** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="983ec-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787803.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="983ec-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787803.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="983ec-140">On the **Configure App URL** page, in the **Kudos Sign On URL** textbox, type your URL using the following pattern **https://company.kudosnow.com**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="983ec-140">On the **Configure App URL** page, in the **Kudos Sign On URL** textbox, type your URL using the following pattern **https://company.kudosnow.com**, and then click **Next**.</span></span>
   
   <span data-ttu-id="983ec-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787804.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="983ec-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787804.png "Configure App URL")</span></span>
4. <span data-ttu-id="983ec-142">On the **Configure single sign-on at Kudos** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="983ec-142">On the **Configure single sign-on at Kudos** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="983ec-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787805.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="983ec-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787805.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="983ec-144">In a different web browser window, log into your Kudos company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="983ec-144">In a different web browser window, log into your Kudos company site as an administrator.</span></span>
6. <span data-ttu-id="983ec-145">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="983ec-145">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="983ec-146">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787806.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="983ec-146">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787806.png "Settings")</span></span>
7. <span data-ttu-id="983ec-147">Click **Integrations \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="983ec-147">Click **Integrations \> SSO**.</span></span>
8. <span data-ttu-id="983ec-148">In the **SSO** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="983ec-148">In the **SSO** section, perform the following steps:</span></span>
   
   <span data-ttu-id="983ec-149">![SSO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="983ec-149">![SSO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787807.png "SSO")</span></span>
   
   1. <span data-ttu-id="983ec-150">In the Azure classic portal, on the **Configure single sign-on at Kudos** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the \*\*Sign on URL \*\* textbox.</span><span class="sxs-lookup"><span data-stu-id="983ec-150">In the Azure classic portal, on the **Configure single sign-on at Kudos** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the \*\*Sign on URL \*\* textbox.</span></span>
   2. <span data-ttu-id="983ec-151">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="983ec-151">Create a **base-64 encoded** file from your downloaded certificate.</span></span> 
   
      >[!TIP]
      ><span data-ttu-id="983ec-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="983ec-152">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span> 
      > 
   3. <span data-ttu-id="983ec-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="983ec-153">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   4. <span data-ttu-id="983ec-154">In the Azure classic portal, on the **Configure single sign-on at Kudos** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the \*\*Logout To URL \*\* textbox.</span><span class="sxs-lookup"><span data-stu-id="983ec-154">In the Azure classic portal, on the **Configure single sign-on at Kudos** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the \*\*Logout To URL \*\* textbox.</span></span>
   5. <span data-ttu-id="983ec-155">In the **Your Kudos URL** textbox, type your company name.</span><span class="sxs-lookup"><span data-stu-id="983ec-155">In the **Your Kudos URL** textbox, type your company name.</span></span>
   6. <span data-ttu-id="983ec-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="983ec-156">Click **Save**.</span></span>
9. <span data-ttu-id="983ec-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="983ec-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="983ec-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787808.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="983ec-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787808.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="983ec-159">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="983ec-159">Configure user provisioning</span></span>

<span data-ttu-id="983ec-160">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span><span class="sxs-lookup"><span data-stu-id="983ec-160">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

* <span data-ttu-id="983ec-161">In the case of Kudos, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="983ec-161">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="983ec-162">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="983ec-162">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="983ec-163">Log in to your **Kudos** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="983ec-163">Log in to your **Kudos** company site as administrator.</span></span>
2. <span data-ttu-id="983ec-164">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="983ec-164">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="983ec-165">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787806.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="983ec-165">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787806.png "Settings")</span></span>
3. <span data-ttu-id="983ec-166">Click **User Admin**.</span><span class="sxs-lookup"><span data-stu-id="983ec-166">Click **User Admin**.</span></span>
4. <span data-ttu-id="983ec-167">Click the **Users** tab, and then click **Add a user**.</span><span class="sxs-lookup"><span data-stu-id="983ec-167">Click the **Users** tab, and then click **Add a user**.</span></span>
   
   <span data-ttu-id="983ec-168">![User Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787809.png "User Admin")</span><span class="sxs-lookup"><span data-stu-id="983ec-168">![User Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787809.png "User Admin")</span></span>
5. <span data-ttu-id="983ec-169">In the **Add a User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="983ec-169">In the **Add a User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="983ec-170">![Add a User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787810.png "Add a User")</span><span class="sxs-lookup"><span data-stu-id="983ec-170">![Add a User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787810.png "Add a User")</span></span>
   
  1. <span data-ttu-id="983ec-171">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="983ec-171">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="983ec-172">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="983ec-172">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="983ec-173">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="983ec-173">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="983ec-174">Assign users</span><span class="sxs-lookup"><span data-stu-id="983ec-174">Assign users</span></span>
<span data-ttu-id="983ec-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="983ec-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="983ec-176">**To assign users to Kudos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="983ec-176">**To assign users to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="983ec-177">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="983ec-177">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="983ec-178">On the **Kudos** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="983ec-178">On the **Kudos** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="983ec-179">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787811.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="983ec-179">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC787811.png "Assign users")</span></span>
3. <span data-ttu-id="983ec-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="983ec-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="983ec-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="983ec-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kudos-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="983ec-182">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="983ec-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="983ec-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="983ec-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>




















