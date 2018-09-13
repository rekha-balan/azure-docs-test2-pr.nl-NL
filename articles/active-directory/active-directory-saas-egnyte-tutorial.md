---
title: 'Tutorial: Azure Active Directory integration with Egnyte | Microsoft Docs'
description: Learn how to use Egnyte with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 58cefccd92b4f5db27f23fe04a5f7f4e6104fbb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553708"
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="14c71-103">Tutorial: Azure Active Directory integration with Egnyte</span><span class="sxs-lookup"><span data-stu-id="14c71-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>
<span data-ttu-id="14c71-104">The objective of this tutorial is to show the integration of Azure and Egnyte.</span><span class="sxs-lookup"><span data-stu-id="14c71-104">The objective of this tutorial is to show the integration of Azure and Egnyte.</span></span>  
<span data-ttu-id="14c71-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="14c71-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="14c71-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="14c71-106">A valid Azure subscription</span></span>
* <span data-ttu-id="14c71-107">An Egnyte single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="14c71-107">An Egnyte single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="14c71-108">After completing this tutorial, the Azure AD users you have assigned to Egnyte will be able to single sign into the application at your Egnyte company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="14c71-108">After completing this tutorial, the Azure AD users you have assigned to Egnyte will be able to single sign into the application at your Egnyte company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

<span data-ttu-id="14c71-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="14c71-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="14c71-110">Enabling the application integration for Egnyte</span><span class="sxs-lookup"><span data-stu-id="14c71-110">Enabling the application integration for Egnyte</span></span>
* <span data-ttu-id="14c71-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="14c71-111">Configuring single sign-on</span></span>
* <span data-ttu-id="14c71-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="14c71-112">Configuring user provisioning</span></span>
* <span data-ttu-id="14c71-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="14c71-113">Assigning users</span></span>

<span data-ttu-id="14c71-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787812.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="14c71-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787812.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-egnyte"></a><span data-ttu-id="14c71-115">Enable the application integration for Egnyte</span><span class="sxs-lookup"><span data-stu-id="14c71-115">Enable the application integration for Egnyte</span></span>
<span data-ttu-id="14c71-116">The objective of this section is to outline how to enable the application integration for Egnyte.</span><span class="sxs-lookup"><span data-stu-id="14c71-116">The objective of this section is to outline how to enable the application integration for Egnyte.</span></span>

<span data-ttu-id="14c71-117">**To enable the application integration for Egnyte, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14c71-117">**To enable the application integration for Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="14c71-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14c71-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="14c71-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="14c71-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="14c71-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="14c71-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="14c71-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="14c71-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="14c71-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="14c71-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="14c71-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="14c71-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="14c71-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="14c71-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="14c71-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="14c71-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="14c71-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="14c71-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="14c71-127">In the **search box**, type **egnyte**.</span><span class="sxs-lookup"><span data-stu-id="14c71-127">In the **search box**, type **egnyte**.</span></span>
   
   <span data-ttu-id="14c71-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787813.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="14c71-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787813.png "Application Gallery")</span></span>
7. <span data-ttu-id="14c71-129">In the results pane, select **Egnyte**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="14c71-129">In the results pane, select **Egnyte**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="14c71-130">![Egnyte](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787814.png "Egnyte")</span><span class="sxs-lookup"><span data-stu-id="14c71-130">![Egnyte](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787814.png "Egnyte")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="14c71-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="14c71-131">Configure single sign-on</span></span>

<span data-ttu-id="14c71-132">The objective of this section is to outline how to enable users to authenticate to Egnyte with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="14c71-132">The objective of this section is to outline how to enable users to authenticate to Egnyte with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="14c71-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="14c71-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="14c71-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="14c71-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="14c71-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14c71-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="14c71-136">In the Azure classic portal, on the **Egnyte** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="14c71-136">In the Azure classic portal, on the **Egnyte** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="14c71-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787815.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="14c71-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787815.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="14c71-138">On the **How would you like users to sign on to Egnyte** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="14c71-138">On the **How would you like users to sign on to Egnyte** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="14c71-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787816.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="14c71-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787816.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="14c71-140">On the **Configure App URL** page, in the **Egnyte Sign In URL** textbox, type your URL using the following pattern "*https://company.egnyte.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="14c71-140">On the **Configure App URL** page, in the **Egnyte Sign In URL** textbox, type your URL using the following pattern "*https://company.egnyte.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="14c71-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787817.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="14c71-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787817.png "Configure App URL")</span></span>
4. <span data-ttu-id="14c71-142">On the **Configure single sign-on at Egnyte** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="14c71-142">On the **Configure single sign-on at Egnyte** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="14c71-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787818.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="14c71-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787818.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="14c71-144">In a different web browser window, log into your Egnyte company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="14c71-144">In a different web browser window, log into your Egnyte company site as an administrator.</span></span>
6. <span data-ttu-id="14c71-145">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="14c71-145">Click **Settings**.</span></span>
   
   <span data-ttu-id="14c71-146">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787819.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="14c71-146">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787819.png "Settings")</span></span>
7. <span data-ttu-id="14c71-147">In the menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="14c71-147">In the menu, click **Settings**.</span></span>
   
   <span data-ttu-id="14c71-148">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787820.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="14c71-148">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787820.png "Settings")</span></span>
8. <span data-ttu-id="14c71-149">Click the **Configuration** tab, and then click **Security**.</span><span class="sxs-lookup"><span data-stu-id="14c71-149">Click the **Configuration** tab, and then click **Security**.</span></span>
   
   <span data-ttu-id="14c71-150">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787821.png "Security")</span><span class="sxs-lookup"><span data-stu-id="14c71-150">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787821.png "Security")</span></span>
9. <span data-ttu-id="14c71-151">In the **Single Sign-On Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="14c71-151">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>
   
   <span data-ttu-id="14c71-152">![Single Sign On Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787822.png "Single Sign On Authentication")</span><span class="sxs-lookup"><span data-stu-id="14c71-152">![Single Sign On Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787822.png "Single Sign On Authentication")</span></span>   
   1. <span data-ttu-id="14c71-153">As **Single sign-on authentication**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="14c71-153">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="14c71-154">As **Identity provider**, select **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="14c71-154">As **Identity provider**, select **AzureAD**.</span></span>
   3. <span data-ttu-id="14c71-155">In the Azure classic portal, on the **Configure single sign-on at Egnyte** dialog page, copy the **Remote Login URL** value, and then paste it into the \*\*Identity provider login URL \*\* textbox.</span><span class="sxs-lookup"><span data-stu-id="14c71-155">In the Azure classic portal, on the **Configure single sign-on at Egnyte** dialog page, copy the **Remote Login URL** value, and then paste it into the \*\*Identity provider login URL \*\* textbox.</span></span>
   4. <span data-ttu-id="14c71-156">In the Azure classic portal, on the **Configure single sign-on at Egnyte** dialog page, copy the **Entity ID** value, and then paste it into the **Identity provider entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="14c71-156">In the Azure classic portal, on the **Configure single sign-on at Egnyte** dialog page, copy the **Entity ID** value, and then paste it into the **Identity provider entity ID** textbox.</span></span>
   5. <span data-ttu-id="14c71-157">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="14c71-157">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
     >[!TIP]
     ><span data-ttu-id="14c71-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="14c71-158">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      > 
   6. <span data-ttu-id="14c71-159">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="14c71-159">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   7. <span data-ttu-id="14c71-160">As **Default user mapping**, select **Email address**.</span><span class="sxs-lookup"><span data-stu-id="14c71-160">As **Default user mapping**, select **Email address**.</span></span>
   8. <span data-ttu-id="14c71-161">As **Use domain-specific issuer value**, select **disabled**.</span><span class="sxs-lookup"><span data-stu-id="14c71-161">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   9. <span data-ttu-id="14c71-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14c71-162">Click **Save**.</span></span>
10. <span data-ttu-id="14c71-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="14c71-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="14c71-164">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787823.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="14c71-164">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787823.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="14c71-165">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="14c71-165">Configure user provisioning</span></span>

<span data-ttu-id="14c71-166">In order to enable Azure AD users to log into Egnyte, they must be provisioned into Egnyte.</span><span class="sxs-lookup"><span data-stu-id="14c71-166">In order to enable Azure AD users to log into Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="14c71-167">In the case of Egnyte, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="14c71-167">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="14c71-168">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14c71-168">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="14c71-169">Log in to your **Egnyte** Egnyte company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="14c71-169">Log in to your **Egnyte** Egnyte company site as administrator.</span></span>
2. <span data-ttu-id="14c71-170">Go to **Settings \> Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="14c71-170">Go to **Settings \> Users & Groups**.</span></span>
3. <span data-ttu-id="14c71-171">Click **Add New User**, and then select the type of user you want to add.</span><span class="sxs-lookup"><span data-stu-id="14c71-171">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="14c71-172">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787824.png "Users")</span><span class="sxs-lookup"><span data-stu-id="14c71-172">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787824.png "Users")</span></span>
4. <span data-ttu-id="14c71-173">In the **New Standard User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="14c71-173">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="14c71-174">![New Standard User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787825.png "New Standard User")</span><span class="sxs-lookup"><span data-stu-id="14c71-174">![New Standard User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787825.png "New Standard User")</span></span>   
   1. <span data-ttu-id="14c71-175">Type the **Email**, **Username** and other details of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="14c71-175">Type the **Email**, **Username** and other details of a valid Azure Active Directory account you want to provision.</span></span>
   2. <span data-ttu-id="14c71-176">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14c71-176">Click **Save**.</span></span>
    >[!NOTE]
    ><span data-ttu-id="14c71-177">The Azure Active Directory account holder will receive a notification email.</span><span class="sxs-lookup"><span data-stu-id="14c71-177">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="14c71-178">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="14c71-178">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

## <a name="assign-users"></a><span data-ttu-id="14c71-179">Assign users</span><span class="sxs-lookup"><span data-stu-id="14c71-179">Assign users</span></span>
<span data-ttu-id="14c71-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="14c71-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="14c71-181">**To assign users to Egnyte, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14c71-181">**To assign users to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="14c71-182">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="14c71-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="14c71-183">On the \*\*Egnyte \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="14c71-183">On the \*\*Egnyte \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="14c71-184">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787826.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="14c71-184">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787826.png "Assign Users")</span></span>
3. <span data-ttu-id="14c71-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="14c71-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="14c71-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="14c71-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="14c71-187">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="14c71-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="14c71-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="14c71-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>





















