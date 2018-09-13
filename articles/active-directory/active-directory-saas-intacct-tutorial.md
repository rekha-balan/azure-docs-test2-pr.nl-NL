---
title: 'Tutorial: Azure Active Directory integration with Intacct | Microsoft Docs'
description: Learn how to use Intacct with Azure Active Directory to enable single sign-on, automated provisioning, and more.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 6cc07afc1615e42554b991791b33d67652401690
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554783"
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="a3d57-103">Tutorial: Azure Active Directory integration with Intacct</span><span class="sxs-lookup"><span data-stu-id="a3d57-103">Tutorial: Azure Active Directory integration with Intacct</span></span>
<span data-ttu-id="a3d57-104">The objective of this tutorial is to show the integration of Azure and Intacct.</span><span class="sxs-lookup"><span data-stu-id="a3d57-104">The objective of this tutorial is to show the integration of Azure and Intacct.</span></span>  
<span data-ttu-id="a3d57-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a3d57-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a3d57-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a3d57-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a3d57-107">An Intacct tenant</span><span class="sxs-lookup"><span data-stu-id="a3d57-107">An Intacct tenant</span></span>

<span data-ttu-id="a3d57-108">After you complete this tutorial, the Azure Active Directory (Azure AD) users you have assigned to Intacct will be able to sign in to the application at your Intacct company site (service provider initiated sign-on), or use the [Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3d57-108">After you complete this tutorial, the Azure Active Directory (Azure AD) users you have assigned to Intacct will be able to sign in to the application at your Intacct company site (service provider initiated sign-on), or use the [Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a3d57-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a3d57-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="a3d57-110">Enabling the application integration for Intacct</span><span class="sxs-lookup"><span data-stu-id="a3d57-110">Enabling the application integration for Intacct</span></span>
* <span data-ttu-id="a3d57-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3d57-111">Configuring single sign-on</span></span>
* <span data-ttu-id="a3d57-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a3d57-112">Configuring user provisioning</span></span>
* <span data-ttu-id="a3d57-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a3d57-113">Assigning users</span></span>

<span data-ttu-id="a3d57-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790030.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a3d57-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790030.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-intacct"></a><span data-ttu-id="a3d57-115">Enable the application integration for Intacct</span><span class="sxs-lookup"><span data-stu-id="a3d57-115">Enable the application integration for Intacct</span></span>
<span data-ttu-id="a3d57-116">The objective of this section is to outline how to enable the application integration for Intacct.</span><span class="sxs-lookup"><span data-stu-id="a3d57-116">The objective of this section is to outline how to enable the application integration for Intacct.</span></span>

<span data-ttu-id="a3d57-117">**To enable the application integration for Intacct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3d57-117">**To enable the application integration for Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="a3d57-118">In the Azure classic portal, in the left pane, click the Active Directory icon.</span><span class="sxs-lookup"><span data-stu-id="a3d57-118">In the Azure classic portal, in the left pane, click the Active Directory icon.</span></span>

   <span data-ttu-id="a3d57-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a3d57-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a3d57-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a3d57-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a3d57-121">To open the applications view, in the directory view, click **Applications** on the top menu.</span><span class="sxs-lookup"><span data-stu-id="a3d57-121">To open the applications view, in the directory view, click **Applications** on the top menu.</span></span>

   <span data-ttu-id="a3d57-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a3d57-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a3d57-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a3d57-123">Click **Add** at the bottom of the page.</span></span>

   <span data-ttu-id="a3d57-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a3d57-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a3d57-125">On the **What do you want to do** page, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-125">On the **What do you want to do** page, click **Add an application from the gallery**.</span></span>

   <span data-ttu-id="a3d57-126">![Add an application from the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC749322.png "Add an application from gallery")</span><span class="sxs-lookup"><span data-stu-id="a3d57-126">![Add an application from the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC749322.png "Add an application from gallery")</span></span>
6. <span data-ttu-id="a3d57-127">In the search box, enter **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-127">In the search box, enter **Intacct**.</span></span>

   <span data-ttu-id="a3d57-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790031.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a3d57-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790031.png "Application Gallery")</span></span>
7. <span data-ttu-id="a3d57-129">In the results pane, select **Intacct**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a3d57-129">In the results pane, select **Intacct**, and then click **Complete** to add the application.</span></span>

   <span data-ttu-id="a3d57-130">![Intacct](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790032.png "Intacct")</span><span class="sxs-lookup"><span data-stu-id="a3d57-130">![Intacct](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790032.png "Intacct")</span></span>

## <a name="configure-single-sign-on"></a><span data-ttu-id="a3d57-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3d57-131">Configure single sign-on</span></span>

<span data-ttu-id="a3d57-132">The objective of this section is to outline how to enable users to authenticate to Intacct with their account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3d57-132">The objective of this section is to outline how to enable users to authenticate to Intacct with their account in Azure AD.</span></span> <span data-ttu-id="a3d57-133">Federation that is based on the SAML protocol is used for this authentication.</span><span class="sxs-lookup"><span data-stu-id="a3d57-133">Federation that is based on the SAML protocol is used for this authentication.</span></span>  

<span data-ttu-id="a3d57-134">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="a3d57-134">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="a3d57-135">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a3d57-135">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="a3d57-136">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3d57-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a3d57-137">In the Azure classic portal, on the **Intacct** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** page.</span><span class="sxs-lookup"><span data-stu-id="a3d57-137">In the Azure classic portal, on the **Intacct** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** page.</span></span>

   <span data-ttu-id="a3d57-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790033.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a3d57-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790033.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="a3d57-139">On the **How would you like users to sign on to Intacct** page, select **Windows Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-139">On the **How would you like users to sign on to Intacct** page, select **Windows Azure AD Single Sign-On**, and then click **Next**.</span></span>

   <span data-ttu-id="a3d57-140">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790034.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a3d57-140">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790034.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="a3d57-141">On the **Configure App URL** page, in the **Sign On URL** box, enter your URL that uses the *https://Intacct.com/company* pattern, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-141">On the **Configure App URL** page, in the **Sign On URL** box, enter your URL that uses the *https://Intacct.com/company* pattern, and then click **Next**.</span></span>

   <span data-ttu-id="a3d57-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790035.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a3d57-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790035.png "Configure App URL")</span></span>
4. <span data-ttu-id="a3d57-143">On the **Configure single sign-on at Intacct** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a3d57-143">On the **Configure single sign-on at Intacct** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>

   <span data-ttu-id="a3d57-144">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790036.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a3d57-144">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790036.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="a3d57-145">In a different web browser window, sign in to your Intacct company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a3d57-145">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>
6. <span data-ttu-id="a3d57-146">Click the **Company** tab, and then click **Company Info**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-146">Click the **Company** tab, and then click **Company Info**.</span></span>

   <span data-ttu-id="a3d57-147">![Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790037.png "Company")</span><span class="sxs-lookup"><span data-stu-id="a3d57-147">![Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790037.png "Company")</span></span>
7. <span data-ttu-id="a3d57-148">Click the **Security** tab, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-148">Click the **Security** tab, and then click **Edit**.</span></span>

   <span data-ttu-id="a3d57-149">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790038.png "Security")</span><span class="sxs-lookup"><span data-stu-id="a3d57-149">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790038.png "Security")</span></span>
8. <span data-ttu-id="a3d57-150">In the **Single sign on (SSO)** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3d57-150">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

   <span data-ttu-id="a3d57-151">![Single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790039.png "single sign on")</span><span class="sxs-lookup"><span data-stu-id="a3d57-151">![Single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790039.png "single sign on")</span></span>

   1. <span data-ttu-id="a3d57-152">Select **Enable single sign on**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-152">Select **Enable single sign on**.</span></span>
   2. <span data-ttu-id="a3d57-153">As **Identity provider type**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-153">As **Identity provider type**, select **SAML 2.0**.</span></span>
   3. <span data-ttu-id="a3d57-154">In the Azure classic portal, on the **Configure single sign-on at Intacct** page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** box.</span><span class="sxs-lookup"><span data-stu-id="a3d57-154">In the Azure classic portal, on the **Configure single sign-on at Intacct** page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** box.</span></span>
   4. <span data-ttu-id="a3d57-155">In the Azure classic portal, on the **Configure single sign-on at Intacct** page, copy the **Remote Login URL** value, and then paste it into the **Login URL** box.</span><span class="sxs-lookup"><span data-stu-id="a3d57-155">In the Azure classic portal, on the **Configure single sign-on at Intacct** page, copy the **Remote Login URL** value, and then paste it into the **Login URL** box.</span></span>
   5. <span data-ttu-id="a3d57-156">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="a3d57-156">Create a **base-64 encoded** file from your downloaded certificate.</span></span> <span data-ttu-id="a3d57-157">For more information, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a3d57-157">For more information, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>      
   6. <span data-ttu-id="a3d57-158">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="a3d57-158">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   7. <span data-ttu-id="a3d57-159">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-159">Click **Save**.</span></span>
9. <span data-ttu-id="a3d57-160">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign-On** page.</span><span class="sxs-lookup"><span data-stu-id="a3d57-160">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign-On** page.</span></span>

   <span data-ttu-id="a3d57-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790040.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a3d57-161">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790040.png "Configure Single Sign-On")</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="a3d57-162">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a3d57-162">Configure user provisioning</span></span>

<span data-ttu-id="a3d57-163">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span><span class="sxs-lookup"><span data-stu-id="a3d57-163">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="a3d57-164">For Intacct, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a3d57-164">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="a3d57-165">**To provision user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3d57-165">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="a3d57-166">Sign in to your **Intacct** tenant.</span><span class="sxs-lookup"><span data-stu-id="a3d57-166">Sign in to your **Intacct** tenant.</span></span>
2. <span data-ttu-id="a3d57-167">Click the **Company** tab, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-167">Click the **Company** tab, and then click **Users**.</span></span>

   <span data-ttu-id="a3d57-168">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790041.png "Users")</span><span class="sxs-lookup"><span data-stu-id="a3d57-168">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790041.png "Users")</span></span>
3. <span data-ttu-id="a3d57-169">Click the **Add** tab.</span><span class="sxs-lookup"><span data-stu-id="a3d57-169">Click the **Add** tab.</span></span>

   <span data-ttu-id="a3d57-170">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790042.png "Add")</span><span class="sxs-lookup"><span data-stu-id="a3d57-170">![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790042.png "Add")</span></span>
4. <span data-ttu-id="a3d57-171">In the **User Information** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3d57-171">In the **User Information** section, perform the following steps:</span></span>

   <span data-ttu-id="a3d57-172">![User Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790043.png "User Information")</span><span class="sxs-lookup"><span data-stu-id="a3d57-172">![User Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790043.png "User Information")</span></span>

   1. <span data-ttu-id="a3d57-173">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span><span class="sxs-lookup"><span data-stu-id="a3d57-173">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>
   2. <span data-ttu-id="a3d57-174">Select the **Admin privileges** of an Azure AD account that you want to provision.</span><span class="sxs-lookup"><span data-stu-id="a3d57-174">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   3. <span data-ttu-id="a3d57-175">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-175">Click **Save**.</span></span> <span data-ttu-id="a3d57-176">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="a3d57-176">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="a3d57-177">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span><span class="sxs-lookup"><span data-stu-id="a3d57-177">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
>

## <a name="assign-users"></a><span data-ttu-id="a3d57-178">Assign users</span><span class="sxs-lookup"><span data-stu-id="a3d57-178">Assign users</span></span>
<span data-ttu-id="a3d57-179">To test your configuration, you need to assign Azure AD users to Intacct.</span><span class="sxs-lookup"><span data-stu-id="a3d57-179">To test your configuration, you need to assign Azure AD users to Intacct.</span></span> <span data-ttu-id="a3d57-180">After a user is assigned, they can access your application.</span><span class="sxs-lookup"><span data-stu-id="a3d57-180">After a user is assigned, they can access your application.</span></span>

<span data-ttu-id="a3d57-181">**To assign users to Intacct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3d57-181">**To assign users to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="a3d57-182">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a3d57-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a3d57-183">On the **Intacct** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-183">On the **Intacct** application integration page, click **Assign users**.</span></span>

   <span data-ttu-id="a3d57-184">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790044.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="a3d57-184">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790044.png "Assign users")</span></span>
3. <span data-ttu-id="a3d57-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a3d57-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>

   <span data-ttu-id="a3d57-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a3d57-186">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a3d57-187">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a3d57-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a3d57-188">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3d57-188">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a3d57-189">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a3d57-189">Assign the Azure AD test user</span></span>

<span data-ttu-id="a3d57-190">In this section, you set up Britta Simon to use Azure single sign-on by granting Britta access to Intacct.</span><span class="sxs-lookup"><span data-stu-id="a3d57-190">In this section, you set up Britta Simon to use Azure single sign-on by granting Britta access to Intacct.</span></span>

![Assign user][200]

<span data-ttu-id="a3d57-192">**To assign Britta Simon to Intacct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3d57-192">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="a3d57-193">In the Azure portal, open the applications view, go to the directory view, go to **Enterprise applications**, and then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-193">In the Azure portal, open the applications view, go to the directory view, go to **Enterprise applications**, and then click **All applications**.</span></span>

    ![Assign user][201]

2. <span data-ttu-id="a3d57-195">In the applications list, select **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-195">In the applications list, select **Intacct**.</span></span>

    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_intacct_50.png)

3. <span data-ttu-id="a3d57-197">On the **Manage** menu, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-197">On the **Manage** menu, click **Users and groups**.</span></span>

    ![Assign user][202]

4. <span data-ttu-id="a3d57-199">Click the **Add** button, and then in **Add Assignment**, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a3d57-199">Click the **Add** button, and then in **Add Assignment**, select **Users and groups**.</span></span>

    ![Assign user][203]

5. <span data-ttu-id="a3d57-201">In **Users and groups**, select **Britta Simon** from the user's list.</span><span class="sxs-lookup"><span data-stu-id="a3d57-201">In **Users and groups**, select **Britta Simon** from the user's list.</span></span>

6. <span data-ttu-id="a3d57-202">In **Users and groups**, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="a3d57-202">In **Users and groups**, click the **Select** button.</span></span>

7. <span data-ttu-id="a3d57-203">In **Add Assignment**, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="a3d57-203">In **Add Assignment**, click the **Assign** button.</span></span>



### <a name="test-single-sign-on"></a><span data-ttu-id="a3d57-204">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3d57-204">Test single sign-on</span></span>

<span data-ttu-id="a3d57-205">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a3d57-205">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="a3d57-206">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span><span class="sxs-lookup"><span data-stu-id="a3d57-206">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a3d57-207">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a3d57-207">Additional resources</span></span>

* [<span data-ttu-id="a3d57-208">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3d57-208">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3d57-209">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3d57-209">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_203.png






























