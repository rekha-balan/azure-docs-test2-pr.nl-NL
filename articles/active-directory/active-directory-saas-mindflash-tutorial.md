---
title: 'Tutorial: Azure Active Directory integration with Mindflash | Microsoft Docs'
description: Learn how to use Mindflash with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: d1aa9555ea5b38935c7e562704d8f79f3ca3d2dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662658"
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="ed780-103">Tutorial: Azure Active Directory integration with Mindflash</span><span class="sxs-lookup"><span data-stu-id="ed780-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>
<span data-ttu-id="ed780-104">The objective of this tutorial is to show the integration of Azure and Mindflash.</span><span class="sxs-lookup"><span data-stu-id="ed780-104">The objective of this tutorial is to show the integration of Azure and Mindflash.</span></span> <span data-ttu-id="ed780-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="ed780-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ed780-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="ed780-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ed780-107">A Mindflash single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ed780-107">A Mindflash single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="ed780-108">After completing this tutorial, the Azure AD users you have assigned to Mindflash will be able to single sign into the application at your Mindflash company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ed780-108">After completing this tutorial, the Azure AD users you have assigned to Mindflash will be able to single sign into the application at your Mindflash company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="ed780-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ed780-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="ed780-110">Enabling the application integration for Mindflash</span><span class="sxs-lookup"><span data-stu-id="ed780-110">Enabling the application integration for Mindflash</span></span>
2. <span data-ttu-id="ed780-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="ed780-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="ed780-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="ed780-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="ed780-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="ed780-113">Assigning users</span></span>

<span data-ttu-id="ed780-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787132.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="ed780-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787132.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-mindflash"></a><span data-ttu-id="ed780-115">Enabling the application integration for Mindflash</span><span class="sxs-lookup"><span data-stu-id="ed780-115">Enabling the application integration for Mindflash</span></span>
<span data-ttu-id="ed780-116">The objective of this section is to outline how to enable the application integration for Mindflash.</span><span class="sxs-lookup"><span data-stu-id="ed780-116">The objective of this section is to outline how to enable the application integration for Mindflash.</span></span>

### <a name="to-enable-the-application-integration-for-mindflash-perform-the-following-steps"></a><span data-ttu-id="ed780-117">To enable the application integration for Mindflash, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed780-117">To enable the application integration for Mindflash, perform the following steps:</span></span>
1. <span data-ttu-id="ed780-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed780-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ed780-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ed780-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ed780-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ed780-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ed780-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ed780-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ed780-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="ed780-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ed780-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ed780-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ed780-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="ed780-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ed780-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ed780-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ed780-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="ed780-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ed780-127">In the **search box**, type **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="ed780-127">In the **search box**, type **Mindflash**.</span></span>
   
   <span data-ttu-id="ed780-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787133.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="ed780-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787133.png "Application Gallery")</span></span>
7. <span data-ttu-id="ed780-129">In the results pane, select **Mindflash**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ed780-129">In the results pane, select **Mindflash**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ed780-130">![Mindflash](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787134.png "Mindflash")</span><span class="sxs-lookup"><span data-stu-id="ed780-130">![Mindflash](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787134.png "Mindflash")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="ed780-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="ed780-131">Configuring single sign-on</span></span>

<span data-ttu-id="ed780-132">The objective of this section is to outline how to enable users to authenticate to Mindflash with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="ed780-132">The objective of this section is to outline how to enable users to authenticate to Mindflash with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="ed780-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed780-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="ed780-134">In the Azure classic portal, on the **Mindflash** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="ed780-134">In the Azure classic portal, on the **Mindflash** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="ed780-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787135.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ed780-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787135.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="ed780-136">On the **How would you like users to sign on to Mindflash** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed780-136">On the **How would you like users to sign on to Mindflash** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ed780-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787136.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ed780-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787136.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="ed780-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern "*http://company.mindflash.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed780-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern "*http://company.mindflash.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="ed780-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787137.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="ed780-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787137.png "Configure App URL")</span></span>
4. <span data-ttu-id="ed780-140">On the **Configure single sign-on at Mindflash** page, click **Download metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ed780-140">On the **Configure single sign-on at Mindflash** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="ed780-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787138.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ed780-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787138.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="ed780-142">Send the metadatafile to the Mindflash support team.</span><span class="sxs-lookup"><span data-stu-id="ed780-142">Send the metadatafile to the Mindflash support team.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ed780-143">The single sign-on configuration has to be performed by the Mindflash support team.</span><span class="sxs-lookup"><span data-stu-id="ed780-143">The single sign-on configuration has to be performed by the Mindflash support team.</span></span> <span data-ttu-id="ed780-144">You will get a notification as soon as the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="ed780-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="ed780-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ed780-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="ed780-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787139.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ed780-146">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787139.png "Configure Single Sign-On")</span></span>
   
## <a name="configuring-user-provisioning"></a><span data-ttu-id="ed780-147">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="ed780-147">Configuring user provisioning</span></span>

<span data-ttu-id="ed780-148">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span><span class="sxs-lookup"><span data-stu-id="ed780-148">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="ed780-149">In the case of Mindflash, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="ed780-149">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="ed780-150">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed780-150">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="ed780-151">Log in to your **Mindflash** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ed780-151">Log in to your **Mindflash** company site as an administrator.</span></span>
2. <span data-ttu-id="ed780-152">Go to **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="ed780-152">Go to **Manage Users**.</span></span>
   
   <span data-ttu-id="ed780-153">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787140.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="ed780-153">![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787140.png "Manage Users")</span></span>
3. <span data-ttu-id="ed780-154">Click the **Add Users**, and then click **New**.</span><span class="sxs-lookup"><span data-stu-id="ed780-154">Click the **Add Users**, and then click **New**.</span></span>
4. <span data-ttu-id="ed780-155">In the **Add New Users** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed780-155">In the **Add New Users** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ed780-156">![Add New Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787141.png "Add New Users")</span><span class="sxs-lookup"><span data-stu-id="ed780-156">![Add New Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787141.png "Add New Users")</span></span>
   
   1. <span data-ttu-id="ed780-157">Type the **First name**, **Last name** and **Email** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="ed780-157">Type the **First name**, **Last name** and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="ed780-158">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ed780-158">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="ed780-159">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="ed780-159">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="ed780-160">Assigning users</span><span class="sxs-lookup"><span data-stu-id="ed780-160">Assigning users</span></span>
<span data-ttu-id="ed780-161">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="ed780-161">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-mindflash-perform-the-following-steps"></a><span data-ttu-id="ed780-162">To assign users to Mindflash, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed780-162">To assign users to Mindflash, perform the following steps:</span></span>
1. <span data-ttu-id="ed780-163">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="ed780-163">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ed780-164">On the **Mindflash** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="ed780-164">On the **Mindflash** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ed780-165">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787142.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="ed780-165">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC787142.png "Assign users")</span></span>
3. <span data-ttu-id="ed780-166">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="ed780-166">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ed780-167">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="ed780-167">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mindflash-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ed780-168">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ed780-168">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ed780-169">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ed780-169">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

















