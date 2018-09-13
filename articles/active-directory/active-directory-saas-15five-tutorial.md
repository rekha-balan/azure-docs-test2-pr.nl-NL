---
title: 'Tutorial: Azure Active Directory integration with 15Five | Microsoft Docs'
description: Learn how to use 15Five with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 07d2198b51464c700c08e278699f57135141f17b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553807"
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="a1577-103">Tutorial: Azure Active Directory integration with 15Five</span><span class="sxs-lookup"><span data-stu-id="a1577-103">Tutorial: Azure Active Directory integration with 15Five</span></span>
<span data-ttu-id="a1577-104">The objective of this tutorial is to show the integration of Azure and 15Five.</span><span class="sxs-lookup"><span data-stu-id="a1577-104">The objective of this tutorial is to show the integration of Azure and 15Five.</span></span> <span data-ttu-id="a1577-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a1577-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a1577-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a1577-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a1577-107">A 15Five single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a1577-107">A 15Five single sign-on enabled subscription</span></span>

<span data-ttu-id="a1577-108">After completing this tutorial, the Azure AD users you have assigned to 15Five will be able to single sign into the application at your 15Five company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a1577-108">After completing this tutorial, the Azure AD users you have assigned to 15Five will be able to single sign into the application at your 15Five company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a1577-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1577-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="a1577-110">Enabling the application integration for 15Five</span><span class="sxs-lookup"><span data-stu-id="a1577-110">Enabling the application integration for 15Five</span></span>
2. <span data-ttu-id="a1577-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1577-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="a1577-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a1577-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="a1577-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a1577-113">Assigning users</span></span>

<span data-ttu-id="a1577-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784667.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a1577-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784667.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-15five"></a><span data-ttu-id="a1577-115">Enabling the application integration for 15Five</span><span class="sxs-lookup"><span data-stu-id="a1577-115">Enabling the application integration for 15Five</span></span>
<span data-ttu-id="a1577-116">The objective of this section is to outline how to enable the application integration for 15Five.</span><span class="sxs-lookup"><span data-stu-id="a1577-116">The objective of this section is to outline how to enable the application integration for 15Five.</span></span>

### <a name="to-enable-the-application-integration-for-15five-perform-the-following-steps"></a><span data-ttu-id="a1577-117">To enable the application integration for 15Five, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1577-117">To enable the application integration for 15Five, perform the following steps:</span></span>
1. <span data-ttu-id="a1577-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1577-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a1577-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a1577-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a1577-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a1577-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a1577-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a1577-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a1577-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a1577-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a1577-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a1577-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a1577-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a1577-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a1577-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a1577-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a1577-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a1577-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a1577-127">In the **search box**, type **15Five**.</span><span class="sxs-lookup"><span data-stu-id="a1577-127">In the **search box**, type **15Five**.</span></span>
   
   <span data-ttu-id="a1577-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784668.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a1577-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784668.png "Application Gallery")</span></span>
7. <span data-ttu-id="a1577-129">In the results pane, select **15Five**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a1577-129">In the results pane, select **15Five**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a1577-130">![15Five](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784669.png "15Five")</span><span class="sxs-lookup"><span data-stu-id="a1577-130">![15Five](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784669.png "15Five")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="a1577-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1577-131">Configuring single sign-on</span></span>

<span data-ttu-id="a1577-132">The objective of this section is to outline how to enable users to authenticate to 15Five with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a1577-132">The objective of this section is to outline how to enable users to authenticate to 15Five with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="a1577-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1577-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="a1577-134">In the Azure classic portal, on the **15Five** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="a1577-134">In the Azure classic portal, on the **15Five** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="a1577-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784670.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a1577-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784670.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="a1577-136">On the **How would you like users to sign on to 15Five** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1577-136">On the **How would you like users to sign on to 15Five** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a1577-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784671.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a1577-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784671.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="a1577-138">On the **Configure App URL** page, in the **15Five Sign In URL** textbox, type your URL using the following pattern "*https://company.15Five.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1577-138">On the **Configure App URL** page, in the **15Five Sign In URL** textbox, type your URL using the following pattern "*https://company.15Five.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="a1577-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784672.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a1577-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784672.png "Configure App URL")</span></span>
4. <span data-ttu-id="a1577-140">On the **Configure single sign-on at 15Five** page, click **Download metadata**, and then forward the metadata file to the 15Five support team.</span><span class="sxs-lookup"><span data-stu-id="a1577-140">On the **Configure single sign-on at 15Five** page, click **Download metadata**, and then forward the metadata file to the 15Five support team.</span></span>
   
   <span data-ttu-id="a1577-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784673.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a1577-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784673.png "Configure single sign-on")</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1577-142">Single sign-on needs to be enabled by the 15Five support team.</span><span class="sxs-lookup"><span data-stu-id="a1577-142">Single sign-on needs to be enabled by the 15Five support team.</span></span>
   > 
   > 
5. <span data-ttu-id="a1577-143">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1577-143">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a1577-144">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784674.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a1577-144">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784674.png "Configure single sign-on")</span></span>
   

## <a name="configuring-user-provisioning"></a><span data-ttu-id="a1577-145">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a1577-145">Configuring user provisioning</span></span>

<span data-ttu-id="a1577-146">In order to enable Azure AD users to log into 15Five, they must be provisioned into 15Five.</span><span class="sxs-lookup"><span data-stu-id="a1577-146">In order to enable Azure AD users to log into 15Five, they must be provisioned into 15Five.</span></span>  
<span data-ttu-id="a1577-147">In the case of 15Five, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a1577-147">In the case of 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="a1577-148">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1577-148">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="a1577-149">Log in to your **15Five** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="a1577-149">Log in to your **15Five** company site as administrator.</span></span>
2. <span data-ttu-id="a1577-150">Go to **Manage Company**.</span><span class="sxs-lookup"><span data-stu-id="a1577-150">Go to **Manage Company**.</span></span>
   
   <span data-ttu-id="a1577-151">![Manage Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span><span class="sxs-lookup"><span data-stu-id="a1577-151">![Manage Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>
3. <span data-ttu-id="a1577-152">Go to **People \> Add People**.</span><span class="sxs-lookup"><span data-stu-id="a1577-152">Go to **People \> Add People**.</span></span>
   
   <span data-ttu-id="a1577-153">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784676.png "People")</span><span class="sxs-lookup"><span data-stu-id="a1577-153">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>
4. <span data-ttu-id="a1577-154">In the Add New Person section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1577-154">In the Add New Person section, perform the following steps:</span></span>
   
   <span data-ttu-id="a1577-155">![Add New Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span><span class="sxs-lookup"><span data-stu-id="a1577-155">![Add New Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
   1. <span data-ttu-id="a1577-156">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="a1577-156">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="a1577-157">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="a1577-157">Click **Done**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1577-158">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="a1577-158">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span>
   > 
   > 



## <a name="assigning-users"></a><span data-ttu-id="a1577-159">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a1577-159">Assigning users</span></span>
<span data-ttu-id="a1577-160">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a1577-160">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-15five-perform-the-following-steps"></a><span data-ttu-id="a1577-161">To assign users to 15Five, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1577-161">To assign users to 15Five, perform the following steps:</span></span>
1. <span data-ttu-id="a1577-162">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a1577-162">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a1577-163">On the \*\*15Five \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a1577-163">On the \*\*15Five \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a1577-164">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784678.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="a1577-164">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC784678.png "Assign users")</span></span>
3. <span data-ttu-id="a1577-165">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a1577-165">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a1577-166">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a1577-166">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-15five-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a1577-167">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a1577-167">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a1577-168">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a1577-168">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















