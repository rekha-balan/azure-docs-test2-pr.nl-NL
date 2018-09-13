---
title: 'Tutorial: Azure Active Directory integration with Dropbox for Business | Microsoft Docs'
description: Learn how to use Dropbox for Business with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 13052eccc83cb7193cd3b6092c6ce1d3dbd061b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551680"
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="6cc8f-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="6cc8f-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>
<span data-ttu-id="6cc8f-104">The objective of this tutorial is to show the integration of Azure and Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-104">The objective of this tutorial is to show the integration of Azure and Dropbox for Business.</span></span>  
<span data-ttu-id="6cc8f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6cc8f-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="6cc8f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6cc8f-107">A test tenant in Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="6cc8f-107">A test tenant in Dropbox for Business</span></span>

<span data-ttu-id="6cc8f-108">After completing this tutorial, the Azure AD users you have assigned to Dropbox for Business will be able to single sign into the application at your Dropbox for Business company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6cc8f-108">After completing this tutorial, the Azure AD users you have assigned to Dropbox for Business will be able to single sign into the application at your Dropbox for Business company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6cc8f-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="6cc8f-110">Enabling the application integration for Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="6cc8f-110">Enabling the application integration for Dropbox for Business</span></span>
2. <span data-ttu-id="6cc8f-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc8f-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="6cc8f-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6cc8f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="6cc8f-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6cc8f-113">Assigning users</span></span>

<span data-ttu-id="6cc8f-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769508.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769508.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-dropbox-for-business"></a><span data-ttu-id="6cc8f-115">Enabling the application integration for Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="6cc8f-115">Enabling the application integration for Dropbox for Business</span></span>
<span data-ttu-id="6cc8f-116">The objective of this section is to outline how to enable the application integration for Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-116">The objective of this section is to outline how to enable the application integration for Dropbox for Business.</span></span>

### <a name="to-enable-the-application-integration-for-dropbox-for-business-perform-the-following-steps"></a><span data-ttu-id="6cc8f-117">To enable the application integration for Dropbox for Business, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-117">To enable the application integration for Dropbox for Business, perform the following steps:</span></span>
1. <span data-ttu-id="6cc8f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="6cc8f-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6cc8f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6cc8f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="6cc8f-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6cc8f-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="6cc8f-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6cc8f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="6cc8f-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6cc8f-127">In the **search box**, type **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-127">In the **search box**, type **Dropbox for Business**.</span></span>
   
    <span data-ttu-id="6cc8f-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC701010.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC701010.png "Application gallery")</span></span>
7. <span data-ttu-id="6cc8f-129">In the results pane, select **Dropbox for Business**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-129">In the results pane, select **Dropbox for Business**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="6cc8f-130">![Dropbox for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC701011.png "Dropbox for Business")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-130">![Dropbox for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC701011.png "Dropbox for Business")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="6cc8f-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc8f-131">Configuring single sign-on</span></span>
<span data-ttu-id="6cc8f-132">The objective of this section is to outline how to enable users to authenticate to Dropbox for Business with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-132">The objective of this section is to outline how to enable users to authenticate to Dropbox for Business with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="6cc8f-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Dropbox for Business tenant.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Dropbox for Business tenant.</span></span> <span data-ttu-id="6cc8f-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="6cc8f-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="6cc8f-135">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="6cc8f-136">In the Azure classic portal, on the **Dropbox for Business** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-136">In the Azure classic portal, on the **Dropbox for Business** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="6cc8f-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="6cc8f-138">On the **How would you like users to sign on to Dropbox for Business** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-138">On the **How would you like users to sign on to Dropbox for Business** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="6cc8f-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749327.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749327.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="6cc8f-140">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-140">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="6cc8f-141">a.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-141">a.</span></span> <span data-ttu-id="6cc8f-142">Sign-on to your Dropbox for business tenant.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-142">Sign-on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="6cc8f-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769509.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6cc8f-144">b.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-144">b.</span></span> <span data-ttu-id="6cc8f-145">In the navigation pane on the left side, click **Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-145">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="6cc8f-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769510.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-146">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6cc8f-147">c.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-147">c.</span></span> <span data-ttu-id="6cc8f-148">On the **Admin Console**, click **Authentication** in the left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-148">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="6cc8f-149">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769511.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-149">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6cc8f-150">d.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-150">d.</span></span> <span data-ttu-id="6cc8f-151">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-151">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="6cc8f-152">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769512.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-152">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6cc8f-153">e.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-153">e.</span></span> <span data-ttu-id="6cc8f-154">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-154">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
   
    <span data-ttu-id="6cc8f-155">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769513.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-155">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769513.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6cc8f-156">f.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-156">f.</span></span> <span data-ttu-id="6cc8f-157">On the Azure classic portal, in the **DropBox for business sign in** URL textbox, paste the URL.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-157">On the Azure classic portal, in the **DropBox for business sign in** URL textbox, paste the URL.</span></span> 
   
    <span data-ttu-id="6cc8f-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769514.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769514.png "Configure single sign-on")</span></span>  
4. <span data-ttu-id="6cc8f-159">On the **Configure single sign-on at Dropbox for Business** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-159">On the **Configure single sign-on at Dropbox for Business** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>  
   
    <span data-ttu-id="6cc8f-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769515.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769515.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="6cc8f-161">On your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-161">On your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="6cc8f-162">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-162">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6cc8f-163">a.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-163">a.</span></span> <span data-ttu-id="6cc8f-164">Click **Required**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-164">Click **Required**.</span></span>
   
    <span data-ttu-id="6cc8f-165">b.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-165">b.</span></span> <span data-ttu-id="6cc8f-166">In the Azure classic portal, on the **Configure single sign-on at Dropbox for Business** dialog page, copy the **Sign-in page URL** value, and then paste it into the **Sign in URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-166">In the Azure classic portal, on the **Configure single sign-on at Dropbox for Business** dialog page, copy the **Sign-in page URL** value, and then paste it into the **Sign in URL** textbox.</span></span>

    <span data-ttu-id="6cc8f-167">c.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-167">c.</span></span> <span data-ttu-id="6cc8f-168">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-168">Create a **Base-64 encoded** file from your downloaded certificate.</span></span> 

    > [!TIP] 
    > <span data-ttu-id="6cc8f-169">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="6cc8f-169">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="6cc8f-170">d.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-170">d.</span></span> <span data-ttu-id="6cc8f-171">Click **Choose certificate**, and then browse to your **base-64 encoded certificate file**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-171">Click **Choose certificate**, and then browse to your **base-64 encoded certificate file**.</span></span>

    <span data-ttu-id="6cc8f-172">e.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-172">e.</span></span> <span data-ttu-id="6cc8f-173">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-173">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

1. <span data-ttu-id="6cc8f-174">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-174">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    <span data-ttu-id="6cc8f-175">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749329.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-175">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC749329.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="6cc8f-176">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6cc8f-176">Configuring user provisioning</span></span>
<span data-ttu-id="6cc8f-177">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-177">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Dropbox for Business.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="6cc8f-178">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-178">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="6cc8f-179">In the Azure classic Portal, on the **Dropbox for Business** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-179">In the Azure classic Portal, on the **Dropbox for Business** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
2. <span data-ttu-id="6cc8f-180">On the Enable user provisioning to DropBox for Business page, click Enable user provisioning to open the Sign in to Dropbox to link with Azure AD dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-180">On the Enable user provisioning to DropBox for Business page, click Enable user provisioning to open the Sign in to Dropbox to link with Azure AD dialog.</span></span>  
   
    <span data-ttu-id="6cc8f-181">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769517.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-181">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769517.png "User provisioning")</span></span>
3. <span data-ttu-id="6cc8f-182">On the **Sign in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-182">On the **Sign in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span> 
   
    <span data-ttu-id="6cc8f-183">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769518.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-183">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769518.png "User provisioning")</span></span>
4. <span data-ttu-id="6cc8f-184">Click **Allow** to grant Azure AD to access to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-184">Click **Allow** to grant Azure AD to access to Dropbox.</span></span> 
   
    <span data-ttu-id="6cc8f-185">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769519.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-185">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769519.png "User provisioning")</span></span>
5. <span data-ttu-id="6cc8f-186">To finish the configuration, click the **Complete** button.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-186">To finish the configuration, click the **Complete** button.</span></span>  
   
    <span data-ttu-id="6cc8f-187">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769520.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-187">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769520.png "User provisioning")</span></span>

## <a name="assigning-users"></a><span data-ttu-id="6cc8f-188">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6cc8f-188">Assigning users</span></span>
<span data-ttu-id="6cc8f-189">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-189">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-dropbox-for-business-perform-the-following-steps"></a><span data-ttu-id="6cc8f-190">To assign users to Dropbox for Business, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc8f-190">To assign users to Dropbox for Business, perform the following steps:</span></span>
1. <span data-ttu-id="6cc8f-191">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-191">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6cc8f-192">On the \*\*Dropbox for Business \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-192">On the \*\*Dropbox for Business \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="6cc8f-193">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769521.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-193">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769521.png "Assign users")</span></span>
3. <span data-ttu-id="6cc8f-194">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-194">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="6cc8f-195">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-195">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6cc8f-196">You should now wait for 10 minutes and verify that the account has been synchronized to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-196">You should now wait for 10 minutes and verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="6cc8f-197">As a first verification step, you can check the provisioning status, by clicking **Dashboard** in the **Dropbox for Business** application integration page on the Azure classic Portal.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-197">As a first verification step, you can check the provisioning status, by clicking **Dashboard** in the **Dropbox for Business** application integration page on the Azure classic Portal.</span></span>

<span data-ttu-id="6cc8f-198">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769522.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-198">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769522.png "Assign users")</span></span>

<span data-ttu-id="6cc8f-199">A successfully completed user provisioning cycle is indicated by a related status.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-199">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="6cc8f-200">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769523.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="6cc8f-200">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dropboxforbusiness-tutorial/IC769523.png "Assign users")</span></span>

<span data-ttu-id="6cc8f-201">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6cc8f-201">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="6cc8f-202">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6cc8f-202">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6cc8f-203">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="6cc8f-203">Additional Resources</span></span>
* [<span data-ttu-id="6cc8f-204">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cc8f-204">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6cc8f-205">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6cc8f-205">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



























