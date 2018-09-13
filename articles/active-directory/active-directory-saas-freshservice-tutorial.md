---
title: 'Tutorial: Azure Active Directory integration with FreshService | Microsoft Docs'
description: Learn how to use FreshService with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f04c2cc720c95980099d46be7e492de983eea35c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662755"
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="c1c81-103">Tutorial: Azure Active Directory integration with FreshService</span><span class="sxs-lookup"><span data-stu-id="c1c81-103">Tutorial: Azure Active Directory integration with FreshService</span></span>
<span data-ttu-id="c1c81-104">The objective of this tutorial is to show the integration of Azure and FreshService.</span><span class="sxs-lookup"><span data-stu-id="c1c81-104">The objective of this tutorial is to show the integration of Azure and FreshService.</span></span>  

<span data-ttu-id="c1c81-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="c1c81-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c1c81-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c1c81-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c1c81-107">A FreshService single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c1c81-107">A FreshService single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c1c81-108">After completing this tutorial, the Azure AD users you have assigned to FreshService will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1c81-108">After completing this tutorial, the Azure AD users you have assigned to FreshService will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c1c81-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c1c81-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="c1c81-110">Enabling the application integration for FreshService</span><span class="sxs-lookup"><span data-stu-id="c1c81-110">Enabling the application integration for FreshService</span></span>
* <span data-ttu-id="c1c81-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="c1c81-111">Configuring single sign-on</span></span>
* <span data-ttu-id="c1c81-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="c1c81-112">Configuring user provisioning</span></span>
* <span data-ttu-id="c1c81-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="c1c81-113">Assigning users</span></span>

<span data-ttu-id="c1c81-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790807.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="c1c81-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790807.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-freshservice"></a><span data-ttu-id="c1c81-115">Enable the application integration for FreshService</span><span class="sxs-lookup"><span data-stu-id="c1c81-115">Enable the application integration for FreshService</span></span>
<span data-ttu-id="c1c81-116">The objective of this section is to outline how to enable the application integration for FreshService.</span><span class="sxs-lookup"><span data-stu-id="c1c81-116">The objective of this section is to outline how to enable the application integration for FreshService.</span></span>

<span data-ttu-id="c1c81-117">**To enable the application integration for FreshService, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1c81-117">**To enable the application integration for FreshService, perform the following steps:**</span></span>

1. <span data-ttu-id="c1c81-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c1c81-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c1c81-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c1c81-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c1c81-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c1c81-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c1c81-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="c1c81-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="c1c81-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c1c81-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c1c81-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="c1c81-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="c1c81-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c1c81-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="c1c81-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="c1c81-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c1c81-127">In the **search box**, type **FreshService**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-127">In the **search box**, type **FreshService**.</span></span>
   
   <span data-ttu-id="c1c81-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790808.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="c1c81-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790808.png "Application Gallery")</span></span>
7. <span data-ttu-id="c1c81-129">In the results pane, select **FreshService**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c1c81-129">In the results pane, select **FreshService**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="c1c81-130">![Freshservice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790809.png "Freshservice")</span><span class="sxs-lookup"><span data-stu-id="c1c81-130">![Freshservice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790809.png "Freshservice")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c1c81-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="c1c81-131">Configure single sign-on</span></span>

<span data-ttu-id="c1c81-132">The objective of this section is to outline how to enable users to authenticate to FreshService with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="c1c81-132">The objective of this section is to outline how to enable users to authenticate to FreshService with their account in Azure AD using federation based on the SAML protocol.</span></span> 

<span data-ttu-id="c1c81-133">Configuring single sign-on for FreshService requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="c1c81-133">Configuring single sign-on for FreshService requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="c1c81-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="c1c81-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="c1c81-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1c81-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c1c81-136">In the Azure classic portal, on the **FreshService** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="c1c81-136">In the Azure classic portal, on the **FreshService** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c1c81-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790810.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c1c81-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790810.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="c1c81-138">On the **How would you like users to sign on to FreshService** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-138">On the **How would you like users to sign on to FreshService** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c1c81-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790811.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c1c81-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790811.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="c1c81-140">On the **Configure App URL** page, in the **FreshService Sign On URL** textbox, type your URL used by your users to sign on to your Freshdesk application (e.g.: **http://democompany.freshservice.com/**), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-140">On the **Configure App URL** page, in the **FreshService Sign On URL** textbox, type your URL used by your users to sign on to your Freshdesk application (e.g.: **http://democompany.freshservice.com/**), and then click **Next**.</span></span>
   
   <span data-ttu-id="c1c81-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790812.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="c1c81-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790812.png "Configure App URL")</span></span>
4. <span data-ttu-id="c1c81-142">On the **Configure single sign-on at FreshService** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="c1c81-142">On the **Configure single sign-on at FreshService** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="c1c81-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790813.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c1c81-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790813.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="c1c81-144">In a different web browser window, log into your FreshService company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c1c81-144">In a different web browser window, log into your FreshService company site as an administrator.</span></span>
6. <span data-ttu-id="c1c81-145">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-145">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="c1c81-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c1c81-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790814.png "Admin")</span></span>
7. <span data-ttu-id="c1c81-147">In the **Customer Portal**, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-147">In the **Customer Portal**, click **Security**.</span></span>
   
   <span data-ttu-id="c1c81-148">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790815.png "Security")</span><span class="sxs-lookup"><span data-stu-id="c1c81-148">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790815.png "Security")</span></span>
8. <span data-ttu-id="c1c81-149">In the **Security** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c1c81-149">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="c1c81-150">![Single Sign On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790816.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="c1c81-150">![Single Sign On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790816.png "Single Sign On")</span></span>
   
   1. <span data-ttu-id="c1c81-151">Switch **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-151">Switch **Single Sign On**.</span></span>
   2. <span data-ttu-id="c1c81-152">Select **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-152">Select **SAML SSO**.</span></span>
   3. <span data-ttu-id="c1c81-153">In the Azure classic portal, on the **Configure single sign-on at FreshService** dialog page, copy the **Remote Login URL** value, and then paste it into the **SAML Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c1c81-153">In the Azure classic portal, on the **Configure single sign-on at FreshService** dialog page, copy the **Remote Login URL** value, and then paste it into the **SAML Login URL** textbox.</span></span>
   4. <span data-ttu-id="c1c81-154">In the Azure classic portal, on the **Configure single sign-on at FreshService** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c1c81-154">In the Azure classic portal, on the **Configure single sign-on at FreshService** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
   5. <span data-ttu-id="c1c81-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Security Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="c1c81-155">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Security Certificate Fingerprint** textbox.</span></span>
   
      >[!TIP]
      ><span data-ttu-id="c1c81-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="c1c81-156">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span>
      >
9. <span data-ttu-id="c1c81-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="c1c81-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c1c81-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790817.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c1c81-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790817.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c1c81-159">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="c1c81-159">Configure user provisioning</span></span>

<span data-ttu-id="c1c81-160">In order to enable Azure AD users to log into FreshService, they must be provisioned into FreshService.</span><span class="sxs-lookup"><span data-stu-id="c1c81-160">In order to enable Azure AD users to log into FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="c1c81-161">In the case of FreshService, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="c1c81-161">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="c1c81-162">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1c81-162">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="c1c81-163">Log in to your **FreshService** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c1c81-163">Log in to your **FreshService** company site as an administrator.</span></span>
2. <span data-ttu-id="c1c81-164">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-164">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="c1c81-165">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c1c81-165">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790814.png "Admin")</span></span>
3. <span data-ttu-id="c1c81-166">In the **User Management** section, click **Requesters**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-166">In the **User Management** section, click **Requesters**.</span></span>
   
   <span data-ttu-id="c1c81-167">![Requesters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790818.png "Requesters")</span><span class="sxs-lookup"><span data-stu-id="c1c81-167">![Requesters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790818.png "Requesters")</span></span>
4. <span data-ttu-id="c1c81-168">Click **New Requester**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-168">Click **New Requester**.</span></span>
   
   <span data-ttu-id="c1c81-169">![New Requesters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790819.png "New Requesters")</span><span class="sxs-lookup"><span data-stu-id="c1c81-169">![New Requesters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790819.png "New Requesters")</span></span>
5. <span data-ttu-id="c1c81-170">In the **New Requester** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c1c81-170">In the **New Requester** section, perform the following steps:</span></span>
   
   <span data-ttu-id="c1c81-171">![New Requester](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790820.png "New Requester")</span><span class="sxs-lookup"><span data-stu-id="c1c81-171">![New Requester](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790820.png "New Requester")</span></span>   
   1. <span data-ttu-id="c1c81-172">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="c1c81-172">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="c1c81-173">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-173">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c1c81-174">The Azure Active Directory account holder will get an email including a link to confirm the account before it becomes active</span><span class="sxs-lookup"><span data-stu-id="c1c81-174">The Azure Active Directory account holder will get an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="c1c81-175">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="c1c81-175">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="c1c81-176">Assign users</span><span class="sxs-lookup"><span data-stu-id="c1c81-176">Assign users</span></span>
<span data-ttu-id="c1c81-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="c1c81-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c1c81-178">**To assign users to FreshService, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c1c81-178">**To assign users to FreshService, perform the following steps:**</span></span>

1. <span data-ttu-id="c1c81-179">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="c1c81-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c1c81-180">On the **FreshService** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="c1c81-180">On the **FreshService** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c1c81-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790821.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="c1c81-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC790821.png "Assign Users")</span></span>
3. <span data-ttu-id="c1c81-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="c1c81-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="c1c81-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="c1c81-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshservice-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c1c81-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c1c81-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c1c81-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1c81-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















